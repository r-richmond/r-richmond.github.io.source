---
title: "Exploring Complex Types in BigQuery"
date: 2018-09-23
draft: false
categories : [
    "Analyst",
]
tags: ["SQL",
      "BigQuery",
      ]
---

# Introduction

Google's BigQuery has support for complex types (arrays & structs) which are relatively new in analytical databases.
While the ideas and of arrays and structs aren't unique to BigQuery some of the syntax and capabilities are unique.
In this post I'll be going over what I've found to be the most useful patterns and tricks.

## Arrays
Put plainly an array is a series of values of the same type stored within a single value.
You can create array literals via brackets `[]` as demonstrated by the following snippet.
```sql
select [1, 2, 3] as array_of_ints
```
You can also explicitly declare the type of an array as follows.
```sql
select
  ['2018-01-01', '2018-02-01', '2018-03-01'] as array_of_string,
  array<date>['2018-01-01', '2018-02-01', '2018-03-01'] as array_of_date
```
## Structs
A struct is a grouping of values that need not be of the same type and is very similar to the concept of tuples.
They are commonly used to group related values together.
You can create struct literals using the function struct
```sql
select struct(1 as id, 2 as value) as user_info
```
## Purpose
Arrays and structs allow for a more compact organization of related data which makes writing and reading many queries easier.
So while BigQuery is the engine that I'm covering today I expect these concepts to spread to other databases as knowledge of their utility spreads.

# Basic Usage
## Example DataSet
I'll be using the following CTE to demonstrate various functions for arrays & structs.
```sql
with data_sample as (
  select
    1 as id_race,
    date'2018-08-01' as date_race,
    [3, 4] as id_participants,
    [ struct(7.0 as distance, 1 as lap_number, [struct(3 as id_participant, 1 as position),
                                                struct(4 as id_participant, 2 as position)] as finish_order),
      struct(6.5 as distance, 2 as lap_number, [struct(3 as id_participant, 1 as position),
                                                struct(4 as id_participant, 2 as position)] as finish_order),
      struct(7.2 as distance, 3 as lap_number, [struct(4 as id_participant, 1 as position),
                                                struct(3 as id_participant, 2 as position)] as finish_order)
      ] as race_laps
  union all
  select
    2 as id_race,
    date'2018-08-08' as date_race,
    [3, 5] as id_participants,
    [ struct(7.5 as distance, 1 as lap_number, [struct(5 as id_participant, 1 as position),
                                                struct(3 as id_participant, 2 as position)] as finish_order),
      struct(7.4 as distance, 2 as lap_number, [struct(5 as id_participant, 1 as position),
                                                struct(3 as id_participant, 2 as position)] as finish_order),
      struct(7.3 as distance, 3 as lap_number, [struct(5 as id_participant, 1 as position),
                                                struct(3 as id_participant, 2 as position)] as finish_order)
      ] as race_laps
)
```
## Access an individual element from an array
```sql
with data_sample as (
  --See above
  --Note: these lines will be omitted from subsequent examples
)
select
  ds.id_participants[offset(0)] as first_participant, --zero based
  ds.id_participants[ordinal(1)] as first_participant_also --one based
from data_sample as ds
```
## Determine the length of an array
```sql
select
  array_length(ds.id_participants) as number_of_participants
from data_sample as ds
```
## Access values & structs within an array
There are a couple of different ways to interact with arrays in BigQuery. The following three examples show different ways to access the example data structure and calculate the total distance for each race.
### by joining the lap array
```sql
select
  ds.id_race,
  sum(rl.distance) as race_distance
from data_sample as ds
join ds.race_laps as rl
group by 1
```
### by unnesting the lap array
```sql
select
  ds.id_race,
  sum(rl.distance) as race_distance
from data_sample as ds,
unnest(ds.race_laps) as rl
group by 1
```
### by using at inline query
```sql
select
  ds.id_race,
  (select sum(rl.distance) from unnest(ds.race_laps) as rl) as race_distance
from data_sample as ds
```
### by joining multiple arrays
The following query returns a list of race ids & participants ids & and a comma separated string showing that participants place each lap of each race.
```sql
select
  ds.id_race,
  fo.id_participant,
  string_agg(cast(fo.position as string), ', ' order by rl.lap_number) lap_positions
from data_sample as ds
join ds.race_laps as rl
join rl.finish_order as fo
group by 1, 2
```
## Filtering by contents of an array
```sql
select
  ds.id_race
from data_sample as ds
where 3 in unnest(ds.id_participants)
```
