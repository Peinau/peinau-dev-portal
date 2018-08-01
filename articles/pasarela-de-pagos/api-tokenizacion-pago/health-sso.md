# Health Check Obtener Token de Acceso

Puedes consultar el estado del servicio de la siguiente forma:

```
curl -X GET \
  https://api.sandbox.connect.fif.tech/sso/health
  
```

Cuando el status del servicio es **UP** recibirás una respuesta similar a:

```
{
    "status": "UP",
    "up_time": "244:38:45",
    "info": {
        "profile": "PROD",
        "name": "api-qpay-single-sign-on",
        "version": "1.0.30",
        "routePrefix": "/sso",
        "logging": {
            "level": "info"
        }
    }
}
```
Http status code: **200**
