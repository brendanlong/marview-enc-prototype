See https://www.notion.so/brendanlong/Web-App-8c1597ecffab456184b96a6c53006f4c

## Setup

Install GDAL, Docker and docker-compose.

On OSX:

```bash
brew cask install docker # or install this https://docs.docker.com/desktop/install/mac-install/
brew install docker-compose gdal
```

Note that for S57 format to work in GDAL you will need to set this environment variable on OSX (assuming you get the same GDAL version I did):

```
export 57_CSV=/usr/local/Cellar/gdal/3.7.1_2/share/gdal
```

Download and extract the NOAA ENC data to your Downloads folder:

<https://charts.noaa.gov/ENCs/All_ENCs.zip>

Start the database and server in the background:

```bash
docker-compose up -d
```

Run GDAL to load features from NOAA S57 data:

```bash
S57_CSV=/usr/local/Cellar/gdal/3.7.1_2/share/gdal ogr2ogr -f PostgreSQL postgresql://marview:marview@localhost:5431/marview ~/Downloads/ENC_ROOT/US4AL11M/US4AL11M.000 -skipfailures -nlt PROMOTE_TO_MULTI -lco OVERWRITE=YES -lco PRECISION=YES
```

Then open `index.html` in a browser and zoom in on the Southeast U.S. near the border of Louisiana and Mississippi (this is the only data loaded because we only loaded the `US4AL11M` data set which covers this area).