# FROM jenkins/jenkins:alpine

# USER root

# # Install Docker CLI
# RUN apk add --update docker openrc

# # Install app dependencies
# RUN apk add --no-cache openjdk11 python3 py3-pip curl unzip zip bash

# # Install Gradle manually (Alpine may not have a compatible version)
# RUN mkdir /opt/gradle \
#   && curl -sSL https://services.gradle.org/distributions/gradle-7.6-bin.zip -o gradle.zip \
#   && unzip gradle.zip -d /opt/gradle \
#   && ln -s /opt/gradle/gradle-7.6/bin/gradle /usr/bin/gradle \
#   && rm gradle.zip

# # Install pipenv
# RUN pip3 install pipenv --break-system-packages

# # Install Chromedriver
# RUN curl -sSL https://chromedriver.storage.googleapis.com/113.0.5672.63/chromedriver_linux64.zip -o chromedriver.zip \
#     && unzip chromedriver.zip \
#     && mv chromedriver /usr/local/bin/ \
#     && rm chromedriver.zip

# # Copy your app source and configs
# COPY . /workspace
# WORKDIR /workspace

# RUN chmod +x gradlew
# RUN pipenv install

# ENV GRADLE_OPTS="-Dprojectname=ensf400-finalproject"
# EXPOSE 8080

# # Optional: if this is an agent, don't run the app directly
# #CMD ["jenkins-agent"]

FROM jenkins/jenkins:alpine
# switch to root user
USER root

# install docker on top of the base image
RUN apk add --update docker openrc

# Install Gradle dependencies
RUN apk add --no-cache \
    openjdk11 \
    bash \
    docker \
    curl \
    unzip

# Set Gradle version
ENV GRADLE_VERSION=7.6
ENV GRADLE_HOME=/opt/gradle
# Download and install Gradle
RUN mkdir -p ${GRADLE_HOME} && \
    curl -fsSL https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o /tmp/gradle.zip && \
    unzip /tmp/gradle.zip -d /opt/gradle && \
    rm /tmp/gradle.zip

# Add Gradle to PATH
ENV PATH="${GRADLE_HOME}/gradle-${GRADLE_VERSION}/bin:${PATH}"

# Verify installation
RUN gradle -v

