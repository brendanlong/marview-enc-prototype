See https://www.notion.so/brendanlong/Web-App-8c1597ecffab456184b96a6c53006f4c

## GDAL

Install GDAL.

On OSX:

```bash
brew install gdal
```

This will give you access to the `ogr2ogr` command:

https://gdal.org/programs/ogr2ogr.htmls

Note that for S57 format you will need to set this environment variable:

```
export 57_CSV=/usr/local/Cellar/gdal/3.7.1_2/share/gdal
```

Example GDAL command to load features from NOAA S57 data:

```bash
S57_CSV=/usr/local/Cellar/gdal/3.7.1_2/share/gdal ogr2ogr -f PostgreSQL postgresql://marview:marview@localhost:5431/marview ~/Downloads/ENC_ROOT/US4AL11M/US4AL11M.000 -skipfailures -nlt PROMOTE_TO_MULTI -lco OVERWRITE=YES -lco PRECISION=YES
```