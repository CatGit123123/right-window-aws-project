# Use an official Python runtime as a parent image with updated base
FROM public.ecr.aws/docker/library/python:3.10-slim-bookworm

# Create a non-root user
RUN useradd -m -u 1000 appuser

# Set the working directory in the container to /app
WORKDIR /app

# Copy only requirements first for better layer caching
COPY requirements.txt /app/

# Upgrade pip and install Python dependencies
RUN python -m pip install --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code
COPY . /app

# Create required directories
RUN mkdir -p /output/AutotagPDF \
    /output/ExtractTextInfoFromPDF \
    /output/zipfile/images

# Verify that the application files are present
RUN ls -la /app

# Change ownership of the app and output directories to appuser
RUN chown -R appuser:appuser /app /output

# Switch to non-root user
USER appuser

# Set the command to run the Python script when the container launches
CMD ["python", "./autotag.py"]
