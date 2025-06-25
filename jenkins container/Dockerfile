FROM jenkins/jenkins:lts-jdk17

USER root

RUN apt-get update && \
    apt-get install -y \
    php-cli php-mbstring php-dom php-tidy php-curl composer \
    python3 python3-pip python3-venv \
    xsltproc wkhtmltopdf \
    curl wget gnupg apt-transport-https lsb-release && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    mkdir -p /usr/share/java/ && \
    curl -o /usr/share/java/junit-xml.xsl https://raw.githubusercontent.com/junit-team/junit5/main/platform-tests/src/test/resources/junit-xml.xsl && \
    curl -fsSL https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor -o /etc/apt/trusted.gpg.d/trivy.gpg && \
    echo "deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/trivy.list && \
    apt-get update && \
    apt-get install -y trivy && \
    apt-get clean && rm -rf /var/lib/apt/lists/*


VOLUME /var/jenkins_home
VOLUME /var/run/docker.sock

EXPOSE 8080 50000

CMD ["/usr/local/bin/jenkins.sh"]