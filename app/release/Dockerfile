FROM centos:7

ARG APP_NAME=kubejencdp-ui
ARG APP_BASE_DIR=/var/www/html
ARG API_ENDPOINT=http://127.0.0.1:8000
ENV APP_BASE_DIR $APP_BASE_DIR
ENV APP_NAME ${APP_NAME}
ENV API_ENDPOINT ${API_ENDPOINT}

RUN yum install -y httpd httpd-tools

COPY files/httpd/httpd.conf /etc/httpd/conf/
COPY files/httpd/default-site.conf /etc/httpd/conf.d/default-site.conf
COPY ./dist/ $APP_BASE_DIR/
COPY files/entrypoint.sh $APP_BASE_DIR/
#RUN  chown -R www-data:www-data $APP_BASE_DIR/ && \
RUN     chmod -R 0775 $APP_BASE_DIR

EXPOSE 8080
WORKDIR $APP_BASE_DIR
#USER www-data
ENTRYPOINT ["./entrypoint.sh"]
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
