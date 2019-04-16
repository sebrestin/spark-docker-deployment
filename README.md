# spark-docker-deployment

The repository contains a pySpark docker deployment which can be used for fast development.

### Docker image
The docker image depends on 4 important elements:
1. app directory for code input
2. data directory for data input
3. spark-events for logs
4. spark-defaults.conf

The docker-compose.yml file has 2 services which both depend on the spark image:

1. **pyspark service** exports port :4040 in order to visualize the job progress.
    It uses 3 volumes:
    1. app
    2. data
    3. spark-events

2. **history service** exports port :18080 in order to visualize finished jobs.
    It shares spark-events volume with the pyspark service.

### Usage

Running any Spark jobs require 4 steps:
1. copying the spark app to the app directory
2. copying the necessary data to the data directory
3. adjust spark options inside spark-defaults.config
4. running the spark app

    **Command line:**
    ```
    docker-compose up
    docker-compose run --service-ports pyspark python /app/spark_app.py
    ```
    
    **PyCharm Professional:**
    
    The docker-compose services can be linked with PyCharm Professional in order to run Spark apps from the IDE:
    
    1. starting the services
         ```
        docker-compose up
        ```
    2. setting a remote python interpreter using the pyspark service from the docker-compose (https://www.jetbrains.com/help/pycharm/using-docker-compose-as-a-remote-interpreter.html)
    3. running app/spark_app.py from the PyCharm project.
