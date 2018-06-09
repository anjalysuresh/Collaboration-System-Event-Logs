# Collaboration-System-Event-Logs

<p>
Event logging module is a part of the Collaboration system. This module deals with the logging of the user interaction events, such as view an article.
This module works as a middleware in Django project and captures and filters the request based on the specification. The logs will be stored in elasticsearch using logstash.
</p>

## Setup

<p>To setup this module with the Collaboration system, perform the following steps:</p>
1. Copy the `eventlog` folder into the root of the main Django project.
2. Go to project's `settings.py` file and in the set of the middlewares add following line:

```python
MIDDLE_WARE = [
    ...,
    'evenlog.middleware.Middleware'
]
```

And, thats all, you are done!

## Setting up ELK Stack with docker

1. Place elasticsearch, logstash, kibana folders of evelog-Docker in the Collaboration-System repository.

2. Replace the docker-compose.yml file of Collaboration-System repository with the evelog-Docker's docker-compose.yml.

3. Go to `eventlog/main/settings.py` and change address and port as follows:
```python
SERVER_CONF = {
		...,
		"address": "logstash",
                "port": 5000,
		...,
}
```
4. Run the following commands inside the Collaboration-System repository:
```
   docker-compose build
   docker-compose up
```

### Configuring the proxy

1. To setup proxy go to `eventlog/main/settings.py` 
2. For `SERVER_CONF` set `'use_proxy' = True`.
3. Specify the proxy configuration as follows:
```python
SERVER_CONF = {
		...,

              "proxies": {
                    "http": "http://proxy.cse.iitb.ac.in:80",
                    "https": "https://proxy.cse.iitb.ac.in:80",
                    "ftp": "ftp://proxy.cse.iitb.ac.in:80",
              }
}
```
4. To add authentication for proxy add follwowing to `SERVER_CONF` else remove it:
```python
SERVER_CONF = {
		...,
		"proxy_auth": {
                         "username": "<your-proxy-authentication-name>",
                         "password": "<your-proxy-authentication-password>"
                }
	
}

```

##  Debugging and Logging

Debugging module is defined in utils.py and enables 5 levels of logging along with some color customizations for better viewing.

1. To enable debugging go to `eventlog/main/settings.py`.
2. Set `DEBUG = True`


## Installing Search API

1. Copy the `search_api` folder into the root of the main Django project.
2. In the main project's `settings.py` file, add the `'search_api'` in the Installed Apps list -
```python
INSTALLED_APPS = [
    ...,
    'search_api'
]
```
3. Also add the following line in the main project's `urls.py` file:
```python
urlpatterns = [
    ...,
    url(r'^logapi/', include('search_api.urls'))
]
```
4. In the `search_api/essearch.py`, set the host and the port on which elasticsearch is running
```python
class SearchElasticSearch:
    def __init__(self):
        ...
        self.es = Elasticsearch([{'host': '172.18.0.2', 'port': 9200}])
        ...
```
6. Use the URLs to get the required data