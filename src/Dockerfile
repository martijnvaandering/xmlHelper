FROM nginx:1.23.3
ARG DEBIAN_FRONTEND=noninteractive
RUN mkdir /usr/share/cgi
COPY serve.sh /usr/share/cgi/
COPY default.conf /etc/nginx/conf.d/default.conf
COPY init.sh /
COPY favicon.ico /usr/share/static/
RUN apt-get update && apt-get install -yq fcgiwrap jq python3 pip
RUN pip install yq
RUN xq --version
RUN chmod +x /usr/share/cgi/serve.sh 
RUN chown www-data:www-data /usr/share/cgi/serve.sh
RUN chmod +x /init.sh
RUN apt-get clean autoclean && apt-get autoremove --yes && rm -rf /var/lib/{apt,dpkg,cache,log}/
COPY index.html /usr/share/static/
ENTRYPOINT ["/bin/bash", "-c", "/init.sh"]