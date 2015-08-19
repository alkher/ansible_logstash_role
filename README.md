LOGSTASH
========

Instalación y configuración de [logstash](https://www.elastic.co/products/logstash).

Basado en el trabajo de [Larry Smith Jr.](http://everythingshouldbevirtual.com/).

Requisitos
==========

Sistemas operativos soportados:

- CentOS 7 

Variables
=========

	---
    # defaults file for logstash
    # LOGSTASH
    ls_version: 1.5 # Versión de logstash
    ls_fqdn: localhost # IP, FQDN o localhost (servidor donde se instala redis)
    ls_folder: /opt/logstash # Directorio para la instalación
    ls_config_dir: /etc/logstash/conf.d # Directorio con los ficheros de configuración
    ls_log_dir: /var/log/logstash # Directorio con los logs
    config_ls: true # Verdadero si se desea configurar logstash (por defecto false)
    ls_workers: 2  # Número de procesos para repartir entre las CPU (por defecto es 1/CPU) [2 vCPU]
    # ELASTICSEARCH
    es_cluster_name: ELK # Nombre del cluster de elasticsearch
    es_fqdn: elk # VIP del cluster de elasticsearch
    # CONFIGURACIÓN BASE
    ls_configs:
    - 000_inputs
    - 001_filters
    - 999_outputs
    # GROK PATTERNS
    ls_grok_patterns:
    - IPTABLES # Pattern para IPTables
    - NGINXERROR # Pattern para nginx
    # PLUGINS
    ls_plugins:
    - logstash-filter-elasticsearch # Filtro elasticsearch
    - logstash-filter-json_encode # Filtro Json Encode
    - logstash-filter-translate # Filtro translate
    - logstash-filter-zeromq # Filtro ZeroMQ

Dependencias
============

Es necesario tener [JAVA](http://java.com/es/about/whatis_java.jsp) instalado:

	- { role: alkher.java, jdk_java: open }

Ejemplo de playbook
===================

    - hosts: servers
      roles:
         - { role: alkher.elasticsearch }

Licencia
========

BSD

Autor
=====

Andoni Alcalde
- @alkher
- http://zenway.es
- alcher [at] zenway [dot] es