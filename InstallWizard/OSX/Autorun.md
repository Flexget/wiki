# [Install Wizard](/InstallWizard) > [OSX](/InstallWizard/OSX) > Autorun

## Autorun
There are two options for launching FlexGet as a daemon at startup. You can use the macOS launcher package, or setup a launch agent.

### Launcher Package
Please note that the launcher package *was not created, and is not maintained, by Flexget*. Questions or issues regarding the app bundle should be directed to the [issues page](https://github.com/tubedogg/FlexgetDaemon/issues).

The launcher package simply reads your `~/.bash_profile` file and starts the FlexGet daemon.

1. Download the launcher package from [GitHub](https://github.com/tubedogg/FlexgetDaemon).
2. Unzip it and move it to your Applications folder (or anywhere you'd like).
3. Add it to System Preferences > Users > \<your user\> > Startup Items.


### Launch Agent
Create /Users/USERNAME/Library/LaunchAgents/com.flexget.plist with:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>  
	<key>Label</key>
	<string>com.flexget</string>
	<key>ProgramArguments</key>
	<array> 
		<string>/usr/local/bin/flexget</string>
		<string>--cron</string>
		<string>execute</string>
	</array>
	<key>Nice</key>
	<integer>1</integer>
	<key>StartInterval</key>
	<integer>900</integer>
	<key>RunAtLoad</key>
	<true/>
</dict>
</plist>
```

**Note**: On some systems, FlexGet installs itself into `/bin/flexget` instead of `/usr/local/bin/flexget`; type `which flexget` to find out where the FlexGet binary is located and modify `com.flexget.plist` accordingly.

Then:

```
launchctl load -w /Users/USERNAME/Library/LaunchAgents/com.flexget.plist
```

When upgrading, use this to unload the plist:

```
launchctl unload /Users/USERNAME/Library/LaunchAgents/com.flexget.plist
```

If you want to check if Flexget is running, use

```
launchctl list | grep flexget
```

If the process is running, you'll see a process ID in the first column, followed by the last exit status. If the second column isn't 0, check your log file for errors.

Check the launchd man page for other options.