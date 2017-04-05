# Exec
Executes commands on [entries](/Entry).

This plugin can take two configuration formats [simple](#SimpleConfiguration) and [advanced](#AdvancedConfiguration).

## Simple Configuration
With this configuration, your command is executed on all accepted entries that //reach output//.

You can use all (available) [entry](/Entry) fields in the command.

### Example
```
exec: echo "found {{title}} at {{url}}" >> file
```

It also accepts a list and will run the commands in order:

```
exec:
  - echo "found {{title}} at {{url}}" >> file
  - echo "Synopsis: {{imdb_plot_outline}}" >> {{movie_name}}.nfo
```

## Advanced Configuration
If you need more control over what entries and when the command gets executed, you can use the advanced configuration format. This requires some understanding of how the [internals](/Developers) of FlexGet work.

For example the simple form:

```
exec: echo "downloaded file {{output}}" >> file
```

is equivalent to the advanced form:

```
exec:
  on_output:
    for_accepted: echo "downloaded file {{output}}" >> file
```

**Format:**

```
exec:
  ON_PHASE_NAME:
    [phase: CMD]
    [FOR_ITEMS_NAME: CMD]
```

Where *ON_PHASE_NAME* must be one of:
- `on_start`
- `on_input`
- `on_filter`
- `on_output`
- `on_exit`

Where *FOR_ITEMS_NAME* must be one of:
- `for_entries`
- `for_accepted`
- `for_rejected`
- `for_failed`
- `for_undecided`

Where *CMD* is a single command or a list of commands to execute.

**Example:**

```
exec:
  on_start:
    phase: echo "Started"
  on_input:
    for_entries: echo "got {{title}}"
  on_output:
    for_accepted:
      - echo "accepted {{title}} - {{url}}" > file
      - echo "Synopsis: {{imdb_plot_outline}}" >> {{movie_name}}.nfo
```

See [entry documentation](/Entry) for list of possible fields.

### Fail entries option
Setting the `fail_entries` option to yes will cause the entry to fail if the executed command has a non-zero return code.
This option will also cause entries to fail that do not contain all of the variables needed for string substitution.

```
exec:
  fail_entries: yes
  on_output:
    for_accepted: echo "accepted {{title}} - {{url}}" > file
```

### Auto escape option
If one of your variables may contain characters that need to be escaped for the shell, you need to surround it by double quotes and use the `auto_escape` option. This will escape all double quotes inside the variable and therefore ensure that your surrounding double quotes will not cause any problems. The surrounding double quotes then take care of anything else that would need escaping otherwise. For example:
```
exec:
  auto_escape: yes
  on_output:
    for_accepted: echo accepted "{{title}}" - {{url}} > file
```

### Allow background option
Normally, FlexGet will wait the given command to finish so it can capture the return status and log the output. But if the command takes a long time to run (ex. direct downloads of large files), it will prevent further processing until the command completes. To fork the command into a background process so that FlexGet continues processing without delay, you not only have to add an ampersand (&) at the end of the command, you have to use the {{allow_background}} option. Note, this option will also prevent FlexGet from determining if the command failed, so it will not retry. A usage example:

```
exec:
  allow_background: yes
  auto_escape: yes
  on_output:
    for_accepted: get_flash_videos {{url}} &
```

## Notes for Windows Users
You may encounter problems on Windows machines with escaping and backgrounding.  Here are a few tips:

* Specifying a path for the executable itself is problematic.  The simplest solution is to place it in your path.  For example, this will result in parse errors even if you try using backslashes to escape the double quote, path backslashes, or both:

```
exec:
  for_accepted: "d:\Program Files\Aria\aria2c.exe" --log=aria.log <snip> "{{url}}"
```

* If you experience problems backgrounding your task, try using the "start" command.  In the above example, setting "allow_background: yes" and appending the & still wouldn't background the process.  This type of syntax should work:

```
exec:
  allow_background: yes
  on_output:
    for_accepted: start aria2c.exe --log=aria.log <snip> "{{url}}" &
```