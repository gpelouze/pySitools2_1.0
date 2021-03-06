![](http://github.com/SITools2/core-v2/raw/dev/workspace/client-public/res/images/logo_01_petiteTaille.png)
# pySitools2_1.0

## Description

pySitools2_1.0 is a generic python Sitools2V1.0 client

pySitools2 tool has been designed by the IAS MEDOC team to perform all operations available within Sitools2.

The code defines several classes of Sitools2: Field, Query, Dataset and Project. 

It also contains specialized versions of the client, allowing the end user to easily perform queries on selected data sets, namely SDO/AIA, SDO/HMI, and GAIA-DEM at MEDOC, and download the corresponding data.

## Building pySitools2_1.0

### Getting the sources

    git clone https://github.com/MedocIAS/pySitools2_1.0 pySitools2_1.0

The retrieved module structure is the following (not all files are shown):

    LICENCE
    README.md
    setup.py
    -- sitools2
        -- clients
            README_GAIA.txt
            README_MEDIA.txt
            gaia_client_medoc.py
            sdo_client_medoc.py
        -- core
            pySitools2.py
    -- examples
        example_gaia.py
        example_idoc-medoc_aia.py
        example_idoc-medoc_hmi.py
    -- tests
        testGaia.py
        testIdocMedocAiaSearch.py
        testIdocMedocHmiSearch.py

### Testing the module

    cd pySitools2_1.0
    python setup.py test -q

## Installing the module

### Installing the module for the system

    cd pySitools2_1.0
    sudo pip## install .

    where ## is your pip/python version.

## Features

- Make a search providing a date range, a wavelength, a cadence.
- Filter the results with specific keyword values (e.g. filter on quality, cdelt...)
- Download the results of your search.

## Examples of application

Full examples are provided in the `examples` directory.

### sdo_client_medoc.py

This python module will allow you to :

- Make a request using the media_search() function.

        $ from sitools2.clients.sdo_client_medoc import media_search, media_get
        from datetime import datetime, timedelta

        d1 = datetime(2012, 11, 21, 0, 0, 0)
        d2 = d1 + timedelta(days=1)
        sdo_data_list = media_search(dates=[d1, d2], waves=['335'], cadence=['6 h'])

- Simply download the result of your previous search() calling the media_get()function.

        media_get (media_data_list=sdo_data_list, target_dir='results')

<!-- To be updated to work with current version -->
<!--- Have additional metadata information about each previous answer using the media_metadata_search() method.

    $ for item in sdo_data_list:
        my_meta_search = item.media_metadata_search ( KEYWORDS=['quality','cdelt1','cdelt2'] )
        print my_meta_search

- Filter on a specific keyword before download data using the get_file() method.

    $ for item in sdo_data_list:
        my_meta_search = item.media_metadata_search ( KEYWORDS=['date__obs','quality','cdelt1','crval1'] )
        if (my_meta_search['quality'] == 0) :
            item.get_file( TARGET_DIR='results/' )-->

For more information see the `README_MEDIA.txt` file.

### gaia_client_medoc.py

This python module will allow you to :

- Make a request using the gaia_search() function.
        
        $ from sitools2.clients.gaia_client_medoc import gaia_search, gaia_get
        from datetime import datetime, timedelta
        d1 = datetime(2012, 11, 21, 0, 0, 0)
        d2 = d1 + timedelta(days=1)
        gaia_data_list = gaia_search(dates=[d1, d2])

- Simply download the result of your previous media_search() calling the media_get() function.

        gaia_get(gaia_list=gaia_data_list, target_dir='results')

- Specify the type of data you want to retrieve, it should be a list containg elements among: 'temp', 'em', 'width', 'chi2':

        gaia_get (gaia_list=gaia_data_list, target_dir="results", type=['temp', 'em'])

For more information see the `README_GAIA.txt` file.

## Update the module 

    cd pySitools2_1.0
    git pull origin master 
    sudo -H pip## install . --upgrade

where ## is your pip/python version.

## Remove the module 

### For the system

    cd pySitools2_1.0
    sudo pip## uninstall pySitools2_1.0

where ## is your pip/python version.
