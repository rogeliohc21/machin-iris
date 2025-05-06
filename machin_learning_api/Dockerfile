# Usar imagen oficial de Python
FROM python:3.10

# Crear directorio de trabajo
WORKDIR /app

# Copiar archivos
COPY app.py .
COPY models/ ./models/

# Instalar dependencias
RUN pip install flask joblib scikit-learn

# Exponer el puerto
EXPOSE 5001

# Comando de inicio
CMD ["python", "app.py"]
