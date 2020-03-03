# HadoopGis-Revision
  
## Installation Notes:

Detailed installation refers to http://bmidb.cs.stonybrook.edu/hadoopgis/installation.
 
 - Please git clone this repositry instead of the original one, this version added some dependencies, revisied some source code and have re-compiled some components of haddopgis. (To note that, it has only been tested in Ubuntu environments).

 - Besides "HADOOP_INSTALL", "HADOOP_HDFS_HOME", "YARN_HOME" and "HADOOP_PREFIX", please also add "**HADOOPGIS_BIN_PATH**" to your environment variables and point it to the correct paths (for example, in your *~/.bashrc* file, add "export HADOOPGIS_BIN_PATH=/root/hadoopgis/build/bin").

  - Please configure */etc/ld.so.conf* to add "/root/hadoopgis/installer/built/lib" (or your corresponding path), than execute "ldconfig" to make your change effective.

 - Remember to rename the hadoop-streaming-x.x.x.jar(*XXX* represents version number) to hadoop-streaming.jar (the jar file is normally in hadoop/share/hadoop/tools/lib/ folder)

## Example Notes:

Please refer to http://bmidb.cs.stonybrook.edu/hadoopgis/examples to find related examples and datasets.

- The **partition** query does not recognize parameter **bsp**, it should be **bsp_2d**. In addition, you cannot use `--s`, you have to use either `-s`or `--samplingrate`. For example, the commond in original website such as:
```
./build/bin/queryprocessor_2d --querytype partition --geom1 5 \
    --input1 YOUR_HDFS_PATH/tweets/rawdata/tweets.filtered.tsv \
    --outputpath YOUR_HDFS_PATH/tweetspartitioned --partitioner bsp --s 0.1 --numreducers 10
 ```
should be changed into:
```
./build/bin/queryprocessor_2d --querytype partition --geom1 5 \
    --input1 YOUR_HDFS_PATH/tweets/rawdata/tweets.filtered.tsv \
    --outputpath YOUR_HDFS_PATH/tweetspartitioned --partitioner bsp_2d -s 0.1 --numreducers 10
```

- The **containment** query reguires a parameter of **containrange**, according to http://bmidb.cs.stonybrook.edu/hadoopgis/features, this value should be a comma separated list of `min_x min_y max_x max_y`, however, this should be space seperated parameter enclosed in quote. In addition, this query type require a parameter of **-p** (--predicate), which is missing in their website (Be aware, in http://bmidb.cs.stonybrook.edu/hadoopgis/features, the explaination of `-p` and `-t` are the contrary of each other). For example, the commond in original website such as:
```
./build/bin/queryprocessor_2d --querytype containment --containrange -124.7,24.5,67.0,49.5 \ 
    --input1=YOUR_HDFS_PATH/tweetspartitioned --outputpath=YOUR_HDFS_PATH/containmentout
```
should be changed into:
```
./build/bin/queryprocessor_2d --querytype containment --containrange "-124.7 24.5 67.0 49.5" --geom1 2 --input1 YOUR_HDFS_PATH/tweetspartitioned --outputpath YOUR_HDFS_PATH/containmentout -p st_within
```
