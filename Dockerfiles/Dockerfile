FROM openshift/jenkins-slave-base-centos7:v3.11

USER root

RUN yum -y update && \
    yum install -y java-11-openjdk-devel openssl && \
    yum clean all -y

RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/

RUN curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 && \
    chmod 700 get_helm.sh && \
    ./get_helm.sh

RUN helm plugin install https://github.com/chartmuseum/helm-push.git

RUN curl -sL -o hadolint "https://github.com/hadolint/hadolint/releases/download/v2.10.0/hadolint-Linux-x86_64" && \
    chmod +x hadolint && \
    mv hadolint /usr/local/bin/

RUN wget https://github.com/tfutils/tfenv/archive/refs/tags/v2.2.2.tar.gz && \
    tar xf v2.2.2.tar.gz && \
    mv tfenv-2.2.2 /opt/tfenv && \
    ln -s /opt/tfenv/bin/* /usr/local/bin

ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk
ENV PATH $PATH:$JAVA_HOME/bin

RUN chown -R 1001:0 /opt/tfenv && \
    chmod -R g+rw /opt/tfenv

COPY agent.jar /usr/local/bin/

USER 1001
