# Usage: docker build . -t mydebian:4
FROM debian:buster

# Install sudo and python packages using apt-get
RUN apt-get update \
&& apt-get install -y python3 sudo \
&& rm -rf /var/lib/apt/lists/*

# Add simple user
RUN useradd -m ansible
RUN echo 'ansible:password' | chpasswd
# add sudo rule
RUN echo 'ansible    ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/ansible

#Add sshd service for awx

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:password' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]