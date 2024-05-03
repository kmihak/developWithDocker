# Use the official Python image from Docker Hub
FROM python:3.8.18-slim-bullseye

# Find the local file platform for local image build:
# docker inspect --format='{{.Os}}/{{.Architecture}}' <IMAGE_NAME>
# FROM --platform=linux/amd64 <IME>:<TAG>

# Arguments from the "docker build ..." command
ARG USER_ID
ARG GROUP_ID

# Set the working directory in the container
WORKDIR /workspace

# Linux dependencies
RUN apt-get update && \
  apt-get install -y build-essential sudo unzip bzip2 autoconf && \ 
  # apt-get install -y git wget && \
  # gcc g++ is necessary for pytorch and some other C++ demanding dependencies
  # apt-get install -y gcc g++ make && \
  rm -rf /var/lib/apt/lists/*
  
# Copy the Python script into the container
# COPY helloworld.py /workspace/
COPY . /workspace

# update and install packages in python
RUN pip install --upgrade pip && \
  pip install -r req.txt

# Add your user to the environment helps with mounts and creating and saving files
RUN useradd user -u $USER_ID -g $GROUP_ID -m -s /bin/bash
RUN chown -R $USER_ID:$GROUP_ID /workspace 

# Run the Python script
CMD ["python", "helloworld.py"]
