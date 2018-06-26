# Collaboration-System-Event-Logs

<p>
Event logging module is a part of the Collaboration system. This module deals with the logging of the user interaction events, such as view an article.
This module works as a middleware in Django project and captures and filters the request based on the specification. The logs will be stored in elasticsearch using logstash.
</p>

## Setting up ELK Stack with docker

1. Place elasticsearch, logstash, kibana folders of evelog-Docker in the Collaboration-System repository.

2. Replace the docker-compose.yml file of Collaboration-System repository with the evelog-Docker's docker-compose.yml.

