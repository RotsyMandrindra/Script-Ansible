# Script-Ansible
Explication of how to make a script with Ansible


sudo apt-get install apache2
installation d'apache2 sur votre ordinateur

sudo apt install python-pip
installation de python sur votre ordinateur

 python3 --version
 voir si python est installé

 sudo pip install ansible
 installation d'ansible sur votre ordinateur
 
 ansible --version
 voir si ansible est installé
 
sudo touch /etc/apache2/sites-available/www.hei.school.conf
creer un fichier .conf qui hebergera notre script avec ansible

 nano www.hei.school.conf 
 editer le fichier le contenu sera un script
 
 voici le contenu de ce fichier
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/html

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

sudo ln -s /etc/apache2 ~/new.yml
creer un lien symbolique avec un nouveau fichier .yml ceci etant un fichier qui n'est pas encore creer c'est un fichierde configuration d'ansible qui hebergera ce script suivant


---
- name: Deploy hei server web with ansible
  hosts: web_servers
  become: true

  tasks:
    - name: hei server
      apt:
        name: hei server
        state: latest

    - name: hei server
      service:
        name: hei server
        state: started
        enabled: true
   
creer un fichier .ini, un inventaire Ansible pour spécifier les serveurs sur lesquels on souhaite déployer notre site web
server ansible_host = IP_du_server


Il faut se placer /chemin/vers/les/fichiers par le chemin local de notre site web que nous souhaitons.
En executant cette commande ci-dessous cela permettra de déployer notre site web sur un serveur spécifié dans l'inventaire. 
ansible-playbook -i inventory.ini deploy_website.yml
Pour l'execution de cette commande il faut se connectée entant que root

Voilà nous avons finit de deployer notre site web
