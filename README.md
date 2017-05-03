# LiveFreeOrDICOM
DICOM to SQL DVH Database

This code is intended for Radiation Oncology departments to build a SQL database of DVH's and various planning parameters from DICOM files (Plan, Structure, Dose).
This is a work in progress.

## Code organization
#### *DICOM_to_Python*  
This code contains functions that read dicom files and generate python objects containing the data required for input into the
SQL database.  There is no explicit user input.  All data is pulled from DICOM files (except for Rx's and Tx site from Pinnacle).

#### *DVH_SQL*  
This code handles all communication with SQL using MySQL Connector.  No DICOM files are used in this code and require the python objects
generated by DICOM_to_Python functions.

#### *DICOM_to_SQL*  
This has the simple objective of writing to SQL Database with only a starting path folder containing DICOM files (will search all sub-folders as well).

#### *Analysis_Tools*  
These functions are designed to process data retrieved from the SQL database and convert into python objects.

#### *ROI_Name_Manager*  
From independently created .roi files, this class generates a map of ROI names and provides functions to query
and edit this map.  Each ROI points to an institutional ROI, physician ROI, and a physician.  

#### *SQL_to_Python*  
This code uses *DVH_SQL* to query the SQL DB. Input requires a table name, the resulting object contains properties 
corresponding to each of the column in the queried table.


## To Do List
- [ ] Validate dicompyler-core DVH calculations

- [ ] Write DICOM pre-import validation function

- [ ] Add thorough comments throughout all code

- [x] EUD calculations: Incorporate look-up tables of a-values
    - [ ] Validate calculations

- [ ] Incorporate BED, TCP, NTCP calculations

- [X] Validate functions in *Analysis_Tools*

- [ ] Develop for SQL other than MySQL

- [X] Update stats DVHs for other DVH scales

- [ ] Track wedge info on 3D beams

- [ ] Look into filtering by date range

- [ ] Dose grid resolution is undefined

- [ ] Post-import file management

- [ ] Write an update ROI category function in *DVH_SQL*

- [ ] Clean and add comments to main.py code


## Dependencies
* [Python](https://www.python.org) 2.7 tested
* [MySQL](https://dev.mysql.com/downloads/mysql/) and [MySQL Connector](https://dev.mysql.com/downloads/connector/python/)
* [numpy](https://pypi.python.org/pypi/numpy) 1.12.1 tested
* [pydicom](https://github.com/darcymason/pydicom) 0.9.9
* [dicompyler-core](https://pypi.python.org/pypi/dicompyler-core) 0.5.2
    * requirements per [developer](https://github.com/bastula)
        * [numpy](http://www.numpy.org/) 1.2 or higher
        * [pydicom](http://code.google.com/p/pydicom/) 0.9.9 or higher
            * pydicom 1.0 is preferred and can be installed via pip using: pip install https://github.com/darcymason/pydicom/archive/master.zip
        * [matplotlib](http://matplotlib.sourceforge.net/) 1.3.0 or higher (for DVH calculation)
        * [six](https://pythonhosted.org/six/) 1.5 or higher
* [Pretty Table](https://pypi.python.org/pypi/PrettyTable/) 0.7.2 (optional, for command line only)
* [Bokeh](http://bokeh.pydata.org/en/latest/index.html) 0.12.5
    * requirements per [developer](http://bokeh.pydata.org/en/latest/docs/installation.html)
        * [NumPy](http://www.numpy.org/)
        * [Jinja2](http://jinja.pocoo.org/)
        * [Six](https://pythonhosted.org/six/)
        * [Requests](http://docs.python-requests.org/en/master/user/install/)
        * [Tornado](http://www.tornadoweb.org/en/stable/) >= 4.0, <=4.4.2
        * [PyYaml](https://pypi.python.org/pypi/pyaml)
        * [DateUtil](https://pypi.python.org/pypi/python-dateutil)
