# Internal memo
Currently:

```
series:
  - some serie:
      timeframe:
        hours: 4
        enough: 720p
  - another serie
  - third serie
```

Timeframe indentation causes a lot of problems for new users, also the **:** in **some serie**.

Alternative implementation:

```
series:
  - name: some serie
    timeframe:
      hours: 4
      enough: 720p
  - another serie
  - third serie
```

Difference? (in python)

```
Original:

{'some serie': {'timeframe': {'hours': 4, 'enough': '720p'}}}
another serie
third serie

VS:

{'name': 'some serie', 'timeframe': {'hours': 4, 'enough': '720p'}}
another serie
third serie
```