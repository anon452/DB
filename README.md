# AnonDB
AnonDB is the name we gave to our database for the double-blind submission.

## Main features
- A flexible and more expressive graph data mode.
- Efficient property paths solving.
- Worst case optimal join algorithm.

This project is in an early stage of development and is not production ready yet, as it may contain bugs. Also, there are some features we think are important for a graph database and are not supported yet. However we want them to be supported in the future:

- A database can't be modified after its created.
- Only well-designed patterns are supported when using the `OPTIONAL` operator.
- More datatypes for properties values, e.g: dates, points and lists.
- Filters only support basic operations. We would like to support pattern matching and functions.

___
# Table of Contents
- [Project build](#project-build)
- [Creating a database](#creating-a-database)
- [Querying a database](#querying-a-database)
  * [Run the server](#run-the-server)
  * [Execute a query](#execute-a-query)
___
# Project build

AnonDB should be able to be built in any x86-64 linux distribution.
If you work on windows, you can use Windows Subsystem for Linux (WSL).

1. Install prerequisites to compile:

    - Boost Library (versions 1.71, 1.74 and 1.76 have been tested to work propertly, versions 1.65 and 1.78 won't work)
    - Gcc version 8.1 or newer
    - Cmake version 3.10 or newer

    For distributions based on **Ubuntu 20.04** this can be done by running:
    - `sudo apt update`
    - `sudo apt install bzip2 git g++ cmake libboost-all-dev gdb`

     Other linux distributions may need to install the prerequisites differenlty. Some distributions might have repositories with too old versions and the project won't compile, in that case you'll need to manually install the appropiate versions.

2. Clone this repository and enter to the project folder:

3. Build the project:
    - `cmake -Bbuild/Release -DCMAKE_BUILD_TYPE=Release && cmake --build build/Release/`

# Creating a database
The command to create a new database looks like this:
- `build/Release/bin/create_db [path/to/import_file] [path/to/new_database_folder]`

For instance, if you want to create a database into the folder `tests/dbs/snb` using the example we provide in `tests/dbs/snb.txt` you need to run:
- `bzip2 -k -d tests/dbs/snb.txt.bz2` (to decompress the example file)
- `build/Release/bin/create_db tests/dbs/snb.txt tests/dbs/snb`

To delete a database just manually delete the created folder: `rm -r [path/to/database_folder]`.

# Querying a database
We implement the typical a client/server model, so in order to query a database, you need to have a server running and then send queries to it.
## Run the server
- `build/Release/bin/server [path/to/database_folder]`

## Execute a query
- `build/Release/bin/query < [path/to/query_file]`
