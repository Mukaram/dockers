FROM mukaram/stormbase:0.9.2
MAINTAINER Mukaram Aziz<mukaram.aziz@verizon.com>

RUN sh /usr/bin/config-supervisord.sh ui

EXPOSE 8080
CMD sh /usr/bin/start-supervisor.sh