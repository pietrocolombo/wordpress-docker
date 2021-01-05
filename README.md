# How to run a wordpress on docker, with phpMyAdmin, SSL (via Traefik) and automatic updates

* Docker, a powerful and standardized way to deploy applications
* Free SSL certificates from Let’s Encrypt (via Traefik)
* phpMyAdmin to easily manage your databases
* Automatic container updates (via Watchtower)

For a VM ypu can use google cloud with the standard free VM but you have only 600 MB of ram, one share core, 30Gb.
I personaly raccomend to use Oracle Cloud because you have 1 GB of ram, 2 core, 50 GB

In any case i racomend to add a swapfile
``` bash
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

and you have to add this (/swapfile none swap sw 0 0) here:
``` bash
sudo nano /etc/fstab
```

Install Docker (https://get.docker.com)

You have to assigne permissions:
``` bash
sudo usermod -aG docker your_user
```

Install Docker compose (https://docs.docker.com/compose/install/)

Clone this repository

Create acme.json file
``` bash
touch acme.json
chmod 0600 acme.json 
```

Now you have to edit **.env** file and add all information (BASIC_AUTH, ACME_EMAIL, TRAEFIK_DOMAINS, WORDPRESS_DOMAINS, WORDPRESS_DB_ROOT_PASSWORD, WORDPRESS_DB_PASSWORD).

for the domain part:
https://www.youtube.com/watch?v=y0VgnNbCneU&t=191s

if you use oracle cloud you have to open the port 443 and 80 (https://oracle-base.com/articles/vm/oracle-cloud-infrastructure-oci-amend-firewall-rules)

to run:
``` bash
docker-compose up -d
```



All site file are here:
/var/lib/docker/volumes/

To fix the issue requiring ftp access for plug-in installation
``` bash
sudo chown -R www-data  /var/lib/docker/volumes/thismac_vol-wp-content/
```

for the docker part I used this guide modifying it a bit:
https://docs.bytemark.co.uk/article/wordpress-on-docker-with-phpmyadmin-ssl-via-traefik-and-automatic-updates/#manage-your-containers

for the part about the Google VM:
https://www.youtube.com/watch?v=5YkkqjwRqN4
