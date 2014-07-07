FROM mukaram/stormbase:0.9.2
MAINTAINER Mukaram Aziz<mukaram.aziz@verizon.com>

EXPOSE 6700
EXPOSE 6701
EXPOSE 6702
EXPOSE 6703
EXPOSE 8000

RUN sh /usr/bin/config-supervisord.sh supervisor
RUN sh /usr/bin/config-supervisord.sh logviewer
CMD sh /usr/bin/start-supervisor.sh