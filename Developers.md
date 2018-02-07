# Documentation
View the documentation and tutorials at [flexget.readthedocs.org](https://flexget.readthedocs.org/en/latest/)

### Python2/3 Compatibility
We use python-future [http://python-future.org/](http://python-future.org/) for python2/3 compatibily. See the cheat-sheet for more information [http://python-future.org/compatible_idioms.html](http://python-future.org/compatible_idioms.html)

Within flexget every python module must import the following for python2/3 compatibility. 

```python
from __future__ import unicode_literals, division, absolute_import
from builtins import *
```


### Resources
 * [Good overview of SQLAlchemy concepts](http://techspot.zzzeek.org/2012/02/07/patterns-implemented-by-sqlalchemy/)

## Contributing
Making custom plugins should be easy for anyone with some python experience.

If you're working on good re-usable plugin we're be more than happy to include it in official distribution. See [Contribute](/Contribute) for more information.

## Unit testing
FlexGet has over 200 unit tests so changes are that if your modifications pass the tests nothing major has been broken. We also have CI at [http://ci.flexget.com](http://ci.flexget.com).

## Enhancement proposals
 * [Drafts](/_index/Drafts/)
 * [Roadmap](/Roadmap)

## Running IPython inside FlexGet
First install IPython

```bash
bin/pip install ipython
```

And then place this where you wish to hack:

```
import IPython; IPython.embed()
```

-------------------------
Thanks to JetBrains for the free open source PyCharm license!


<img src="https://d3nmt5vlzunoa1.cloudfront.net/pycharm/files/2015/12/PyCharm_400x400_Twitter_logo_white.png" width=200 link=https://www.jetbrains.com/pycharm/ alt="pycharm logo">  

### Attachments  

* [events in feed](/attachments/Developers/flexget_events.png)
