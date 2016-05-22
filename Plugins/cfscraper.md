= Cloudflare Scraper =
Enables cloudflare scraping in a task. Useful if you are using [wiki:Plugins/html html] to scrape a site that utilizes Cloudflares anti-bot services.

Requires cfscrape and a Javascript engine. Simply follow the installation instructions at https://github.com/Anorov/cloudflare-scrape.

'''Warning:''' The author of Cloudflare-Scrape does not guarantee 100% safety against malicious attacks targetting any vulnerability in Cloudflare-Scrape. Precautions have been taken, but nothing is ever really safe when executing arbitrary code.

'''Note:''' When Cloudflare updates its anti-botting measures, this plugin may cease to function. Always make sure cfscrape is uptodate. Follow the instructions at https://github.com/Anorov/cloudflare-scrape#updates if it stops working.
{{{
cfscraper: yes
}}}

If execution fails, then you may have to install cfscrape from git. Do the following
{{{
pip uninstall cfscrape
pip install https://github.com/Anorov/cloudflare-scrape/zipball/master
}}}