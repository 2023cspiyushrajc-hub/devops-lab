# Base image
FROM python:3.12-slim

# Working directory inside container
WORKDIR /app

# Copy dependency list first (better caching)
COPY requirements.txt .

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy app code
COPY . .

# Environment variables
ENV FLASK_ENV=production
ENV REDIS_HOST=redis

# Port the app listens on
EXPOSE 5000

# Health check
HEALTHCHECK --interval=30s --timeout=5s \
  CMD curl -f http://localhost:5000/health || exit 1

# Start the app with gunicorn
CMD ["gunicorn","--bind","0.0.0.0:5000","--workers","2","app:app"]
