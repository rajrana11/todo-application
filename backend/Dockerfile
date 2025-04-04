# Use official Python image as base
FROM tiangolo/uwsgi-nginx-flask:python3.10

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Set working directory
WORKDIR /app

# Install system dependencies for building Python packages
RUN apt-get update && apt-get install -y \
    build-essential \
    gcc \
    libffi-dev \
    libssl-dev \
    python3-dev \
    && apt-get clean

# Install dependencies
COPY requirements.txt /app/

# Ensure pip is updated and install Python dependencies
RUN pip install --no-cache-dir --upgrade pip && pip install --no-cache-dir -r requirements.txt

# Copy application files
COPY . /app/

# Expose the application port (usually 5000 or 8000)
EXPOSE 5000

# Run the application after creating the DB
CMD ["sh", "-c", "python create_db.py && python main.py"]