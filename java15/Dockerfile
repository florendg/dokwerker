FROM centos:8

RUN yum install -y glibc-locale-source
RUN localedef --no-archive -i en_US -f UTF-8 en_US.UTF-8

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN yum install -y tzdata openssl curl ca-certificates fontconfig gzip tar \
  && yum update -y yum clean all

ENV BINARY_URL='https://github.com/AdoptOpenJDK/openjdk15-binaries/releases/download/jdk15u-2021-01-22-02-31/OpenJDK15U-jdk_x64_linux_hotspot_2021-01-22-02-31.tar.gz'
ENV CHKSUM='eee6ea48d0dccfdc6c229e6635776aa8245d8d11b69bbf470f30d92b5e8ac8b8'

RUN curl -LfsSo /tmp/openjdk.tar.gz ${BINARY_URL}
RUN echo "${CHKSUM} */tmp/openjdk.tar.gz" | sha256sum -c -

RUN \
  mkdir -p /opt/java/openjdk; \
  cd /opt/java/openjdk; \
  tar -xf /tmp/openjdk.tar.gz --strip-components=1; \
  rm -rf /tmp/openjdk.tar.gz;

ENV JAVA_HOME=/opt/java/openjdk \
    PATH="/opt/java/openjdk/bin:${PATH}"
