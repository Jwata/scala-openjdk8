FROM jwata:debian-openjdk8

MAINTAINER Junji Watanabe

# Install requirements
RUN apt-get install -y wget curl

RUN \
  echo 'Installing scala...' && \
  wget "http://www.scala-lang.org/files/archive/scala-$SCALA_VERSION.tgz" && \
  tar xzf scala-$SCALA_VERSION.tgz -C /tmp/ && rm -rf scala-$SCALA_VERSION.tgz && \
  mv /tmp/scala-$SCALA_VERSION /usr/share/scala && \
  ln -s /usr/share/scala/bin/* /usr/local/bin/ && \

  echo 'Installing sbt...' && \
  curl -O -J -L "http://dl.bintray.com/typesafe/ivy-releases/org.scala-sbt/sbt-launch/$SBT_VERSION/sbt-launch.jar" && mv sbt-launch.jar /usr/local/bin/ && \
  touch /usr/local/bin/sbt && \
  echo '#!/bin/bash' >> /usr/local/bin/sbt && \
  echo 'SBT_OPTS="-Xms512M -Xmx1536M -Xss1M -XX:+CMSClassUnloadingEnabled"' >> /usr/local/bin/sbt && \
  echo 'java $SBT_OPTS -jar `dirname $0`/sbt-launch.jar "$@"' >> /usr/local/bin/sbt && \
  chmod u+x /usr/local/bin/sbt && \

  echo 'Fetching all sbt related dependencies...' && \
  mkdir -p /tmp/sbt-dummy && \
  echo 'name := "DummyProject"' > /tmp/sbt-dummy/build.sbt && \
  echo 'version := "1.0"' >> /tmp/sbt-dummy/build.sbt && \
  echo "scalaVersion := \"$SCALA_VERSION\"" >> /tmp/sbt-dummy/build.sbt && \
  mkdir -p /tmp/sbt-dummy/src/main/scala && \
  echo 'object Main { def main(args: Array[String]) = println("Dummy") }' > /tmp/sbt-dummy/src/main/scala/Main.scala && \
  cd /tmp/sbt-dummy && sbt run && \

  echo 'removing temporary directory'
  rm -rf /tmp/*
