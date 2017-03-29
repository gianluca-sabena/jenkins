FROM openshift/jenkins-slave-base-centos7

ENV MAVEN_VERSION=3.3.9

# Install Maven
RUN INSTALL_PKGS="java-1.8.0-openjdk-devel which" && \
    yum install -y --enablerepo=centosplus $INSTALL_PKGS && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y && \
    (curl -v https://www.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | \
    tar -zx -C /usr/local) && \
    ln -sf /usr/local/apache-maven-$MAVEN_VERSION/bin/mvn /usr/local/bin/mvn && \
    mkdir -p $HOME/.m2

ENV SBT_OPTS=" -Dsbt.log.noformat=true -Xms512M -Xmx2G  -Xss2M -XX:+CMSClassUnloadingEnabled "
RUN curl -s https://raw.githubusercontent.com/paulp/sbt-extras/master/sbt > /usr/local/bin/sbt  && chmod 0777 /usr/local/bin/sbt

RUN echo "TEST" > /test.txt

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
