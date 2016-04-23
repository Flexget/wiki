= Documentation =

View the documentation and tutorials at [https://flexget.readthedocs.org/en/latest/ flexget.readthedocs.org]

=== Python2/3 Compatibility ===

We use python-future [http://python-future.org/] for python2/3 compatibily. See the cheat-sheet for more information [http://python-future.org/compatible_idioms.html]

Within flexget every python module must import the following for python2/3 compatibility. 

{{{
from __future__ import unicode_literals, division, absolute_import
from builtins import *
}}}


=== Resources ===

 * [http://techspot.zzzeek.org/2012/02/07/patterns-implemented-by-sqlalchemy/ Good overview of SQLAlchemy concepts]

== Contributing ==

Making custom plugins should be easy for anyone with some python experience.

If you're working on good re-usable plugin we're be more than happy to include it in official distribution. See [wiki:Contribute] for more information.

== Unit testing ==

!FlexGet has over 200 unit tests so changes are that if your modifications pass the tests nothing major has been broken. We also have CI at [http://ci.flexget.com].

== Running IPython inside !FlexGet ==

First install IPython

{{{
bin/pip install ipython
}}}

And then place this where you wish to hack:

{{{
import IPython; IPython.embed()
}}}

-------------------------
Thanks to !JetBrains for the free open source !PyCharm license!

[[Image(pycharm_logo.gif, 200px, link=http://www.jetbrains.com/pycharm/)]]