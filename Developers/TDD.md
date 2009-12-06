= How to create plugins in test driven way =

First create some kind of plugin. In our example: module_hello.py

{{{
from flexget.plugin import *

class PluginHello:

    def on_feed_filter(self, feed):
        for entry in feed.entries:
            log.debug('hello there %s' % entry['title'])


register_plugin(PluginHello, 'hello')
}}}

Now, how can you test how this plugin works? Easy, create a test case for it.

Add new testcase file into tests. In our case: test_hello.py

{{{
from tests import FlexGetBase

class TestHello(FlexGetBase):
    
    __yaml__ = """
        feeds:
          test:
            mock:                 # let's use this plugin to create test data
              - {title: 'foobar'} # we can omit url if we do not care about it, in this case mock will add random url
            hello: yes            # our plugin, no relevant configuration yet ...
    """
    
    def test_feature(self):
        # run the feed
        self.execute_feed('test')
        assert False, 'incomple tests' # causes test to fail and log to be displayed
}}}

And to run the newly added test:

{{{
bin/nosetests tests/test_hello.py:TestHello.test_feature
}}}

Note that {{{:TestHello}}} and {{{.testFeature}}} are optional, you can run just whole file as well.

Once plugin is starting to work like it should, you can add more actual real tests. See existing tests for more tips.

Happy coding :)