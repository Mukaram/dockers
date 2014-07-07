FROM mukaram/stormbase:0.9.2
MAINTAINER Mukaram Aziz<mukaram.aziz@verizon.com>

RUN sh /usr/bin/config-supervisord.sh nimbus 
RUN sh /usr/bin/config-supervisord.sh drpc

EXPOSE 6627
EXPOSE 3772
EXPOSE 3773
ADD start-nimbus-supervisord.sh /usr/bin/start-nimbus-supervisord.sh
CMD sh /usr/bin/start-nimbus-supervisord.sh