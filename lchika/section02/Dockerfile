FROM openjdk:11.0.3-jre-slim
MAINTAINER Ryosuke Kataoka<kataoka.ryosuke1@gmail.com>

RUN apt-get update
RUN apt-get install unzip
RUN mkdir -p /opt/led

ADD rpi-led-*.zip /opt/led

RUN cd /opt/led && \
  cmd=$(basename rpi-led-*.zip .zip) && \
  unzip -q $cmd.zip && \
  echo /opt/led/$cmd/bin/rpi-led '$RPI_LED_OPTS' > /opt/led/launch.sh '&' && \
  echo trap '"echo TERM signal detected."' TERM >> /opt/led/launch.sh && \
  echo wait >> /opt/led/launch.sh && \
  chmod +x /opt/led/launch.sh

EXPOSE 8080
ENTRYPOINT ["/bin/bash", "-c", "opt/led/launch.sh"]
