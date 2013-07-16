= Webui Config Editor =

We are hoping to get a web developer to help out with a new config editor for the webui, thought I'd sketch out some ideas on how I think it could work.

The general idea is that we now have JSON schemas describing the whole config, including which options each plugin takes. We can use jsonary to render the config (in json format) with custom html/css based on these schemas. Jsonary already does much of what is described below, we just need to configure it for a couple different views.

=== Config Overview ===
I'm thinking have the whole config in non-editable form on the first page, with +/- expander for each section, so you can get a quick compact overview. Have buttons to create a new task or preset, and have edit and delete buttons next to the existing tasks or preset.

=== Edit Task/Preset ===
Have a separate view once you click on add/edit task, just for editing that particular task. It will have a list of available plugins to add to the task, divided into their logical category. Have some sort of description expandable, or maybe on mouseover, possibly also a link to the wiki page for that plugin. In the main edit view, appropriate controls are rendered based on option types, e.g. booleans have a checkbox, integers have a spin edit button, lists have an 'add item' button. When adding a new plugin, all of the required options will show up automatically for the user to fill in, and beneath that have a list of other options that can be defined for the plugin, with mouseover descriptions again maybe. Clicking on one adds that option to be filled in with an edit control. Descriptions for options still need to be added to the schemas, as well as metadata like descriptions of plugins themselves.