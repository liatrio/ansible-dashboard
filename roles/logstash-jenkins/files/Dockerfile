FROM docker.elastic.co/logstash/logstash:6.5.4 

EXPOSE 9000

ADD --chown=logstash logstash.yml /usr/share/logstash/config/logstash.yml
ADD --chown=logstash jenkins.yml /usr/share/logstash/pipeline/jenkins.yml

