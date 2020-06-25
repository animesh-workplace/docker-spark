# Docker Spark

This creates a docker of Apache Spark v2.3.4 with the base image of Apache Hadoop 2.8.5 and openjdk8 can be found in this [repository](https://github.com/animesh-workplace/docker-hadoop)

Use the following Docker compose file to create master and worker nodes:

```bash
version: "2"

services:
  master:
    image: animeshworkplace/docker-spark
    command: start-spark master
    hostname: master
    ports:
      - "6066:6066"
      - "7070:7070"
      - "8080:8080"
      - "50070:50070"
  worker:
    image: animeshworkplace/docker-spark
    command: start-spark worker master
    environment:
      SPARK_WORKER_CORES: 1
      SPARK_WORKER_MEMORY: 2g
    links:
      - master
```

- Create a file and copy the above code
- Name the file ```docker-compose.yaml```
- Run the command ```docker-compose up```