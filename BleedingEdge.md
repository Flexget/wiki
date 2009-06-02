= Bleeding edge users information =

Important notes for bleeding edge users:

== r661 - setup tools / pavement ==

After updating to this revision you need to run:

{{{
python bootstrap.py
}}}

!FlexGet executable has also been relocated, it is now in:

{{{
bin/flexget
}}}

Edit your cron to new location:

{{{
~/(install path)/bin/flexget -q
}}}