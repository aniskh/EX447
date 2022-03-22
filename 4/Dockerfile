# Usage: docker build . -t mydebian:1
FROM debian:buster

# Install packages using apt-get
RUN apt-get update \
&& apt-get install -y python3 sudo \
&& rm -rf /var/lib/apt/lists/*

# Add simple user
RUN  useradd ansible

# Install sudo
RUN echo 'ansible    ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/ansible
