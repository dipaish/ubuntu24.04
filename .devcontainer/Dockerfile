# Use the official Ubuntu image as a base
FROM ubuntu:24.04

# Prevent interactive prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update the package list and install common dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    wget \
    git \
    vim \
    && rm -rf /var/lib/apt/lists/*

# (Optional) Set a working directory
WORKDIR /workspace
