FROM java:8

ENV ACTIVATOR_VERSION 1.3.7

# Install activator
RUN wget http://downloads.typesafe.com/typesafe-activator/$ACTIVATOR_VERSION/typesafe-activator-$ACTIVATOR_VERSION.zip && \
    unzip typesafe-activator-$ACTIVATOR_VERSION.zip && \
    mv activator-dist-$ACTIVATOR_VERSION /opt/activator && \
    rm typesafe-activator-$ACTIVATOR_VERSION.zip

# Add PATH
RUN export PATH=$PATH:/opt/activator

# Default port
EXPOSE 9999
# Debug port
EXPOSE 8888