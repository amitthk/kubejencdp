# The MIT License
# SPDX short identifier: MIT
# Copyright 2018 Amit Thakur - amitthk - <e.amitthakur@gmail.com>
# Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
# The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
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
