# The MIT License
# SPDX short identifier: MIT
# Copyright 2018 Amit Thakur - amitthk - <e.amitthakur@gmail.com>
# Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
# The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
FROM centos/nodejs-8-centos7

ARG APP_NAME=kubejencdp-ui
ARG APP_BASE_DIR=/var/www/html
ARG APP_BUILD_DIR=/opt/app-root/src/
ARG API_ENDPOINT=http://127.0.0.1:8000
ENV APP_BASE_DIR $APP_BASE_DIR
ENV APP_NAME ${APP_NAME}
ENV API_ENDPOINT ${API_ENDPOINT}
ENV LD_LIBRARY_PATH /opt/rh/rh-nodejs8/root/usr/lib64
ENV PATH /opt/rh/rh-nodejs8/root/usr/bin:/opt/app-root/src/node_modules/.bin/:/opt/app-root/src/.npm-global/bin/:/opt/app-root/src/bin:/opt/app-root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV NPM_CONFIG_PREFIX /opt/app-root/src/.npm-global

EXPOSE 8080

USER root

COPY files ${APP_BASE_DIR}/files


#RUN cp ${APP_BASE_DIR}/files/pyfln.rep /etc/yum.repos.d/ \
#    && update-ca-trust force-enable

RUN yum install -y httpd httpd-tools

RUN cp ${APP_BASE_DIR}/files/npm/npmrc ~/.npmrc \
    && cp ${APP_BASE_DIR}/files/httpd/httpd.conf /etc/httpd/conf/ \
    && cp ${APP_BASE_DIR}/files/httpd/default-site.conf /etc/httpd/conf.d/default-site.conf \
    && chown apache:apache /etc/httpd/conf/httpd.conf \
    && chmod 755 /etc/httpd/conf/httpd.conf \
    && chown -R apache:apache /etc/httpd/conf.d \
    && chmod -R 755 /etc/httpd/conf.d \
    && touch /etc/httpd/logs/error_log /etc/httpd/logs/access_log \
    && chmod -R 766 /etc/httpd/logs \
    && chown -R apache:apache /etc/httpd/logs \
    && chown -R apache:apache /var/log/httpd \
    && chmod -R g+rwX /var/log/httpd \
    && chown -R apache:apache /var/run/httpd \
    && chmod -R g+rwX /var/log/httpd


COPY dist/. ${APP_BASE_DIR}

RUN cd $APP_BASE_DIR/ \
    && cp ${APP_BASE_DIR}/files/entrypoint.sh ${APP_BASE_DIR}/ \
    && chmod -R 0775 $APP_BASE_DIR/ \
    && chown -R apache:apache $APP_BASE_DIR/

WORKDIR $APP_BASE_DIR
USER apache
ENTRYPOINT ["./entrypoint.sh"]
CMD ["/usr/sbin/httpd","-f","/etc/httpd/conf/httpd.conf","-D","FOREGROUND"]
