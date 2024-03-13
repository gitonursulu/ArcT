FROM jenkins/jenkins:lts
USER root

# Gerekli paketleri kurun
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common

# Docker reposunu ve anahtarını ekleyin
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable"

# Docker CLI'yi kurun
RUN apt-get update -qq \
    && apt-get install -qqy docker-ce-cli

# Docker grubunu oluşturun ve Jenkins kullanıcısını bu gruba ekleyin
RUN groupadd -f docker \
    && usermod -aG docker jenkins

    # Tini'yi indirin ve yükleyin
RUN curl -fsSL https://github.com/krallin/tini/releases/download/v0.19.0/tini -o /bin/tini \
    && chmod +x /bin/tini

USER jenkins

# ENTRYPOINT'i varsayılana ayarlayın
ENTRYPOINT ["/bin/tini", "--", "/usr/local/bin/jenkins.sh"]
