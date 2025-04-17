FROM postgres:16.8

# Agregar etiquetas de metadatos
# LABEL maintainer="Tu Nombre <tu@email.com>"
# LABEL version="1.0"
LABEL description="PostgreSQL personalizado para Grafana"

# Establecer variables de entorno predeterminadas
ENV POSTGRES_USER=grafana
ENV POSTGRES_PASSWORD="grafanapass"
ENV POSTGRES_DB=grafana

# Copiar script de inicialización
# COPY init.sql /docker-entrypoint-initdb.d/

# Personalizar configuración si es necesario
# COPY postgresql.conf /etc/postgresql/postgresql.conf

# puerto expuesto
EXPOSE 5432