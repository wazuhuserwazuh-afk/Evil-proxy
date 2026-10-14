# Evil-proxy from Whoami-labs
Abre una conexión al servidor, envía un POST con una petición oculta dentro del body (smuggling CL.TE), manda luego un GET / por la misma conexión como disparador, y lee la respuesta para extraer las claves internas.
