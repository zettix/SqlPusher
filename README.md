Tankette Utility : SqlPusher
==============================

(C) Sean Brennan, 2018
------------------------------

### Description

This program is used to collect output many files from an input directories,
and output a mysql database with 3 tables:
1. textures
2. meshes
3. manifest

The files are either PNGs or 16-bit unsigned int data files.

Example input files are generated from the imagecooker utility using
 NASA's Mars DEM and Viking color TIFF images, with
resolutions of 46080 x 23040 and 92160 x 46080, and sizes of 2 gigs and
12 gigs respectively.

The pusher is not very intelligent and expects images and data here:
For tiles numbering w across and h high, images are in:
+ ./textures/i_y/tex_y_x.png

and mesh data in
+ ./meshes/d_y/data_y_x.dat

The manifest table is generated from the data file directory contents.


### Usage

The following directories/links to directories should be prepared ahead of time.
1. ./textures
2. ./meshes

They should be readable and contain the files.  Then decide the following:
1. The name of the database.

Then create the database with the following two  commands:
+ _textures_ java -classpath "./sqlite/sqlite-jdbc-3.19.3.jar:." terrain.SqlPusher -f $db -d textures -t textures

+ _meshes_ java -classpath "./sqlite/sqlite-jdbc-3.19.3.jar:." terrain.SqlPusher -f $db -d meshes -t terrain

./imagecooker -f input.png -x xres -y yres -w width -h height -t
echo "DB Tex"
echo "DB Ter"
java -classpath "../sqlite/sqlite-jdbc-3.19.3.jar:." terrain.SqlPusher -f ${db} -d meshes -t terrain >> $log 


Load the file using tankette's TerrainConstants.java file.
