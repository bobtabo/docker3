FROM nginx:1.19
# RUN rm /etc/nginx/conf.d/default.conf

ARG APP_NAME
ENV APP_NAME = $APP_NAME

# ユーザーを作成
ARG DOCKER_UID=1000
ARG DOCKER_USER=docker
ARG DOCKER_PASSWORD=docker
    RUN useradd -m --uid ${DOCKER_UID} --groups sudo ${DOCKER_USER} \
    && echo ${DOCKER_USER}:${DOCKER_PASSWORD} | chpasswd \
    && echo "docker    ALL=(ALL)       ALL" >> /etc/sudoers

# 設定の置換
# COPY templates/default.conf.template /etc/nginx/conf.d/default.conf
# COPY /etc/nginx/templates/default.conf.template /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/nginx.conf
# RUN envsubst /etc/nginx/templates/default.conf.template > /etc/nginx/conf.d/default.conf
RUN envsubst templates/default.conf.template > /etc/nginx/conf.d/default.conf

RUN chgrp -R docker /var/cache/nginx /var/run /var/log/nginx && \
    chmod -R 770 /var/cache/nginx /var/run /var/log/nginx

CMD ["nginx", "-g", "daemon off;"]
