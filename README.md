# HadoopGis-Revision
  
 Detailed installation refers to http://bmidb.cs.stonybrook.edu/hadoopgis/installation.
 
 - Please git clone this repositry instead of the original one, this version added some dependencies, revisied some source code and have re-compiled some components of haddopgis. (To note that, it has only been tested in Ubuntu environments).

 - Besides "HADOOP_INSTALL", "HADOOP_HDFS_HOME", "YARN_HOME" and "HADOOP_PREFIX", please also add "**HADOOPGIS_BIN_PATH**" to your environment variables and point it to the correct paths (for example, in your *~/.bashrc* file, add "export HADOOPGIS_BIN_PATH=/root/hadoopgis/build/bin").

  - Please configure */etc/ld.so.conf* to add "/root/hadoopgis/installer/built/lib" (or your corresponding path), than execute "ldconfig" to make your change effective.

 - Remember to rename the hadoop-streaming-x.x.x.jar(*XXX* represents version number) to hadoop-streaming.jar (the jar file is normally in hadoop/share/hadoop/tools/lib/ folder)
