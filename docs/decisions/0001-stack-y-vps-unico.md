# 0001. Stack y VPS único

Fecha: 2026-10-28 · Estado: aceptada

## Contexto

Conectar Trabajo será un marketplace con perfiles públicos de emprendedores,
búsqueda y contacto. Los perfiles deben poder indexarse en buscadores, y el
equipo necesita una infraestructura inicial que sea sencilla de operar y
económica para el MVP.

El código de aplicación y la infraestructura necesitan ciclos de cambios,
dependencias y controles de acceso diferentes. Las imágenes de la API y la web
deben construirse fuera del servidor para evitar consumir recursos del VPS.

## Decisión

- La web se desarrolla con Next.js y TypeScript para permitir renderizado del
  lado del servidor y generación estática orientada a SEO.
- La API se desarrolla con FastAPI, Pydantic, SQLAlchemy y Alembic.
- PostgreSQL es la base de datos relacional del proyecto.
- El proyecto se divide en `connect-work-api`, `connect-work-web` y
  `connect-work-infra`.
- Cada repositorio de aplicación construye y publica su propia imagen.
- `connect-work-infra` referencia esas imágenes y las orquesta con Docker
  Compose.
- El MVP se despliega inicialmente en un único VPS.
- Caddy es el único punto de entrada público y administra el proxy inverso y
  los certificados HTTPS.
- PostgreSQL permanece en una red interna y no publica puertos a internet.

## Alternativas descartadas

- Un único repositorio para aplicación e infraestructura, porque mezclaría
  dependencias, permisos y ciclos de entrega distintos.
- Distribuir desde el inicio los componentes entre varios proveedores, porque
  aumentaría la complejidad operativa del MVP.
- Desplegar la web en Vercel y el resto en el VPS, para mantener inicialmente
  todos los servicios operativos bajo un mismo destino de despliegue.
- Kubernetes y microservicios, porque agregan complejidad sin una necesidad de
  escala demostrada.

## Consecuencias

- Cada repositorio puede validar y publicar sus cambios de forma independiente.
- El VPS no necesita compilar la API ni la web; solo descarga y ejecuta
  imágenes ya construidas.
- Docker Compose y Caddy reducen la complejidad operativa inicial.
- Los despliegues que afecten a más de un repositorio requieren coordinación y
  cambios compatibles hacia atrás.
- El VPS es un punto único de falla aceptado para el MVP.
- Staging y producción pueden competir por recursos si comparten servidor.
- El crecimiento inicial se resuelve aumentando el tamaño del VPS; si deja de
  ser suficiente, la base de datos puede migrarse a un servicio administrado.

El proveedor, la región y el tamaño del VPS, la ubicación de staging y la
estrategia de despliegue a producción permanecen pendientes.
