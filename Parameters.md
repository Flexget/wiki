# Parameters
*TODO: write this section! *
*NOTE: this should be generated and should be synced with the `flexget -h`'s output.*

usage: flexget.py [options](/options)

options:
```
-h, --help            show this help message and exit
  --test                Verbose what would happend on normal execution.
  --learn               Matches are not downloaded but will be skipped in the
                        future.
  --task=ONLYFEED       Run only specified feed from config.
  --no-cache            Disable caches. Works only in modules that have
                        explicit support.
  --reset-session       Forgets everything that has been downloaded and learns
                        current matches.
  --doc=DOC             Display module documentation (example: --doc
                        patterns). See --list.
  --list                List all available modules.
  --failed              List recently failed entries.
  --clear-failed        Clear recently failed list.
  -c CONFIG             Specify configuration file. Default is config.yml
  -q                    Disables stdout and stderr output. Logging is done
                        only to file.
  -d                    Display detailed process information.
  --cli-config=CLI_CONFIG
                        Configuration parameters trough commandline. See --doc
                        cli_config.
  --dl-path=DL_PATH     Override path for download module. Applies to all
                        executed feeds.
```