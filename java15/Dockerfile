FROM centos:8

RUN yum install -y glibc-locale-source
RUN localedef --no-archive -i en_US -f UTF-8 en_US.UTF-8

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN yum install -y tzdata openssl curl ca-certificates fontconfig gzip tar \
  && yum update -y yum clean all

ENV BINARY_URL='https://github.com/AdoptOpenJDK/openjdk15-binaries/releases/download/jdk-15.0.1%2B9/OpenJDK15U-jdk_aarch64_linux_hotspot_15.0.1_9.tar.gz'
ENV CHKSUM='84398a1566d66ee5a88f3326fb7f0b70504eb510190f8f798bdb386481a3900e'

RUN curl -LfsSo /tmp/openjdk.tar.gz ${BINARY_URL}
RUN echo "${CHKSUM} */tmp/openjdk.tar.gz" | sha256sum -c -

RUN \
  mkdir -p /opt/java/openjdk; \
  cd /opt/java/openjdk; \
  tar -xf /tmp/openjdk.tar.gz --strip-components=1; \
  rm -rf /tmp/openjdk.tar.gz;

ENV JAVA_HOME=/opt/java/openjdk \
    PATH="/opt/java/openjdk/bin:${PATH}"
