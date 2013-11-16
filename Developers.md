[[PageOutline]]

View the documentation and tutorials at [https://flexget.readthedocs.org/en/latest/ flexget.readthedocs.org]

=== Resources ===

 * [http://techspot.zzzeek.org/2012/02/07/patterns-implemented-by-sqlalchemy/ Good overview of SQLAlchemy concepts]

== Contributing ==

Making custom plugins should be easy for anyone with some python experience.

If you're working on good re-usable plugin we're be more than happy to include it in official distribution. See [wiki:Contribute] for more information.

=== Task execution UML ===

Only most important phases shown.

{{{
#!SequenceDiagram
participant Task
participant Input
participant Filter
participant Download
participant Output

Task->Input: Execute Input(s)
Input->Task: Add entries
Task->Task: Purge Rejected, Failed
Task->Filter: Execute Filter(s)
Filter->Task: Reject entries
Filter->Task: Accept entries
Task->Task: Purge Rejected, Failed
Task->Download: Execute Download(s)
Task->Task: Purge Rejected, Failed
Task->Output: Execute Output(s)
'}}}

=== Other phases ===

 * on_task_abort(self, task, config)


== Unit testing ==

!FlexGet has over 200 unit tests so changes are that if your modifications pass the tests nothing major has been broken. We also have CI at [http://ci.flexget.com].

== Running IPython inside !FlexGet ==

First install IPython

{{{
bin/easy_install ipython
}}}

And then place this where you wish to hack:

{{{
import IPython; IPython.embed()
}}}

-------------------------
Thanks to !JetBrains for the free open source !PyCharm license!

[[Image(pycharm_logo.gif, 200px, link=http://www.jetbrains.com/pycharm/)]]
