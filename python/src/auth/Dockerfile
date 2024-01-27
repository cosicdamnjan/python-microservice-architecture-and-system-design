# Use the official Python 3.12 image as the base image
FROM python:3.12-slim-bullseye

# Set the working directory in the container
WORKDIR /app

# Install system-level dependencies
RUN apt-get update && apt-get install -y --no-install-recommends --no-install-suggests \
    build-essential default-libmysqlclient-dev pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Copy the requirements file to the container
COPY ./requirements.txt /app/

# Set environment variables for mysqlclient
ENV MYSQLCLIENT_CFLAGS="-I/usr/include/mysql"
ENV MYSQLCLIENT_LDFLAGS="-L/usr/lib/x86_64-linux-gnu -lmysqlclient"

# Upgrade pip and install Python packages
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Copy the rest of your application code into the container
COPY . /app/

# Expose the port your application will listen on
EXPOSE 5000

# Define the command to run your application
CMD ["python3", "server.py"]

