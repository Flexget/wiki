# [Install Wizard](/InstallWizard) > [Windows](/InstallWizard/Windows) > Scheduling

## Configure
Follow the [configuration tutorial](/Configuration) and make a basic configuration file as a starting point.

### Windows-specific tips

You can place the configuration file anywhere you like. One good place is `C:\Documents and Settings\<your user>\flexget\config.yml` as this location is automatically checked regardless where you execute `flexget` command. Another logical choice would be `c:\program files\flexget\config.yml`.

If you opt later you'll need to specify the configuration file explicitly with `flexget -c <config>` if you run FlexGet from anywhere else than this directory. This applies also if you use different name than `config.yml`.

## Scheduling
Now, let's get FlexGet to run once per hour!

Open *Scheduling Tasks* from windows *Control panel*.

**1.** Create new Task

<img src="https://flexget.com/attachments/WikiPics/scheduling_1.png">

**2.** Open the newly created task

<img src="https://flexget.com/attachments/WikiPics/scheduling_2.png">

**3.** Command to execute. If you stored `config.yml` under `Documents and Settings\<user profile>\flexget\` then the `Start in` is not necessary. \\
**NOTE:**
- If you would like to avoid the cmd window popup, you can use the `flexget-headless` executable instead of plain `flexget`.
- If you have not added the python scripts folder to your PATH environment variable, you should use the full path to flexget in this step. i.e. `C:\Python26\Scripts\flexget-headless.exe --cron execute` for python 2.6

<img src="https://flexget.com/attachments/WikiPics/scheduling_3.png">

**4.** Go into *Schedule* tab. And press *Advanced* button.

<img src="https://flexget.com/attachments/WikiPics/scheduling_4.png">

**5.** Enter scheduling values.

<img src="https://flexget.com/attachments/WikiPics/scheduling_5.png">

# Done

Enjoy automation. If you encounter issues [ask for help](/NeedHelp)