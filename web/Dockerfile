FROM nginx:1

LABEL org.opencontainers.image.description="Mainsail nginx image with upstream and webcam configs"

RUN addgroup --gid 1000 mainsail
RUN useradd -rm -d /home/mainsail -u 1000 -g 1000 mainsail

COPY nginx/common_vars.conf /etc/nginx/conf.d/common_vars.conf
COPY nginx/upstreams.conf /etc/nginx/conf.d/upstreams.conf
COPY nginx/mainsail.conf /etc/nginx/conf.d/default.conf

RUN apt-get update \
    && apt-get install -y unzip wget sudo git

RUN echo "mainsail ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY start-web /bin/start-web
RUN chmod +x /bin/start-web

EXPOSE 80

ENTRYPOINT ["/bin/start-web"]
