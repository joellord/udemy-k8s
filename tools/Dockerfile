FROM fedora:32

# Add repos
COPY ./docker-ce.repo /etc/yum.repos.d/docker-ce.repo
COPY ./kubernetes.repo /etc/yum.repos.d/kubernetes.repo
# install docker
RUN dnf -y update
RUN dnf -y install dnf-plugins-core
RUN dnf makecache
RUN dnf install -y docker-ce docker-ce-cli containerd.io
VOLUME /var/lib/docker
EXPOSE 2375

# install NodeJs
RUN dnf install -y nodejs

# install git
RUN dnf install -y git

# install code editors
RUN dnf install -y nano 
RUN dnf install -y jed

# install kubectl
RUN dnf install -y kubectl

#install minikube
RUN dnf install -y conntrack
RUN curl -Lo minikube https://storage.googleapis.com/minikube/releases/v0.25.0/minikube-linux-amd64 \
     && chmod +x minikube
RUN mkdir -p /usr/local/bin/
RUN install minikube /usr/local/bin/

EXPOSE 8080
EXPOSE 3000
EXPOSE 3001
EXPOSE 3306

# Environment setup
COPY start.sh /usr/local/bin/start.sh
RUN chmod +x /usr/local/bin/start.sh
RUN adduser course
COPY ./.bashrc /tmp/bashext
RUN cat /tmp/bashext >> ~/.bashrc
RUN cp ~/.bashrc /home/course/.bashrc
USER course
WORKDIR /home/course
