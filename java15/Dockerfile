FROM centos:8

RUN yum install -y glibc-locale-source
RUN localedef --no-archive -i en_US -f UTF-8 en_US.UTF-8

ENV LANG='en_US.UTF-8' LANGUAGE='en_US:en' LC_ALL='en_US.UTF-8'

RUN yum install -y tzdata openssl curl ca-certificates fontconfig gzip tar \
  && yum update -y yum clean all

ENV BINARY_URL='https://github.com/AdoptOpenJDK/openjdk15-binaries/releases/download/jdk-15%2B36/OpenJDK15U-jre_x64_linux_hotspot_15_36.tar.gz'
ENV CHKSUM='230d97a6b16a0735f15013a91f7582a22282ec12bdfaec291ab63274cc075efb'

RUN curl -LfsSo /tmp/openjdk.tar.gz ${BINARY_URL}
RUN echo "${CHKSUM} */tmp/openjdk.tar.gz" | sha256sum -c -

RUN \
  mkdir -p /opt/java/openjdk; \
  cd /opt/java/openjdk; \
  tar -xf /tmp/openjdk.tar.gz --strip-components=1; \
  rm -rf /tmp/openjdk.tar.gz;

ENV JAVA_HOME=/opt/java/openjdk \
    PATH="/opt/java/openjdk/bin:${PATH}"
