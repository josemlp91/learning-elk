# Curso Elastic Search y Kibana.

Para facilitar el uso de peticones con CURL defino las siguientes varaibles de entorno:

1. `$ELASTICURL`: URL de del servidor ElasticSearch preparado para atender peticiones REST.
2. `$ELASTICAUTH`: Credenciales básicas para poder hacer peticiones en el formado `usuario:pass`

``export ELASTICURL=https://elasticsearh_host``
``export ELASTICAUTH=user:password``

Una vez defininidas podemos probar que podemos hacer conexiones HTTP.


```sh
http GET $ELASTICURL -a $ELASTICAUTH
```

![](https://pix.toile-libre.org/upload/original/1534863877.png)


## Mapping y datos de prueba en nuestro cluster.

```sh
# Descargar mapping y dataset
wget http://media.sundog-soft.com/es6/shakes-mapping.json
wget http://media.sundog-soft.com/es6/shakespeare_6.0.json

# Crear mapping y inyectar datos usando una operación bulk
http PUT $ELASTICURL/shakespeare/ @shakes-mapping.json -a $ELASTICAUTH 
http POST $ELASTICURL/shakespeare//doc/_bulk shakespeare_6.0.json -a $ELASTICAUTH 

# Revisar que ya existen los datos.
http GET $ELASTICURL/shakespeare/_search -a $ELASTICAUTH
```

![](http://pix.toile-libre.org/upload/original/1534864392.png)


## Instalar Kibana y primera búsqueda.

![](http://pix.toile-libre.org/upload/original/1534865441.png)
