FROM prom/prometheus:v2.45.0

#LABEL maintainer="Tu Nombre <tu@email.com>"
LABEL description="Prometheus personalizado para monitoreo de red"

# Copiar archivo de configuración personalizado
#COPY prometheus.yml /etc/prometheus/prometheus.yml
#COPY alerts.yml /etc/prometheus/alerts.yml

# Exponer puerto
EXPOSE 9090

# Los archivos de configuración necesarios son prometheus.yml y alerts.yml
# que debes crear en el mismo directorio que este Dockerfile