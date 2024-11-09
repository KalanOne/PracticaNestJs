# Prerrequisitos para la práctica de NestJS
Antes de comenzar con la práctica de NestJS, asegúrate de tener los siguientes componentes instalados y configurados.

1. Node.js y npm
NestJS requiere Node.js y npm (el gestor de paquetes de Node.js). Puedes descargar e instalar la versión LTS más reciente desde la página oficial de [Node.js](https://nodejs.org/). Verifica la instalación ejecutando los siguientes comandos en tu terminal:

```bash
node -v
npm -v
```
2. NestJS CLI
Para facilitar la creación y administración de proyectos NestJS, es recomendable instalar la CLI de NestJS de forma global:

```bash
npm install -g @nestjs/cli
```
Una vez instalada, puedes verificarla con:

```bash
nest --version
```

3. Base de Datos
Usaremos PostgreSQL como base de datos en esta práctica. Hay dos maneras de configurarlo:

- Opción 1: Usar PostgreSQL con Docker
Si prefieres no instalar PostgreSQL directamente en tu sistema, puedes utilizar Docker para ejecutar una instancia de PostgreSQL. Para esto, necesitas tener Docker instalado.

Configuración de Docker para PostgreSQL
Crea un archivo docker-compose.yaml con la siguiente configuración:

```yaml
services:
  db:
    image: postgres:latest
    restart: always
    ports:
      - "${DB_PORT}:${DB_PORT}"
    environment:
      POSTGRES_PASSWORD: ${DB_PASSWORD}
      POSTGRES_DB: ${DB_NAME}
      PGTZ: 'America/Mexico_City'
    container_name: ${CONTAINER_NAME}
    command: -p ${DB_PORT}
```
Además, puedes utilizar el siguiente archivo Dockerfile para personalizar la configuración de PostgreSQL:

```Dockerfile
FROM postgres:latest

# Configura la zona horaria
ENV TZ=America/Mexico_City

# Crea el directorio para los respaldos
RUN mkdir -p /var/lib/postgresql/backup
```

Variables de entorno
Para esta configuración, crea un archivo .env con las siguientes variables de entorno:

```env
DB_PASSWORD=mypassword
DB_NAME=moviesdb
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
CONTAINER_NAME=practica
```
Una vez configurado, ejecuta el contenedor:

```bash
docker-compose up -d
```

- Opción 2: Instalar PostgreSQL localmente

Si prefieres instalar PostgreSQL en tu computadora, descarga e instala la versión adecuada para tu sistema operativo desde la página oficial de [PostgreSQL](https://www.postgresql.org/download/).

Configuración en NestJS: En la configuración del módulo de TypeORM, podrás establecer los detalles de conexión a PostgreSQL en el código.

- Opción 3: Usar SQLite
Para simplificar, también se puede utilizar SQLite, que es más ligero y no requiere configuración de servidor de base de datos. A continuación se muestra la configuración básica para SQLite en NestJS con TypeORM. Esto se utilizará más adelante en la práctica si decides trabajar con SQLite en lugar de PostgreSQL:

```typescript
TypeOrmModule.forRoot({
      type: 'sqlite',
      database: 'db/sql.sqlite',
      autoLoadEntities: true,
      synchronize: true,
    })
```
