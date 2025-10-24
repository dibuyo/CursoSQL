# CursoSQL - Entorno dockerizado 🚀

Entorno listo para practicar SQL con PostgreSQL, MySQL y SQL Server, acompañado de herramientas visuales (Metabase, pgAdmin y phpMyAdmin). Todo se orquesta con Docker Compose para que puedas replicar el laboratorio en segundos.

- 🧠 Postgres centraliza la base de Metabase.
- 🔄 MySQL y SQL Server permiten contrastar motores y sintaxis.
- 🎯 Metabase, pgAdmin y phpMyAdmin facilitan la exploracion y visualizacion.

## Requisitos previos ⚙️

- 🐳 Docker Engine 24+ y Docker Compose Plugin.
- 📁 Acceso para crear carpetas en el directorio del proyecto (volumenes persistentes).

## Configuracion de variables 🔐

1. Copia el archivo de ejemplo: `cp .env.example .env`.
2. Completa los valores sensibles en `.env`. Nunca lo compartas ni lo subas al control de versiones.

Variables principales:

| Variable | Rol | Comentario |
| --- | --- | --- |
| `PATH_DATA` | Ruta local para los volumenes | Por defecto usa `./_data`. Puedes apuntar a otra carpeta absoluta. |
| `METABASE_DB_TYPE`, `METABASE_DB_NAME`, `POSTGRES_HOST`, `POSTGRES_PORT`, `POSTGRES_USER`, `POSTGRES_PASSWORD` | Parametrizan la base interna de Metabase (en Postgres). | Usa credenciales coherentes con la configuracion de `postgres`. |
| `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD` | Inicializan MySQL. | Evita credenciales triviales. |
| `PGADMIN_DEFAULT_EMAIL`, `PGADMIN_DEFAULT_PASSWORD` | Acceso a pgAdmin. | Pueden ser diferentes al correo personal. |
| `MSSQL_SA_PASSWORD` | Clave del usuario `sa` en SQL Server. | Debe cumplir las reglas de complejidad de Microsoft. |

> 💡 Consejo: si necesitas distinguir entornos (local, laboratorio, etc.), utiliza diferentes carpetas en `PATH_DATA` para mantener los datos separados.

## Puesta en marcha ▶️

```bash
docker compose up -d
```

El primer arranque puede tardar unos minutos mientras se descargan las imagenes y se inicializan los volumenes persistentes en `_data/`.

### Comandos utiles 🧰

- 👁️ Ver estado de los contenedores: `docker compose ps`
- 📡 Seguir los logs de un servicio: `docker compose logs -f <servicio>`
- 🔁 Reiniciar todo: `docker compose down && docker compose up -d`
- 📴 Detener sin borrar volumenes: `docker compose stop`

## Servicios expuestos 🌐

| Servicio | URL / Puerto local | Notas |
| --- | --- | --- |
| PostgreSQL | `localhost:5432` | Credenciales definidas en `.env`. |
| MySQL | `localhost:3306` | Usuario raiz y de aplicacion segun `.env`. |
| SQL Server | `localhost:1433` | Accede con `sa` y la clave configurada. |
| Metabase | http://localhost:8082 | Metabase guarda su metadata en Postgres. |
| pgAdmin | http://localhost:5050 | Cuenta inicial tomada de `.env`. Se conecta solo a Postgres via `pgadmin/servers.json`. |
| phpMyAdmin | http://localhost:6060 | Host preconfigurado `mysql`. |

## Estructura del proyecto 🗂️

```
.
├── docker-compose.yaml   # Orquestacion principal
├── .env.example          # Plantilla de variables
├── _data/                # Volumenes persistentes (se crean al primer arranque)
└── pgadmin/servers.json  # Conexion automatica a Postgres desde pgAdmin
```

## Consejos para el aula 📚

- 💾 Realiza respaldos copiando las carpetas dentro de `_data/` cuando los contenedores esten detenidos.
- 🔄 Si una herramienta no responde tras cambios en `.env`, ejecuta `docker compose down` y vuelve a levantar para aplicar la configuracion.
- 🤫 Comparte solo el archivo `.env.example`; mantén tus credenciales en privado.

Listo. Con este stack puedes dedicarte a practicar SQL sin invertir tiempo en instalaciones individuales. ✨
