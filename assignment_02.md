## Ansible Assignment-2

### Install nginx in your servers(more then 2) and make sure the log files of nginx should not be granted more than 1 GB space on the nodes

- Install NGINX

      ansible tag_Name_ansible_02 -b -m apt -a "name=nginx state=present update_cache=yes"

  verify

      ansible tag_Name_ansible_02 -m command -a “nginx -v”

- limit the NGINX log file size by 1GB

      ansible tag_Name_ansible_02 -b -a "sed -i '3i\       size 1G' /etc/logrotate.d/nginx

  verify

      ansible tag_Name_ansible_02 -b -a "cat /etc/logrotate.d/nginx "

- configure NGINX

      ansible all -b -m shell -a "echo > /etc/nginx/sites-enabled/default"

  add new content

      ansible all -b -m shell -a "echo 'server {
      listen 80;
      server_name quadSquad.opstree.com;
      root /var/www/content;
      index index.html;
      location / {
        try_files \$uri \$uri/ =404;
      }
      }' >> /etc/nginx/sites-available/default"

- add team member's HTML page 

      ansible server2 -m copy -ba "src=/var/www/ dest=/var/www"

  verify
  
      ansible server2 -ba "ls /var/www/ "

- web rotation script

        #!/bin/bash
      
      # Define an array of website folder names
      websites=( "harshit" "samir" "vikram" "abhijeet" "rahul" )
      
      
      
      while true; do
          for website in "${websites[@]}"; do
      # create a soft link and change it to each website dir
              ln -sf "$website" content
              sleep 7200  # Sleep for 2 hours (7200 seconds)
              rm content
          done
      done

- Restart NGINX

      ansible server2 -m ansible.builtin.service -a "name=nginx state=restarted" -b



- run the script

      ansible server2 -m shell -a "bash /var/www/web_rotate.sh" -b


- Install Apache
  Also Configure nginx to run as reverse proxy to apache after completing first point individually.


- Run the ansible commands in such a way that workers nodes are updated one by one and not altogether and also make sure using all type of strategies.
