= How to create plugins in test driven way =

Create (beginning of) new plugin. In our example: plugin_hello.py

{{{
from flexget.plugin import register_plugin


class PluginHello(object):
    """Short description of what this plugin does."""

    def on_task_filter(self, task, config):
        """Work on entries in the filter phase."""
        for entry in task.entries:
            log.debug('hello there %s' % entry['title'])


register_plugin(PluginHello, 'hello', api_ver=2)
}}}

Now, how can you test how this plugin works? Easy, create a test case for it.

Add new testcase file into tests. In our case: test_hello.py

{{{
from tests import FlexGetBase


class TestHello(FlexGetBase):
    
    __yaml__ = """
        tasks:
          test:
            mock:                 # let's use this plugin to create test data
              - {title: 'foobar'} # we can omit url if we do not care about it, in this case mock will add random url
            hello: yes            # our plugin, no relevant configuration yet ...
    """
    
    def test_feature(self):
        # run the task
        self.execute_task('test')
        assert False, 'incomple tests' # causes test to fail and log to be displayed
}}}

And to run the newly added test:
{{{
bin/nosetests test_hello.py:TestHello.test_feature
}}}
Note that {{{:TestHello}}} and {{{.testFeature}}} are optional, you can run just test the whole file as well:
{{{
bin/nosetests test_hello.py
}}}
To run all project tests (a good thing to do before committing changes):
{{{
bin/paver test
}}}

Once the plugin is starting to work like it should, you can add more actual real tests. See existing tests for more tips.

Happy coding! :)
