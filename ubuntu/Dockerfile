FROM ubuntu:18.04

RUN apt-get update && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y ant && \
    apt-get clean;
    
# Fix certificate issues
RUN apt-get update && \
    apt-get install ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f;

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
ENV LANG C.UTF-8
RUN export JAVA_HOME

RUN apt-get update && \
 apt-get install -y openssh-server && \
 apt-get install -y python3-pip && \
 pip3 install --upgrade setuptools && \ 
 pip3 install --upgrade pip && \
 pip3 install ansible --upgrade

RUN useradd remote_user && \
    echo "remote_user:1234" | chpasswd && \
    mkdir /home/remote_user/.ssh -p && \
    chmod 700 /home/remote_user/.ssh && \
    mkdir -p -m0755 /var/run/sshd

COPY remote_key.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user   -R /home/remote_user && \
    chmod 400 /home/remote_user/.ssh/authorized_keys

CMD /usr/sbin/sshd -D
