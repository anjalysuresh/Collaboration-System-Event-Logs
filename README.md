# Collaboration-System-Event-Logs

<p>
Event logging module is a part of the Collaboration system. This module deals with the logging of the user interaction events, such as view an article.
This module works as a middleware in Django project and captures and filters the request based on the specification. The logs will be stored in elasticsearch using logstash.
</p>

## Setting up ELK Stack with docker

1. Clone the collaboration-Communities Repository by typing following command and follow the instructions to install the system.
```bash
$ git clone https://github.com/fresearchgroup/Collaboration-System.git

```

2. Add/replace the following lines in `.env` file to add user and password for Event API Authorization
	```bash
		EVENTAPI_TOKEN_USER=<name-of-user>
		EVENTAPI_TOKEN_PASS=<password>

	```

3. __Generating a new Token__. To generate a new Token type the following command
	```bash
		$ python3 manage.py generateToken --n
	```
	i. Use --r flag instead of --n for renewing the flag
	ii. Use --g flag to get value for the current User

4. Copy the value of the token and paste in `.env` file
	```bash
		EVENT_API_TOKEN=<token-generated>

	```

5. In `.env` change the value of `LOG_TYPE` to ip address of `logstash`(see step 11 to know how to get the address of logstash).

6. In `.env` change the value of `LOG_PORT` to port on which `logstash` is running.

7. In `.env` change the value of `ELASTICSEARCH_ADDRESS` to ip address of `elasticsearch`(see step 11 to know how to get the address of elasticsearch).

8. Run the server using the following command
	```bash
		$ python3 manage.py runserver
	```
9. __Running ELK Stack in docker__. change to evelog-Docker folder using the following command
	```bash
		$ cd evelog-Docker	
	```

10. Run the following command to build and start docker
	```bash
		$ docker-compose build
		$ docker-compose up
	```
11. __Getting the ip address of logstash and elasticsearch(When running on same pc).__ Open a new terminal window and type the following command to get the name of logstash and elasticsearch container
	```bash
		$ sudo docker ps
	```

12. Once you get the name of container run the following command to inspect the docker container
	```bash
		$ sudo docker inspect <container-name>
	```

13. There is a field mentioning the ip address of container. Copy it to the desired location.

14. __Getting the ip address of ELK(when running on different machines).__ For different machines use the ip address of machine on which docker is running.
