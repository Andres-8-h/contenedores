FROM grafana/grafana-oss:11.5.3

# Agregar etiquetas de metadatos
# LABEL maintainer="Tu Nombre <tu@email.com>"
# LABEL version="1.0"
LABEL description="Grafana personalizado para monitoreo"

# Copiar archivo de configuración personalizado
#COPY grafana.ini /etc/grafana/grafana.ini

# Instalar plugins adicionales
RUN grafana-cli plugins install grafana-clock-panel
RUN grafana-cli plugins install grafana-piechart-panel
RUN grafana-cli plugins install grafana-worldmap-panel
RUN grafana-cli plugins install grafana-statusmap-panel
RUN grafana-cli plugins install grafana-network-panel


# puerto expuesto
EXPOSE 3000