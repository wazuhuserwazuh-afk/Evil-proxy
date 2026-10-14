# ============================================================================
#  Exploit: HTTP Request Smuggling (CL.TE)
#
#  Creado exclusivamente para la máquina "Proxy" de WhoamiLabs.
#  Si alguien necesita reutilizarlo para otro entorno, puede adaptarlo
#  libremente a sus necesidades (IP, puerto, rutas, payload, etc.).
#
#  Uso exclusivo en entornos controlados y con autorización.
# ============================================================================




# Evil-proxy from Whoami-labs
Abre una conexión al servidor, envía un POST con una petición oculta dentro del body (smuggling CL.TE), manda luego un GET / por la misma conexión como disparador, y lee la respuesta para extraer las claves internas.

# HTTP Request Smuggling (CL.TE) - PoC

Exploit en Python para una vulnerabilidad **HTTP Request Smuggling CL.TE** contra un servidor con HAProxy como frontend y un backend que solo respeta `Content-Length`.

## Cómo funciona

HAProxy parsea el body como `chunked` y borra la cabecera `Transfer-Encoding` antes de reenviar al backend. El backend, que solo usa `Content-Length`, consume solo los primeros 4 bytes del body y guarda el resto en su buffer, donde queda escondida una segunda petición a `/api/internal/backup_keys`. Un `GET /` enviado después por la misma conexión dispara su ejecución.

## Requisitos

- Python 3
- Acceso de red al servidor objetivo

## Uso

```bash
python3 exploit.py
