FROM weirdduke/java15:latest

ENV \
  KEYCLOAK_URL='https://downloads.jboss.org/keycloak/11.0.3/keycloak-11.0.3.tar.gz' \
  KEYCLOAK_CHKSUM='87bae7fd63b49756f54e4e293fb37329f117e30d' \
  KEYCLOAK_HOME=/opt/keycloak

RUN groupadd --gid 5000 keycloak \
    && useradd --home-dir /home/keycloak --create-home --uid 5000 \
        --gid 5000 --shell /bin/sh --skel /dev/null keycloak

RUN curl -LfsSo /tmp/keycloak.tar.gz ${KEYCLOAK_URL}
RUN echo "${KEYCLOAK_CHKSUM} */tmp/keycloak.tar.gz" | sha1sum -c -

RUN \
    mkdir -p /opt/keycloak \
    && cd /opt/keycloak \
    && tar -xf /tmp/keycloak.tar.gz --strip-components=1 \
    && rm -rf /tmp/keycloak.tar.gz \
    && chown -R keycloak:keycloak /opt \
    && chmod a+x ${KEYCLOAK_HOME}/bin/standalone.sh \
    && chmod -R a+rw /opt

ENV CONFIGURATION_DIR=${KEYCLOAK_HOME}/standalone/configuration
ENV PATH="/opt/keycloak/bin:${PATH}"

RUN /opt/keycloak/bin/add-user.sh -u master -p mariner --silent

RUN /opt/keycloak/bin/add-user-keycloak.sh -u admin -p admin

ENTRYPOINT ${KEYCLOAK_HOME}/bin/standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0
EXPOSE 8080
EXPOSE 9990

