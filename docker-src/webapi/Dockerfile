FROM ubuntu:16.04


RUN apt update && apt -y full-upgrade
RUN apt -y install netcat \
    && apt -y install curl \
    && apt -y install openjdk-8-jdk-headless \
    && apt -y install postgresql-client-9.5 \
    && apt -y autoremove \
    && apt -y autoclean

COPY sources/configs/local_settings.properties /root/
RUN mkdir -p /opt/metasfresh-webui-api/metasfresh-webui-api \
    && mkdir -p /opt/metasfresh-webui-api/log
RUN curl https://repo.metasfresh.com/service/local/repositories/mvn-release/content/de/metas/ui/web/metasfresh-webui-api/2.88/metasfresh-webui-api-2.88.jar \
    --output /opt/metasfresh-webui-api/metasfresh-webui-api.jar \
    && chmod 750 /opt/metasfresh-webui-api/metasfresh-webui-api.jar

COPY sources/configs/* /opt/metasfresh-webui-api/
COPY sources/start_webapi.sh /opt/metasfresh-webui-api/
RUN chmod 700 /opt/metasfresh-webui-api/start_webapi.sh

ENTRYPOINT ["/opt/metasfresh-webui-api/start_webapi.sh"]
