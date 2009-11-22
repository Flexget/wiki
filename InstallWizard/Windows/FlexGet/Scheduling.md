= Configure =

Follow the [wiki:Configuration configuration tutorial] and make some basic configuration as a starting point.

Some windows specific tips:

You can place the configuration file anywhere you like. One good place is `C:\Documents and Settings\<your user>\.flexget\config.yml` as this location is automatically checked regardless where you execute `flexget` command. Another logical choice would be `c:\program files\flexget\config.yml`. If you opt later you'll need to specify the configuration file explicitly with `flexget -c <config>` if you run !FlexGet from anywhere else than this directory. This applies also if you use different name than `config.yml`.

= Scheduling =

Now, let's get !FlexGet to run once per hour!

Open ''Scheduling Tasks'' from windows ''Control panel''.

'''1.''' Create new Task

[[Image(wiki:WikiPics:scheduling_1.png)]]

'''2.''' Open the newly created task

[[Image(wiki:WikiPics:scheduling_2.png)]]

'''3.''' Command to execute. If you stored `config.yml` under `Documents and Settings\<user profile>\.flexget\` then the `Start in` is not necessary.

[[Image(wiki:WikiPics:scheduling_3.png)]]

'''4.''' Go into ''Schedule'' tab. And press ''Advanced'' button.

[[Image(wiki:WikiPics:scheduling_4.png)]]

'''5.''' Enter scheduling values.

[[Image(wiki:WikiPics:scheduling_5.png)]]

== Installation completed ==

If you encounter problems, feel free to join our IRC channel (`#FlexGet`) at freenode. Or request help via tickets if IRC isn't your thing.