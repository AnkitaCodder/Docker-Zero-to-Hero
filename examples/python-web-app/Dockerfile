# Base image
FROM ubuntu:latest

# Set working directory
WORKDIR /app

# Install Python and pip
RUN apt-get update && apt-get install -y python3 python3-pip python3-venv && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Copy only requirements first (for better caching)
COPY requirements.txt .

# Create and use virtual environment
RUN python3 -m venv /opt/venv
ENV PATH="/opt/venv/bin:$PATH"

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the app code
COPY devops /app/

# Run database migrations (optional — better to do at runtime)
# RUN python manage.py migrate

# Expose Django port
EXPOSE 8000

# Run the Django app
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]




