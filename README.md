# Project-3-Topics-in-Telematics

Ingesta de datos 
#!/bin/bash
# Descargar el archivo
wget -O data.csv "https://www.datos.gov.co/api/views/gt2j-8ykr/rows.csv?accessType=DOWNLOAD"
# Subir el archivo a S3
aws s3 cp data.csv s3://covid-data-bucket/raw/
