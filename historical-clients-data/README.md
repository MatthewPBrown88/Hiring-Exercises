# Historical Clients Data

Progress of our clients in the app is tracked using statuses (prelead > lead > prospect > active > suspended).

To better understand this pipeline we want to see a report on how many clients have entered each status during each day.

Given an `example_clients` table (in `data.sql` file) with a PostgreSQL schema like this:

``` text
id bigint NOT NULL,  -- primary ID
created_at timestamp without time zone NOT NULL,  -- when the client was created
status character varying DEFAULT 'lead'::character varying NOT NULL,  -- current status of the client
status_history jsonb DEFAULT '{}'::jsonb NOT NULL  -- client's previous transitions between statuses in a format: `status_name: timestamptz`
```

write a query to generate a table like this:

``` text
| Day        | Preleads | Leads | Prospects | Active | Suspended |
|------------+----------+-------+-----------+--------+-----------|
| 2021-07-01 |       20 |    10 |         5 |      6 |        10 |
| 2021-07-02 |       15 |     7 |         4 |      5 |        13 |
| ...        |      ... |   ... |       ... |    ... |       ... |
```

where numbers are counts of clients that entered specified status during specified day. If client has enetered several statuses during the same day, counts for both statuses should be incremented.
