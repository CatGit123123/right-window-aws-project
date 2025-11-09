# Use an official Python runtime as a parent image
FROM python:3.10-slim-buster

# Create a non-root user
RUN useradd -m -u 1000 appuser

# Set the working directory in the container to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . /app

# Create required directories
RUN mkdir -p /output/AutotagPDF \
    /output/ExtractTextInfoFromPDF \
    /output/zipfile/images

# Upgrade pip and install Python dependencies
RUN python -m pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

# Change ownership of the app and output directories to appuser
RUN chown -R appuser:appuser /app /output

# Switch to non-root user
USER appuser

# Verify that the application files are present
RUN ls -la /app

# Set the command to run the Python script when the container launches
CMD ["python", "./autotag.py"]
