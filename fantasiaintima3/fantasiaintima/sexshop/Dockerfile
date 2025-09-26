# Usa una imagen base ligera de Python
FROM python:3.10-slim

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Si necesitas paquetes del sistema para compilar dependencias, descomenta y ajusta:
# RUN apt-get update && apt-get install -y --no-install-recommends build-essential gcc libpq-dev \
#     && rm -rf /var/lib/apt/lists/*

# Copiamos SOLO el requirements desde su ruta real en el repo (relative al build context '.')
COPY fantasiaintima3/fantasiaintima/sexshop/requirements.txt /app/requirements.txt

# Instala pip y dependencias
RUN pip install --upgrade pip \
    && pip install --no-cache-dir -r /app/requirements.txt

# Copiamos el resto del proyecto (contexto de build debe ser la raíz del repo)
COPY . /app

# Expone el puerto que usará Gunicorn en Render
EXPOSE 8000

# Comando por defecto (ajusta el módulo wsgi si tu proyecto tiene otro nombre)
CMD ["gunicorn", "sexshop.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "3"]
