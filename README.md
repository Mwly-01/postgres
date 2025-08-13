# PostgreSQL con Docker 

# Creación del Contenedor 
```bash
docker run -d --name postgres_container -e POSTGRES_USER=admin -e POSTGRES_PASSWORD=admin -e POSTGRES_DB=campus -p 5433:5432 -v pgdata:/var/lib/postgresql/data --restart=unless-stopped postgres:15
docker 
```

## Conectar al Contenedor de Docker
```bash
docker exec -it postgres_container bash
```
## Conectar con PostgreSQL bajo Consola
```bash
psql --host=localhost --username=admin  -d campus --password admin
psql -h localhost -u admin -w admin -d campus
```

### Para usuario por defecto
```bash
psql ... --username=postgres ...
```
### descargar database client
