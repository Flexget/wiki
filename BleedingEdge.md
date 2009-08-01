= Bleeding edge users information =

Important notes for bleeding edge users:

== r663 - dependency changes ==

If upgrading to this, run:

{{{
bin/paver clean
python bootstrap.py
}}}

== r661 - setup tools / pavement ==

After updating to this revision you need to run:

{{{
python bootstrap.py
}}}

If you get error about !BeautifulSoup add parameter {{{--no-site-packages}}}

!FlexGet executable has also been relocated, it is now in:

{{{
bin/flexget
}}}

Edit your cron to new location:

{{{
~/(install path)/bin/flexget -q
}}}