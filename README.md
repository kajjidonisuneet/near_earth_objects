## Near Earth Objects (NEOs) 

NEOs are any small Solar System body whose orbit brings it into proximity with Earth. This program is command-line tool to inspect and query a dataset of NEOs and their close approaches to Earth by querying data from  NASA/JPL's Center for Near Earth Object Studies.

This program is built to demonstrate the OOP in Python.


## Features
- To read the NEOs data from CSV/JSON files and represent the data in a python object.
- To filter the data based on criteria like distance, velocity, date, diameter, hazardous. 
- If required to write the filtered data in CSV/Json file.

## Getting Started

Download the NEOs and approach data from <a href='https://drive.google.com/drive/folders/1S6EL-foVzgLbOAg8STyif-prNDnHLdlL?usp=sharing'>here</a> and place them in data folder.

### Prerequisites
This program has no dependence.

### Installation

1. Clone the repo.
   ```bash
   git clone https://github.com/kajjidonisuneet/near_earth_objects.git
   ```
2. Make a folder named data and place both the downloaded files or user the command line arguments to provide file paths ```--neofile``` and ``` --cadfile ```.

## Usage

### List of Command Line Arguments (with example)

There are three main subcommand interface. ie ```inspect```, ```query``` and ```interactive```.

### `inspect`
This subcommand is used to inspect only a single NEO at at time. The NEO is specified with exactly one of the `--pdes` option (the primary designation) and the `--name` option (the IAU name). The `--verbose` flag additionally prints out, in a human-readable form, all known close approaches to Earth made by this NEO. 
Following are the some examples.

```bash
# Inspect the NEO with a primary designation of 433 (that's Eros!)
$ python3 main.py inspect --pdes 433
NEO 433 (Eros) has a diameter of 16.840 km and is not potentially hazardous.

# Inspect the NEO with an IAU name of "Halley" (that's Halley's Comet!)
$ python3 main.py inspect --name Halley
NEO 1P (Halley) has a diameter of 11.000 km and is not potentially hazardous.

# Verbosely list information about Ganymed and each of its known close approaches.
# For the record, Ganymed is HUGE - it's the largest known NEO.
$ python3 main.py inspect --verbose --name Ganymed
NEO 1036 (Ganymed) has a diameter of 37.675 km and is not potentially hazardous.
- On 1911-10-15 19:16, '1036 (Ganymed)' approaches Earth at a distance of 0.38 au and a velocity of 17.09 km/s.
- On 1924-10-17 00:51, '1036 (Ganymed)' approaches Earth at a distance of 0.50 au and a velocity of 19.36 km/s.
- On 1998-10-14 05:12, '1036 (Ganymed)' approaches Earth at a distance of 0.46 au and a velocity of 13.64 km/s.
- On 2011-10-13 00:04, '1036 (Ganymed)' approaches Earth at a distance of 0.36 au and a velocity of 14.30 km/s.
- On 2024-10-13 01:56, '1036 (Ganymed)' approaches Earth at a distance of 0.37 au and a velocity of 16.33 km/s.
- On 2037-10-15 18:31, '1036 (Ganymed)' approaches Earth at a distance of 0.47 au and a velocity of 18.68 km/s.

```
### `query`
This subcommand is bit more advance. A `query` subcommand generates a collection of close approaches that match a set of specified filters, and either displays a limited set of those results to standard output or writes the structured results to a file.

Following are list of filters and optional arguments.
#### Filters
- `-d DATE, --date DATE` Only return close approaches on the given date, in YYYY-MM-DD format (e.g. 2020-12-31).
- `-s START_DATE, --start-date START_DATE` Only return close approaches on or after the given date, in YYYY-MM-DD format (e.g. 2020-12-31).
- `-e END_DATE, --end-date END_DATE` Only return close approaches on or before the given date, in YYYY-MM-DD format (e.g. 2020-12-31).
- `--min-distance DISTANCE_MIN` In astronomical units. Only return close approaches that pass as far or farther away from Earth as the given
                        distance.
- ` --max-distance DISTANCE_MAX` In astronomical units. Only return close approaches that pass as near or nearer to Earth as the given
                        distance.
- `--min-velocity VELOCITY_MIN` In kilometers per second. Only return close approaches whose relative velocity to Earth at approach is as fast
                        or faster than the given velocity.
- `--max-velocity VELOCITY_MAX` In kilometers per second. Only return close approaches whose relative velocity to Earth at approach is as slow
                        or slower than the given velocity.
- `--min-diameter DIAMETER_MIN` In kilometers. Only return close approaches of NEOs with diameters as large or larger than the given size.
- `--max-diameter DIAMETER_MAX` In kilometers. Only return close approaches of NEOs with diameters as small or smaller than the given size.
-`--hazardous ` If specified, only return close approaches of NEOs that are potentially hazardous.
-`--not-hazardous` If specified, only return close approaches of NEOs that are not potentially hazardous.

#### Optional arguments
- `-l LIMIT, --limit LIMIT` The maximum number of matches to return. Defaults to 10 if no --outfile is given.
- `-o OUTFILE, --outfile OUTFIL` File in which to save structured results. If omitted, results are printed to standard output.

Few examples

```bash
# Show (the first) four close approaches in March 2020 that passed at least 0.4au of Earth.
$ python3 main.py query --start-date 2020-03-01 --end-date 2020-03-31 --min-distance 0.4 --limit 4
On 2020-03-01 00:28, '152561' approaches Earth at a distance of 0.42 au and a velocity of 11.23 km/s.
On 2020-03-01 09:28, '462550' approaches Earth at a distance of 0.47 au and a velocity of 17.19 km/s.
On 2020-03-02 21:41, '2020 QF2' approaches Earth at a distance of 0.45 au and a velocity of 8.79 km/s.
On 2020-03-03 00:49, '2019 TU' approaches Earth at a distance of 0.49 au and a velocity of 5.92 km/s.

# Show (the first) two close approaches in January 2030 of NEOs that are at most 50m in diameter and are marked not potentially hazardous.
$ python3 main.py query --start-date 2030-01-01 --end-date 2030-01-31 --max-diameter 0.05 --not-hazardous --limit 2
On 2030-01-07 20:59, '2010 GH7' approaches Earth at a distance of 0.46 au and a velocity of 18.84 km/s.
On 2030-01-13 07:29, '2010 AE30' approaches Earth at a distance of 0.06 au and a velocity of 14.00 km/s.

# Save, to a JSON file, all close approaches in the 2020s of NEOs at least 1km in diameter that pass between 0.01 au and 0.1 au away from Earth.
$ python3 main.py query --start-date 2020-01-01 --end-date 2029-12-31 --min-diameter 1 --min-distance 0.01 --max-distance 0.1 --outfile results.json
```

### `interactive`
This subcommand first loads the database and then starts a command loop so that you can repeatedly run `inspect` and `query` subcommands on the database without having to wait to reload the data each time you want to run a new command, which saves an extraordinary amount of time.

following is an example of program in an interactive mode.

```bash
$ python3 main.py interactive
Explore close approaches of near-Earth objects. Type `help` or `?` to list commands and `exit` to exit.

(neo) inspect --pdes 433
NEO 433 (Eros) has a diameter of 16.840 km and is not potentially hazardous.
(neo) help i
Shorthand for `inspect`.
(neo) i --name Halley
NEO 1P (Halley) has a diameter of 11.000 km and is not potentially hazardous.
(neo) query --date 2020-12-31 --limit 2
On 2020-12-31 05:48, '2010 PQ10' approaches Earth at a distance of 0.45 au and a velocity of 21.69 km/s.
On 2020-12-31 16:00, '2015 YA' approaches Earth at a distance of 0.17 au and a velocity of 5.65 km/s.
(neo) q --date 2021-3-14 --min-velocity 10
On 2021-03-14 06:17, '2019 DS1' approaches Earth at a distance of 0.39 au and a velocity of 20.17 km/s.
On 2021-03-14 20:19, '483656' approaches Earth at a distance of 0.06 au and a velocity of 12.09 km/s.
```

## Acknowledgments
This project is built as a requirement of Udacity's Intermediate Python Nanodegree <a href='https://confirm.udacity.com/TFTPFCWS' >click here</a> to view the certificate.
