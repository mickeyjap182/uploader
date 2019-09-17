FROM centos:centos7

LABEL org.label-schema.schema-version="1.0" \
    org.label-schema.name="CentOS Base Image" \
    org.label-schema.vendor="CentOS" \
    org.label-schema.license="GPLv2" \
    org.label-schema.build-date="20181204"
#
## install util
RUN yum -y update \
 && yum -y install \
    epel-release gcc make bash git wget vim which openssl-devel bzip2-devel libffi-devel \
 && yum clean all

# https://www.python.jp/install/centos/index.html
RUN yum install -y https://centos7.iuscommunity.org/ius-release.rpm
RUN wget -O /usr/local/src/Python-3.7.4.tgz https://www.python.org/ftp/python/3.7.4/Python-3.7.4.tgz

WORKDIR /usr/local/src
RUN tar xzf Python-3.7.4.tgz
WORKDIR  /usr/local/src/Python-3.7.4
RUN mkdir -p /usr/local/Python3.7/Python-3.7.4
RUN ln -s /usr/local/Python3.7/Python-3.7.4 /usr/local/Python3.7/latest
RUN ln -s /usr/local/Python3.7/latest /usr/local/Python3.7/default
RUN ./configure --enable-optimizations --prefix=/usr/local/Python3.7/default
RUN make -j4
RUN make altinstall
RUN rm -f /usr/local/src/Python-3.7.4.tgz
RUN echo "export PATH="/usr/local/Python3.7/default/bin:$PATH"" >> /etc/profile
RUN ln -s /usr/local/Python3.7/default/bin/pip3.7 /usr/local/Python3.7/default/bin/pip

# locale & timezone
RUN yum clean all && yum reinstall -y glibc-common
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
# RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8 \
# && echo 'ZONE="Asia/Tokyo"' > /etc/sysconfig/clock \
# && ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
# && echo 'KEYMAP="jp106"' > /etc/vconsole.conf
#
# # setting
# RUN echo 'alias ll="ls -laF --color=auto"' >> /root/.bashrc \
# && echo 'export PS1="[\u@\h \w]\$ "' >> /root/.bashrc \
# && echo 'alias python=python3.7' >> ~/.bashrc \
# && echo 'alias pip=pip3' >> ~/.bashrc

# RUN yum install -y mysql_config epel-release nginx

# ENV
ENV PYTHONUNBUFFERED 1

# COPY analyze_service /var/www/analyze_service/
# RUN pip install -r /var/www/analyze_service/requirements.txt

# sync directory
# RUN mkdir /app
# WORKDIR /app
# COPY ./app /app

# RUN touch /var/run/nginx.pid && \
#   chown -R nginx:nginx /var/run/nginx.pid
  # chown -R nginx:nginx /var/cache/nginx

# RUN adduser -D user -g users -p test
# USER nginx
EXPOSE 80
# ENTRYPOINT ["nginx", "-g", "daemon off;"]
# CMD ["/bin/bash"]
