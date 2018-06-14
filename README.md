# Collaboration-System-Event-Logs

<p>
Event logging module is a part of the Collaboration system. This module deals with the logging of the user interaction events, such as view an article.
This module works as a middleware in Django project and captures and filters the request based on the specification. The logs will be stored in elasticsearch using logstash.
</p>

## Setting up ELK Stack with docker

1. Place elasticsearch, logstash, kibana folders of evelog-Docker in the Collaboration-System repository.

2. Replace the docker-compose.yml file of Collaboration-System repository with the evelog-Docker's docker-compose.yml.

## Installing Search API

1. Install the python client for Elasticsearch using the following pip command:
	``` pip install elasticsearch ```
2. Copy the `search_api` folder into the root of the main Django project.
3. In the main project's `settings.py` file, add the `'search_api'` in the Installed Apps list -
```python
INSTALLED_APPS = [
    ...,
    'search_api'
]
```
4. Also add the following line in the main project's `urls.py` file:
```python
urlpatterns = [
    ...,
    url(r'^logapi/', include('search_api.urls'))
]
```
5. To install the elasticsearchclient add the following in the requirements.text of Collaboration-System Repository
```
    ...,
    elasticsearch
```
6. In the `search_api/settings.py`, add the elasticsearch hosts in SERVER_CONF 
```python
   ...,
   SERVER_CONF = [ "elasticsearch" ]
```
7. Use the URLs to get the required data
