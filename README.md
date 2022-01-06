# docker-spark-cluster
Build your own Hadoop cluster setup in Docker.      
A multinode Hadoop installation where each node of the network runs in its own separated Docker container.   
The installation takes care of the Hadoop configuration, providing:
1) a debian image with java (javabase image)
2) three fully configured Spark nodes running on Hadoop (hadoopbase image):
    * nodemaster (master node)
    * node2      (slave)
    * node3      (slave)

## Installation
1) Clone this repository
2) cd javabase
3) ./build.sh    # This builds the base java+scala debian container from openjdk9
4) cd ../hadoop
5) ./build.sh    # This builds sparkbase image
6) run ./cluster.sh deploy
7) The script will finish displaying the Hadoop and Spark admin URLs:
    * Hadoop info @ nodemaster: http://172.18.1.1:8088/cluster
    * DFS Health @ nodemaster : http://172.18.1.1:9870/dfshealth.html

## Options
```bash
cluster.sh stop   # Stop the cluster
cluster.sh start  # Start the cluster
cluster.sh info   # Shows handy URLs of running cluster

# Warning! This will remove everything from HDFS
cluster.sh deploy # Format the cluster and deploy images again
```
