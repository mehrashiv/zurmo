FROM ubuntu:16.04

RUN apt-get update -y && apt-get install -y  memcached


EXPOSE 11211

CMD ["/usr/bin/memcached", "-u", "memcache", "-v"]
