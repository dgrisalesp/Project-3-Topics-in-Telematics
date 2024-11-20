# Project-3-Topics-in-Telematics

Ingesta de datos 
#!/bin/bash
# Descargar el archivo
wget -O data.csv "https://www.datos.gov.co/api/views/gt2j-8ykr/rows.csv?accessType=DOWNLOAD"
# Subir el archivo a S3
aws s3 cp data.csv s3://covid-data-bucket/raw/


#spark-etl.py#
~~~
import sys
from datetime import datetime
from pyspark.sql import SparkSession
from pyspark.sql.functions import *

if __name__ == "__main__":

    print(len(sys.argv))
    if len(sys.argv) != 3:
        print("Usage: spark-etl [raw-folder] [trusted-folder]")
        sys.exit(0)

    spark = SparkSession\
        .builder\
        .appName("SparkETL")\
        .getOrCreate()

    myTaxi = spark.read.option("inferSchema", "true").option("header", "true").csv(sys.argv[1])

    df = myTaxi.withColumn("current_date", lit(datetime.now()))

    df.printSchema() 
    df.columns
    len(df.columns)
    df.count()
    print((df.count(),len(df.columns)))
    df.printSchema()
    df.show(15)
    df.select('Edad','Nombre municipio').show(10)




    updatedNYTaxi.write.parquet(sys.argv[2])
~~~
