ansible nginx-proxy
===================
[![Build Status](https://travis-ci.org/ypsman/ansible-nginx-proxy.svg?branch=master)](https://travis-ci.org/ypsman/ansible-nginx-proxy)

This Role configures Nginx as Proxy for a single Site.

Some default Options are set.

You can change the default Index.html, simple put youre index.html in

templates/index.html under youre Playbook.

and setup the Variable:

nginx_proxy_custom_index: index.html


Default options: <br>
      # default for nginx-proxy site Config <br>
      nginx_proxy_pass: http://localhost:8080                 # <br>
      nginx_proxy_server_name: "{{ ansible_hostname }}"       # name of the Site <br>
      nginx_proxy_conf_name: site.conf                        # name of the conf fife <br>
      nginx_proxy_location: /                                 # listen on uri <br>
      nginx_proxy_disable_default: true                       # disable default page <br>
      nginx_proxy_ssl_proxy: false                            # Use SSL <br>
      nginx_proxy_http_port: 80                               # port to listen on <br>
      nginx_proxy_https_port: 443                             # port to listen on for https <br>
      nginx_proxy_logdir: /var/log/nginx                      # Folder where to put the Logs in <br>

      # defaults file for nginx-proxy                         # some cache config <br>
      nginx_proxy_max_temp_file_size: 0   <br>
      nginx_proxy_connect_timeout: 90 <br>
      nginx_proxy_send_timeout: 90 <br>
      nginx_proxy_read_timeout: 90 <br>
      nginx_proxy_buffer_size: 4k <br>
      nginx_proxy_buffers: 8 32k <br>
      nginx_proxy_busy_buffers_size: 64k <br>
      nginx_proxy_temp_file_write_size: 64k <br>

      # nginx SSL Config <br>
      nginx_proxy_ssl_session_timeout:  5m                    # SSL Session Timeout <br>
      nginx_proxy_ssl_protocols: TLSv1 TLSv1.1 TLSv1.2        # TLS Versions <br>


Example Playbook
----------------

    # non SSL
    - hosts: all
      roles:
        - role: ypsman.nginx-proxy
          nginx_proxy_server_name: mysite.example.org         # Servername to listen on  
          nginx_proxy_pass: http://localhost:8080             # Site to proxy
          nginx_proxy_http_port: 1080                         # Example change of default port


    # SSL example
    - hosts: all
      roles:
        - role: ypsman.nginx-proxy
          nginx_proxy_ssl_proxy: true                         # Enable SSL
          nginx_proxy_ssl_cert: /etc/ssl/cert.crt             # Location ssl Cert File
          nginx_proxy_ssl_key: /etc/ssl/cert.key              # Location ssl key File
          nginx_proxy_server_name: mysite.example.org         # Servername to listen on  
          nginx_proxy_pass: http://localhost:8080             # Site to proxy
