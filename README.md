 
# Crear redes  para contenedores de PostgreSQL y Grafana
docker network create res_monitoreo
# Crear volumenes para contenedores de PostgreSQL y Grafana
docker volume create grafana-storage 
docker volume create postgres-data
docker volume create grafana-config 
docker volume create grafana-logs 
docker volume create grafana-storage
docker volume create prometheus-data

 ####################################################################
# Crear contenedor de PostgreSQL para Grafana
docker run -d \
  --name grafana-postgres \
  --network red_monitoreo \
  -v postgres-data:/var/lib/postgresql/data \
  -e POSTGRES_PASSWORD=grafanapass \
  -e POSTGRES_USER=grafana \
  -e POSTGRES_DB=grafana \
  --restart unless-stopped \
  postgres:16.8



# Crear contenedor de Grafana 
docker run -d \
 --name grafana \
 --network red_monitoreo \
 -p 3000:3000 \
 -v grafana-config:/etc/grafana \
 -v grafana-logs:/var/log/grafana \
 -e "GF_DATABASE_TYPE=postgres" \
 -e "GF_DATABASE_HOST=grafana-postgres:5432" \
 -e "GF_DATABASE_NAME=grafana" \
 -e "GF_DATABASE_USER=grafana" \
 -e "GF_DATABASE_PASSWORD=grafanapass" \
 --restart unless-stopped \
 grafana/grafana-oss:11.5.3


# Crear contenedor de Prometheus
docker run \
    -p 9090:9090 \
    -v /path/to/prometheus.yml:/etc/prometheus/prometheus.yml \
    -v prometheus-data:/prometheus \
    prom/prometheus
#######################################################################





# Construir imagen personalizada de PostgreSQL
cd postgres
docker build -t postgres:16.8 .

# Construir imagen personalizada de Grafana
cd ../grafana
docker build -t grafana:11.5.3 .

# Construir imagen personalizada de Prometheus
cd ../prometheus
docker build -t prometheus:2.45 .

# Ejecutar PostgreSQL personalizado
docker run -d \
  --name grafana-postgres \
  --network red_monitoreo \
  -v postgres-data:/var/lib/postgresql/data \
  --restart unless-stopped \
  postgres:16.8

# Ejecutar Grafana personalizado
docker run -d \
  --name grafana \
  --network red_monitoreo \
  -p 3000:3000 \
  -v grafana-config:/etc/grafana \
  -v grafana-logs:/var/log/grafana \
  -v grafana-storage:/var/lib/grafana \
  -e "GF_DATABASE_TYPE=postgres" \
  -e "GF_DATABASE_HOST=grafana-postgres:5432" \
  -e "GF_DATABASE_NAME=grafana" \
  -e "GF_DATABASE_USER=grafana" \
  -e "GF_DATABASE_PASSWORD=grafanapass" \
  --restart unless-stopped \
  grafana:11.5.3

# Ejecutar Prometheus personalizado
docker run -d \
  --name prometheus \
  --network red_monitoreo \
  -p 9090:9090 \
  -v prometheus-data:/prometheus \
  --restart unless-stopped \
  prometheus:2.45
  



# Comando para copiar los archivos de configuración
docker cp grafana:/var/lib/grafana/. lib
docker cp grafana:/etc/grafana/. etc
docker cp prometheus:/etc/prometheus/prometheus.yml prometheus.yml

docker cp prometheus:/etc/prometheus/alerts.yml alerts.yml
