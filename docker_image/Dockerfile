# Dockerfile for ShadowsocksR
# https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh
# gost: https://github.com/Mr-LongFly/gost/raw/master/gost.sh && bash gost.sh

FROM ubuntu

LABEL maintainer="Long Fei <31891692@qq.com>"

# prepare
RUN apt-get update \
  && apt-get install -y procps wget psmisc \
  && rm -rf /var/lib/apt/lists/* \
  && export PATH=$PATH:/usr/local/bin:/usr/bin:/bin:/sbin:/usr/local/games:/usr/games \
# install gost
  && wget --no-check-certificate https://github.com/Mr-LongFly/gost/raw/master/gost.sh \
  && chmod 777 gost.sh \
  && export TERM=$TERM \
  && bash gost.sh \
  && exit 0
# install ssr
RUN mkdir /usr/local/ssr \
  && cd /usr/local/ssr \
  && wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR.sh \
  && chmod +x shadowsocksR.sh \
  && export TERM=$TERM \
  && bash shadowsocksR.sh 2>&1 | tee shadowsocksR.log \
  && rm -rf shadowsocksR.sh \
  && exit 0 \
# ssr script
# fake log
  && touch fake_log.log \
# start.sh
  && touch start.sh \
  && echo 'python /usr/local/shadowsocks/server.py -c /etc/shadowsocks.json -d start && tail -f /usr/local/ssr/fake_log.log' > start.sh \
  && chmod 775 start.sh \
# stop.sh
  && touch stop.sh \
  && echo 'python /usr/local/shadowsocks/server.py -c /etc/shadowsocks.json -d stop' > stop.sh \
  && chmod 775 stop.sh \
# restart.sh
  && touch restart.sh \
  && echo './stop.sh && ./start.sh' > restart.sh \
  && chmod 775 restart.sh \
# ssr configuration
  && COPY shadowsocks.json /etc/ \
  && COPY gost.json /usr/local/gost/

ENTRYPOINT ["sh", "/usr/local/ssr/start.sh", "gost start"]
