# Season Packs
## Reasoning 

Season packs can be a great source quickly download/back filling required episodes.
With a well-formed season pack this would actually be preferable for back-filling. This would also empower the search plugin.

## Problem

* Flexget currently handles each torrent file as a unique entity, and season packs do not conform to that schema.
* Passing on parts of the torrent file is a feature not guaranteed to be supported in all torrent clients 
* At least one popular tracker has adopted removing all season episodes and reposting as season packs as soon as a season is complete.

## Proposed solution

The implementation will be divided into several phases where each one should ideally be pushed to master  before the other one, to reduce the risk of noise and issues that may occur.

* Season pack file will be downloaded as a whole, there will be no attempt to split it, pass parts of it or any other manipulation.
* Series parser should know how to correctly match season packs.
* `Season` will be added as a new DB entity. It will link to its relevant `Episode` objects.
* `Season` object will have a `completed` attribute that will be set to `True` when a season pack has been downloaded.
* Series tracking will continue to follow conventional style, meaning season packs will respect `begin` attribute.
* If a season pack was accepted, the `begin` value will be set to the 1st episode of the next season.
* Needless to say, this should **NOT** affect any tracking for users that did not define `season_packs` in config.

### Phase 1: Accept a season pack from a feed:
Configure `series` plugin to accept a season pack if comnfigured to do so:
```yaml
series:
- foo:
    season_packs: yes
mock:
  - {title="Foo.S01.720p-Flexget}
```
Enable searching for season packs *first* when season packs are configured:
```yaml
discover:
  what:
    - next_series_episodes: yes
  from:
    - search_site: yes
series:
- foo:
    season_packs: yes
```
Enable different modes:
```yaml
series:
- foo:
    season_packs: only # Will reject any non-season pack (Episodes)
- bar:
    season_packs: yes # Will accept season pack if no episodes for this season have been downloaded (equivilant to setting `0`)
- baz:
    season_packs: 1 # Override episode threshold, set any integer as episode threshold
- bla:
    season_packs: loose # Will disregared episode threshold, always fetch season pack for a non-completed season
```
### Phase 2: CLI/API support and adjustments

- Series CLI operations should support this new mode (correctly display season packs where relevant)
- API upgrade and adjustments (**Note:** This will probably not be backwards compatible with current API, may require API versioning feature first)

### Phase 3: Support partial season packs
Some series seasons are released in more than 1 part:  
`Some.Show.S03.PART.1.720p` and `Some.Show.S03.PART.2.720p`
***

## Pitfalls

* Verify series parser will be able to identify a wide variety of season pack format (`SXX, Season XX, EXX-EXX, etc.)
- If a season pack is accepted, all other episodes for the same season should npt be accepted in the same task (search for/sort season packs first)
- `guessit` does not support season packs, make sure it doesn't crash


## Open questions

- Should manually setting `begin` set all lower seasons as completed?
- Not sure how to handle `complete` packages (`Foo.COMPLETE.720p-Flexget`). Should we add a `completed` attribute to `Series` as well?