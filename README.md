# edifice

Edifice is an attempt to build a geospatial API for the entire city of Chicago. The goal of the project is to create a simple system for querying the status of a place within the boundaries of the city.

-- Query a building and get all the permits, violations, business licenses associated with it. Get its assessed value and all crimes that happened near it

-- Query a street segment and get its current average traffic speed or all the requests to the 311 system associated with it

-- Query a park and see upcoming special event permits or all the public works of art there 

-- Query a community area and see aggregate health outcome data, population, and demographics

Currently, the vast majority of this data is taken from the [City of Chicago open data portal](https://data.cityofchicago.org/). There are also datasets generated from Cook County web site and sets from the U.S. Census and the American Community Survey. [Google Doc of data sources we are using](https://docs.google.com/spreadsheet/ccc?key=0AtbqcVh3dkAqdGdlcWd5MzRYcGJkS1RoQTM3Qzd4dUE)

But the larger vision for this project is to be an authoritative geospatial database of anything in the city that has some form of a location-- address, lat/long, shapefile, etc.

There are a number of other useful aspects of this project, including address matching, scraping of non data-portal datasets, and a meta description aggregator that helps researchers and civic-minded people to think about what the information in this huge database means. We welcome ideas on how such a tool could be used to make lives better in Chicago.

The first public-facing manifestation of this project is [Edifice Maps](http://edifice.opencityapps.org/), ("Maps of Chicago's built environment"). The informal team working on edifice meets weekly at the [Open Gov Hack Night](http://opengovhacknight.eventbrite.com/). Join us!

## Requirements

* PostgreSQL (9.0.x or later; 9.1.x+ preferred)
* PostGIS (2.0.x or later)
* Python (2.7.x or later)
* wget
* psycopg2

## Using setup_edifice.py

setup_edifice.py is used to recreate the edifice database on a system
with a PostgreSQL database installed (with PostGIS 2.0.x+ support).

Drop and recreate from scratch a `base_postgis` template database, using the 'postgres' admin user.

<pre>
python setup_edifice.py --create_template
</pre>

Drop and recreate from scratch an `edifice` database struture, using the 'edifice' user.
<pre>
python setup_edifice.py --create
</pre>

Download (~165mb), unzip, and import City of Chicago data into the `edifice` database. [NOTE: WORK IN PROGRESS]
<pre>
python setup_edifice.py --data
</pre>

Optional flags:

* `--bindir [DIRNAME]`: specify the location of PostgreSQL binaries such as pg_config, psql, etc.
* `--user [USERNAME]`: use a username other than 'edifice' as the owner of the main database.
* `--database [DBNAME]`: use a name other than 'edifice' for the main database.
* `--delete_downloads`: delete downloaded zip and csv files after import
* `--help`: provide usage info

## Data Sources

[Google Doc of data sources we are using](https://docs.google.com/spreadsheet/ccc?key=0AtbqcVh3dkAqdGdlcWd5MzRYcGJkS1RoQTM3Qzd4dUE)

## QGIS and TileMill

Once you are done setting up your Edifice database, you can use the following tools (including psql) to explore the datasets.

[QGIS](http://qgis.org) is a free, open-source [GIS](http://en.wikipedia.org/wiki/Geographic_information_system) application that can connect directly to a PostGIS database and display and analyze geographic data.

[TileMill](http://mapbox.com/tilemill) is a map-design studio that can also connect directly to a PostGIS datastore and create interactive web maps using [OpenStreetMap](http://openstreetmap.org) as the base layer.
