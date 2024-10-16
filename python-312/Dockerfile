FROM python:3.12-slim

# Define a build argument for the username
ARG USERNAME=jsuser

# Install cron, supervisor, and other utilities
RUN apt-get update && apt-get install -y \
    sudo \
    supervisor \
    cron \
    git \
    nano \
    build-essential \
    libzstd-dev \
    python3-dev \
    gcc \
    && apt-get clean

# Create a user with the username specified in the build argument and a home directory
RUN useradd -m -s /bin/bash $USERNAME

# Set user permissions and allow sudo if needed
RUN echo "$USERNAME ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Ensure the correct permissions for log files or directories
RUN mkdir -p /var/log && \
    touch /var/log/cron.log /var/log/cron.error.log && \
    chmod 666 /var/log/cron.log /var/log/cron.error.log && \
    chown -R $USERNAME:$USERNAME /var/log

# Switch to non-root user after necessary setup is done
USER $USERNAME

# Set the working directory for the created user
WORKDIR /home/$USERNAME

# Add the local bin directory to PATH
ENV PATH="/home/$USERNAME/.local/bin:${PATH}"