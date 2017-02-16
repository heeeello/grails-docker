FROM java:8
MAINTAINER jim.mei@centling.com

# Set customizable env vars defaults.
ENV GRAILS_VERSION 3.2.6

# Install Grails
WORKDIR /usr/lib/jvm
RUN wget https://github.com/grails/grails-core/releases/download/v$GRAILS_VERSION/grails-$GRAILS_VERSION.zip && \
    unzip grails-$GRAILS_VERSION.zip && \
    rm -rf grails-$GRAILS_VERSION.zip && \
    ln -s grails-$GRAILS_VERSION grails

# Setup Grails path.
ENV GRAILS_HOME /usr/lib/jvm/grails
ENV PATH $GRAILS_HOME/bin:$PATH

# Create App Directory
RUN mkdir /app

# Set Workdir
WORKDIR /app

# Run Grails dependency-report command to pre-download dependencies but not 
# create unnecessary build files or artifacts.
RUN grails create-app --inplace --profile rest-api  
RUN grails dependency-report

# Set Default Behavior
ENTRYPOINT ["/bin/bash"]

# install vim
RUN apt-get update && apt-get install -y vim 

# put /usr/lib/jvm/grails/bin/ to path
RUN echo 'export PATH=/usr/lib/jvm/grails/bin/:$PATH'  >> /root/.bashrc
