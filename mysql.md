## SQL Y BD

*Estandar ISO de SQL, marca a donde hay que ir
*ISO/IEC 9075-1:2023

* Tutorial: W3Schools
--------------------------------------------------------------------------------------------
# Relacionales
Datos relacionados de forma profunda que queremos relacionarlo con otras entidades.

# No Relacionales
Datos que deseamos acceder muy rápido pero no queremos relacionarlo con otras entidades.
--------------------------------------------------------------------------------------------
# DBMS: Data Base Management System
BD Oracle
IBM DB2
SQLite (no sirve para proyectos muy grandes)
MariaDB
SQL Server (Microsoft)
PostgreSQL (la más popular hoy)
MySQL (2 partes, comunity y private, es de Oracle)
--------------------------------------------------------------------------------------------
# Teoria 1
Las tablas guardan atributos en las filas en modo de columnas
1 usuario es una fila y puede tener diferentes atributos (columnas)
--------------------------------------------------------------------------------------------
# Instalaciíon y conexión MYSQL

https://medium.com/@chrischuck35/how-to-create-a-mysql-instance-with-docker-compose-1598f3cc1bee
https://dev.to/darkmavis1980/how-to-persist-data-with-docker-compose-ik8

docker container exec -it my_mysql /bin/bash

docker inspect \
  -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' container_name_or_id
  
mysql -u test -p (test)

#  Comandos iniciales

SHOW DATABASES;
USE "XXXX";
SHOW TABLES;

# Cliente SQL
- DbVisualizer
- phpMyAdmin
- dbforge
- devart
- sqlProStudio
- TablePlus****
- MySQL Workbench (Herramienta propia de MySQL)****
