# authservice

auth.mayone.us

Please see https://github.com/MayOneUS/wiki/wiki/My-SuperPAC-design-doc

## Getting started

First, make sure the service is configured. You'll need to run

    cp config_NOCOMMIT_template config_NOCOMMIT.py

and then edit `config_NOCOMMIT.py` to contain some API keys and secrets.

This service must run over HTTPS on something that your computer's hostname
resolution thinks is `auth.mayone.us`. This is because we are using secure
cookies, which your browser requires pass over HTTPS for subdomains of
`mayone.us`.

The easiest way to get an HTTPS server running is to run

    docker pull jtolds/mayone-gae
    docker run -t -i -v /path/to/your/checkout:/develop jtolds/mayone-gae /start.sh /develop

(`start.sh` runs `dev_appserver.py` for you and sets up stunnel to wrap HTTPS
 traffic)

Run `docker ps` to find the container id of your running instance, then find
its IP address by running

    docker inspect -f "{{.NetworkSettings.IPAddress}}" container_id

Finally, add the container's IP and `auth.mayone.us` to your `/etc/hosts` file.
