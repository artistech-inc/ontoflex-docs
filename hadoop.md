# OntoFlex Hadoop

1. Install [Hadoop](https://hadoop.apache.org/)
2. [Setup Single Cluster](https://hadoop.apache.org/docs/r2.8.0/hadoop-project-dist/hadoop-common/SingleCluster.html)

3. Setup files system and input directory
```sh
bin/hdfs namenode -format
sbin/start-dfs.sh
bin/hdfs dfs -mkdir /user
bin/hdfs dfs -mkdir /user/<username>
bin/hdfs dfs -mkdir input
```
4. Copy input files:  
```sh
bin/hdfs dfs -put /local/input/files/* input
```
5. Source ClassPath:  
```sh
cd /to/location/of/generateClassPath.sh
source ./generateClassPath.sh
```

# Known Issues

## BeanUtils for type conversion (PropertiesInitializer)
The BeanUtils lookup doesn't take to/from Class parameters, so check (once) and then use the best method available.
```java
boolean lookup = true;
Class<?> c = BeanUtilsBean.getInstance().getConvertUtils().getClass();
try {
		c.getMethod("lookup", Class.class, Class.class);
} catch (NoSuchMethodException | SecurityException ex) {
		lookup = false;
}
TWO_PARAM_LOOKUP = lookup;
```
This is/was an issue for any class that derives from `PropertiesInitializer`.

## Deserializing MatchSet from XML
If deserializing using UTF-8; the above will throw an exception about 0x19.  But the string content is there.  Initialize the byte data from US-ASCII and it works.

```java
String str = new String(value.getBytes(), "US-ASCII");
```

Also, the `WholeFileInputFormat` class is needed as the input to OntoFlex is the file contents, not one-line-per-file.

# Setting CLASSPATH
I'm not sure how to handle setting the CLASSPATH for all of the dependencies in Hadoop.  It looks like there is a way to set add to the classpath if you put the JAR in the dfs.  But this wasn't letting me now about the existance of necessary classes (ClassNotFoundException).
```java
//Path rootDir = new Path("/users/matta/lib);
if (args.length > 2) {
    Path rootDir = new Path(args[2]);
    FileSystem fs = rootDir.getFileSystem(conf);
    FileStatus[] status = fs.listStatus(rootDir);
    for (FileStatus file : status) {
        job.addFileToClassPath(file.getPath());
    }
}
```
We can override the `$HADOOP_CLASSPATH` using the `generateClassPath.sh` script, but I'm not sure how that works when using a distributed cluster environment.
