FROM java15:latest

ENV \
  WILDFLY_URL='https://download.jboss.org/wildfly/23.0.0.Final/wildfly-preview-23.0.0.Final.tar.gz' \
  WILDFLY_CHKSUM='34d38f73d18fab4dfb0d58159fc79657bec42692' \
  WILDFLY_HOME=/opt/wildfly

RUN curl -LfsSo /tmp/wildfly.tar.gz ${WILDFLY_URL}
RUN echo "${WILDFLY_CHKSUM} */tmp/wildfly.tar.gz" | sha1sum -c -

RUN useradd -b /opt -s /bin/sh -d /opt serveradmin && echo serveradmin:serveradmin | chpasswd

RUN \
    mkdir -p /opt/wildfly \
    && cd /opt/wildfly \
    && tar -xf /tmp/wildfly.tar.gz --strip-components=1 \
    && rm -rf /tmp/wildfly.tar.gz \
    && chown -R serveradmin:serveradmin /opt \
    && chmod a+x ${WILDFLY_HOME}/bin/standalone.sh \
    && chmod -R a+rw /opt


ENV DEPLOYMENT_DIR=${WILDFLY_HOME}/standalone/deployments
ENV CONFIGURATION_DIR=${WILDFLY_HOME}/standalone/configuration
ENV PATH="/opt/wildfly/bin:${PATH}"

ENTRYPOINT ${WILDFLY_HOME}/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0
EXPOSE 8080
EXPOSE 9990
