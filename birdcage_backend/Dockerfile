# Use the official Python 3.10 image as the base image
FROM python:3.10

# Install system dependencies
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y ffmpeg pulseaudio && rm -rf /var/lib/apt/lists/*

COPY requirements.txt /tmp

# Install Python packages from requirements.txt
RUN pip install -r /tmp/requirements.txt

# Copy files into the container
COPY run.py start_app.sh config.py celery_worker.py /
COPY app /app

# Set environment variables
ENV DATABASE_FILE=/db/birdcage.db \
    API_SERVER_PORT=7007 \
    TEMP_DIR_NAME=tmp \
    ANALYZE_SERVER=127.0.0.1 \
    ANALYZE_PORT=7667 \
    DETECTION_DIR_NAME=detections \
    CORS_ORIGINS=http://192.168.1.75:7008 \
    REDIS_SERVER=127.0.0.1 \
    REDIS_PORT=6379

# Grant execution permission to start_app.sh
RUN chmod +x start_app.sh

# Start the app
CMD ["./start_app.sh"]
