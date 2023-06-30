# Use the base Jenkins slave image with CentOS 7 version 3.11
FROM openshift/jenkins-slave-base-centos7:v3.11
# Define build-time arguments for component versions
ARG KUBECTL_VERSION=$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)
ARG HADOLINT_VERSION=v2.10.0
ARG TFENV_VERSION=v2.2.2
ARG HELM_VERSION=3.7.1
# Switch to root user to install dependencies
USER root
# Update and install Java 11 and OpenSSL
RUN yum -y update && \
    yum install -y java-11-openjdk-devel openssl && \
    yum clean all -y

# Install kubectl
RUN curl -LO "https://storage.googleapis.com/kubernetes-release/release/$KUBECTL_VERSION/bin/linux/amd64/kubectl" && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/

# Install Helm 3
RUN curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 && \
    chmod 700 get_helm.sh && \
    ./get_helm.sh --version $HELM_VERSION
# Install Helm plugin for ChartMuseum push    
RUN helm plugin install https://github.com/chartmuseum/helm-push.git

# Install Hadolint for Dockerfile linting
RUN curl -sL -o hadolint "https://github.com/hadolint/hadolint/releases/download/$HADOLINT_VERSION/hadolint-Linux-x86_64" && \
    chmod +x hadolint && \
    mv hadolint /usr/local/bin/
# Install tfenv for Terraform version management
RUN wget https://github.com/tfutils/tfenv/archive/refs/tags/$TFENV_VERSION.tar.gz && \
    tar xf $TFENV_VERSION.tar.gz && \
    mv tfenv-$TFENV_VERSION /opt/tfenv && \
    ln -s /opt/tfenv/bin/* /usr/local/bin
# Set environment variables
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk
ENV PATH $PATH:$JAVA_HOME/bin
# Set ownership and permissions for tfenv directory
RUN chown -R 1001:0 /opt/tfenv && \
    chmod -R g+rw /opt/tfenv
# Switch to non-root user
USER 1001
