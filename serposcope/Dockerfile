ARG UBUNTU_DOCKER_IMAGE
FROM ${UBUNTU_DOCKER_IMAGE}

ARG SERPOSCOPE_VERSION
# ENV SERPOSCOPE_VERSION=${SERPOSCOPE_VERSION}

ARG CPU_MODEL
# ENV CPU_MODEL=${CPU_MODEL}

ARG CPU_MODEL
# ENV CPU_MODEL=${CPU_MODEL}

ARG APP_USER
ARG APP_GROUP

# 必要なツールをインストール
RUN apt-get update && \
    apt-get install -y wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Serposcopeの.debパッケージをダウンロードしてインストール
RUN wget https://www.serposcope.com/downloads/${SERPOSCOPE_VERSION}/serposcope_${SERPOSCOPE_VERSION}_${CPU_MODEL}.deb -O serposcope.deb && \
    dpkg -i serposcope.deb && \
    rm serposcope.deb

COPY serposcope/application.conf /usr/share/serposcope/application.conf
COPY serposcope/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

WORKDIR /usr/share/serposcope/

# serposcope ユーザーとグループを作成
RUN groupadd -r ${APP_USER} && \
    useradd -r -g ${APP_USER} ${APP_GROUP}

# 必要なディレクトリを作成し、所有者を設定
RUN mkdir -p /usr/share/serposcope/database && \
    chown -R ${APP_USER}:${APP_GROUP} /usr/share/serposcope/database

USER root

EXPOSE ${WEB_PORT}
