# Imagen base oficial de Python
FROM python:3.11-slim

# Establece el directorio de trabajo
WORKDIR /app

# Copia los archivos de la app
COPY . .

# Instala las dependencias
RUN pip install --no-cache-dir -r requirements.txt

# Expone el puerto de la app (usualmente 5000)
EXPOSE 5000

# Comando para ejecutar la app (ajústalo si usas FastAPI o gunicorn)
CMD ["python", "app.py"]
