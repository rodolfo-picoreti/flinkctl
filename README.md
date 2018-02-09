# Flinkctl
Command line utility to interact with Flink job manager using the monitoring REST API. 

# Why?
Communicating with the job manager when deploying Flink with Kubernetes can be a pain 
due to some problems with Akka ([more](https://youtu.be/w721NI-mtAA)).

# Dependencies
- python2
- arrow 
- fire 
- requests

```shell
sudo pip install arrow fire requests
```

# Usage

## Configuration File
The tool will try to read your current path and *~/.config/flink/* for a file named **config.json** that 
should contain the uri to connect to the monitoring rest api.
```json
{
  "uri": "http://localhost:8081"
}
```

## List uploaded jars
```shell
$ flinkctl jars ls 
id                                       name                                     uploaded
2d193028-eb06-441a-ade1-6839a1d7f002     wordcount-1.0-SNAPSHOT-jar-with-depend   just now
86e6086c-5f8d-4784-9dd5-07570a4b1d20     wordcount-1.0-SNAPSHOT-jar-with-depend   an hour ago
```

## Remove a jar
```shell
$ flinkctl jars rm 2d 
```

## Upload a jar
```shell
$ flinkctl jars upload ~/IdeaProjects/wordcount/target/wordcount-1.0-SNAPSHOT-jar-with-dependencies.jar 
```

## Run a jar
```shell
$ flinkctl jars run 86e #--entry MainKt --args ...
```

## List jobs
```shell
$ flinkctl jobs ls 
id                                       name                 state         started
d4648be93718eb094aa75759913e1715         Word Counter         RUNNING       3 hours ago
4ee09d87ee8de6baf30aa3e096904a0b         Word Counter         CANCELED      4 hours ago
f184b029b2ae5715a7cb6c56fd92f276         Word Counter         CANCELED      2 hours ago
```

## Cancel a job
```shell
$ flinkctl jobs stop 4ee
```
