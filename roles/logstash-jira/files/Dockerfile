FROM docker.elastic.co/logstash/logstash:6.5.4 

USER root

RUN logstash-plugin install logstash-filter-prune
RUN yum install -y sudo git vim

USER logstash
ENV PATH=$PATH:/usr/share/logstash/vendor/jruby/bin/
RUN gem install bundler

ADD --chown=logstash logstash.yml /usr/share/logstash/config/logstash.yml
ADD --chown=logstash jira.yml /usr/share/logstash/pipeline/jira.yml
RUN git clone https://github.com/liatrio/logstash-input-jira /usr/share/logstash/plugins/logstash-input-jira

WORKDIR /usr/share/logstash/plugins/logstash-input-jira
RUN bundler install 
RUN gem build /usr/share/logstash/plugins/logstash-input-jira/logstash-input-jira.gemspec

WORKDIR /usr/share/logstash
RUN env
RUN logstash-plugin install /usr/share/logstash/plugins/logstash-input-jira/logstash-input-jira-*.gem

