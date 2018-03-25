# Flexget V3 - Drop Py2 support

Python 2 EOL is 2020-01-01 which means now is a good time for us to start dropping it completely.

## Prepearations 

- Stabalize/add Online tests
- 

## Checklist:

- Research which dependencies we currently use that are py2 only
- Drop `future` and its realted libs usage
- Drop `builtins` usage
- 

### Py2 only deps that we'll drop/update and plugins that use them

- deluge/deluge
- mechanize (?)

## Open questions?

- Should we support "maintenance" stuff for flexget 2.x? Is it that even feasible with our current infrastructure?
- Is there any thing else we wanna change with this version? Maybe replace argparse with click?

