= Cloudflare Scraper =
Enables cloudflare scraping in a task. Useful if you are using [wiki:Plugins/html html] to scrape a site that utilizes Cloudflares anti-bot services.

Requires cfscrape and a Javascript engine. Simply follow the installation instructions at https://github.com/Anorov/cloudflare-scrape.

'''Warning:''' When Cloudflare updates its anti-botting measures, this plugin may cease to function. Always make sure cfscrape is uptodate.
{{{
cfscraper: yes
}}}