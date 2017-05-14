# [Install Wizard](/InstallWizard) > [Windows](/InstallWizard/Windows) > FlexGet
<div class="alert alert-warning" role="alert">

If you do not have the Python scripts directory in your [PATH](http://en.wikipedia.org/wiki/Environment_variable#System_path_variables) you will 
need to use the full path for commands 
`pip` and `flexget`. Otherwise you will get a "command not found" error. Find instructions on the previous page for [modifying your PATH](/InstallWizard/Windows#verify-python-is-in-your-path) to make your life easier!
</div>

### Install

Run this program as an administrator: `Start Menu` &rarr; `Accessories` &rarr; `Command Prompt`.

Type this command in the command prompt:
```cmd
pip install flexget
```

This will install FlexGet and all of the additional components it requires.

### Verify installation
Run this command in the command prompt:

```cmd
flexget -V
```
This should output the installed version.

## Continue
[Scheduling](/InstallWizard/Windows/FlexGet/Scheduling)

