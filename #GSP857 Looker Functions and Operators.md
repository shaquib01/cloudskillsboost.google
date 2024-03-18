## FOR FEW CHANGES WATCH VIDEO
```
https://www.youtube.com/watch?v=dOzjipAOmZY
```
# Place in `faa` model
## TASK 1:-

```
explore: +flights {
  query: start_from_here{
      dimensions: [depart_week, distance_tiered]
      measures: [count]
      filters: [flights.depart_date: "2003"]
    }
  }
```
```
Flight Count by Departure Week and Distance Tier
```

## TASK 2:-
```
# Place in `faa` model
explore: +flights {
  query: start_from_here{
      dimensions: [aircraft_origin.state]
      measures: [percent_cancelled]
      filters: [flights.depart_date: "2000"]
    }
  }
```
```
Percent of Flights Cancelled by State in 2000
```
## TASK 3:-
```
# Place in `faa` model
explore: +flights {
    query: start_from_here{
      dimensions: [aircraft_origin.state]
      measures: [cancelled_count, count]
      filters: [flights.depart_date: "2004"]
    }
}
```
```
Percent of Flights Cancelled by Aircraft Origin 2004
```


## TASK 4:-
```
# Place in `faa` model
explore: +flights {
    query: start_from_here{
      dimensions: [carriers.name]
      measures: [total_distance]
    }
}
```
```
Percent of Total Distance Flown by Carrier
```

## TASK 5:-
```
# Place in `faa` model
explore: +flights {
    query:start_from_here {
      dimensions: [depart_year, distance_tiered]
      measures: [count]
      filters: [flights.depart_date: "after 2000/01/01"]
    }
}
```
```
YoY Percent Change in Flights flown by Distance, 2000-Present
```
