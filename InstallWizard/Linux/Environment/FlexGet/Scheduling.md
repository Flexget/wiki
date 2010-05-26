[[Include(wiki:InstallWizard/Partial/Crontab)]]

Note: If you're configuring flexget to execute via cron it will search by default for it's config.yml file in the home directory of the user cron runs as (usually root).  To modify this behavior use the -c option in your crontab line like this:


{{{
@hourly /usr/local/bin/flexget --cron -c /home/username/.flexget/config.yml
}}}
