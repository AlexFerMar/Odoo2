# odoo

![odoo](https://upload.wikimedia.org/wikipedia/commons/a/a7/Odoo_Official_Logo.png)

## 1. Introduccion 


[**Odoo**](https://es.wikipedia.org/wiki/Odoo) es un software de [ERP](https://es.wikipedia.org/wiki/Planificaci%C3%B3n_de_recursos_empresariales) integrado que incluye CRM, sitio web y comercio electrónico, facturación, contabilidad, fabricación, gestión de almacenes y proyectos, e inventario entre otros[^1]. 

El módulo del servidor está escrito en el lenguaje [**Python**](https://es.wikipedia.org/wiki/Python) y emplea  [**PostgreSQL**](https://es.wikipedia.org/wiki/PostgreSQL) como sistema gestor de base de datos. 


## 2.Instalando odoo 


Para instalar odoo emplearemos docker compose. Esto nos permitira crear un entorno ideal para hacer pruebas gracias a las facilidades que ofrecen los contenedores de docker. 

Creamos una carpeta vacía para almacenar nuestro ***docker-compose.yml***, que es lo que emplearemos para construir nuestro wordpress. El contenido del archivo es el siguiente:

```MiniYAML
version: '3.1'
services:
  mydb:
    image: postgres:13
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
    ports:
      - "5430:5432"
    volumes:
     - dam22_odoo:/var/lib/postgresql/data
  
  odoo:
    image: odoo:14.0
    container_name: dam22_odooklk
    ports:
      - "8069:8069"
    depends_on:
      - mydb
volumes:
  dam22_odoo:
```

Lo siguiente es instalar docker compose, lo cual hacemos mediante el siguiente comando:

```bash
$sudo apt-get install docker-compose-plugin
```

Una vez instalado el docker compose, lanzamos el siguiente comando ***en el mismo directorio donde está nuestro docker-compose.yml***:

```bash
$docker compose up -d
```

Listo, con esto nuestros contenedores están creados y listos para su utilización. 

## 3. Desgosando el Docker-Compose


- Primero, especificamos la version de Docker-Compose con la siguiente línea:

```MiniYAML
version: '3.1'
```


```MiniYAML
services:
```

```MiniYAML
mydb:
    image: postgres:13
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_PASSWORD=odoo
      - POSTGRES_USER=odoo
    ports:
      - "5430:5432"
    volumes:
     - dam22_odoo:/var/lib/postgresql/data
```



```MiniYAML
odoo:
    image: odoo:14.0
    container_name: dam22_odooklk
    ports:
      - "8069:8069"
    depends_on:
      - mydb
```


```MiniYAML
volumes:
  dam22_odoo:
```


[^1]: Descripcion sacada de [Wikipedia](https://es.wikipedia.org/wiki/Odoo).