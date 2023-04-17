# Visualize your (Google) location history 
This project built upon gboeing's lovely [location-history](https://github.com/gboeing/data-visualization/tree/main/location-history) project from a few years ago.

The purpose is to compute border-crossings, as needed for annoying beurocratic things like taxes and visas. 

E.g. for my UK passport application I needed to report all my comings and goings from UK for the past 5 years.  I decided spending 10 hours messing with this was much more fun than spending 1 hour working it out by hand from emails and photos :) 

## Instructions
Click [here](https://accounts.google.com/ServiceLogin?service=backup) to download your Google location history as a JSON file called `Records.json`

It should look something like this:
```json
{
  "locations": [{
    "latitudeE7": 337625316,
    "longitudeE7": -843593197,
    "accuracy": 40,
    "source": "sensor_other",
    "timestamp": "2011-04-23T18:22:13.086Z"
  },
  ...
```

Run the relevant cells.  It should run top-to-bottom if you have all dependencies installed.

This was developed and tested on a 2021 M1 MBP with 32 GB of ram.

The main hurdle I ran into was clustering the GPS data. The example I started from used DBSCAN which always OOMed and killed my kernel.  I found some threads about fixing it, but decided to go with [HDBSCAN](https://hdbscan.readthedocs.io/en/latest/how_hdbscan_works.html) which is a hierarchical extension of DBSCAN that I hoped was more scalable.

In my experience it still choked after about 900k datapoints, but YMMV.