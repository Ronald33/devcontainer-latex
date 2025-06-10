FROM pandoc/latex:3.7-ubuntu

# Arguments for non-root user (commented out if not used yet)
ARG USER_NAME=ubuntu
ARG USER_ID=1000
ARG GROUP_NAME=nonroot

# Environment variables
ENV DEBIAN_FRONTEND=noninteractive
ENV MY_WORKDIR=/workdir
# Useds in entrypoint
ENV MY_USER_NAME=${USER_NAME}
ENV MY_GROUP_NAME=${GROUP_NAME}

# System dependencies installation
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    tini && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    
# Create user and group (uncomment if you want to control UID/GID manually)
#RUN groupadd --force $GROUP_NAME && useradd -G $GROUP_NAME --uid $USER_ID -s /bin/bash -m $USER_NAME

# Create working directory with proper permissions
RUN mkdir -p $MY_WORKDIR

# Copy entrypoint
COPY ./update-permissions.sh /usr/local/bin/update-permissions.sh
RUN chmod +x /usr/local/bin/update-permissions.sh

# Switch to the created user
USER $USER_NAME

# Set working directory
WORKDIR $MY_WORKDIR

# Use tini as the init system to handle zombie processes
ENTRYPOINT ["/usr/bin/tini", "--"]

# Keep the container running indefinitely
CMD ["bash", "update-permissions.sh"]
