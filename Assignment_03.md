## Ansile Assignment-3

Setup Spring3HibernateApp (https://github.com/opstree/spring3hibernate) on created infra using ansible playbook by following the below steps:

Install MySQL
Install JDK 11
Install Tomcat

        - name: Install Multiple Packages in Ubuntu Server
      apt: 
        update_cache: yes
        name:
          - mysql-server
          - openjdk-11-jdk
          - tomcat9
          - maven
        state: present

![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/9a040258-9b2c-4bf0-a4ea-5272a87faa01)


Create the war file for Spring3HibernateApp using maven

          vars:
            mvn_command:
                - mvn clean 
                - mvn dependency:resolve
                - mvn compile
                - mvn test
                - mvn package
                - mvn install
                 
        - name: Clone repository
          git:
            repo: https://github.com/opstree/spring3hibernate
            dest: /home/harshit/spring3hibernate
        
        - name: Generate war  file
          command: 
            chdir: /home/harshit/spring3hibernate
            cmd: "{{ item }}"
          with_items: "{{ mvn_command }}"


  ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/b89a3f69-b9ba-42ca-bc82-689d8affc1a8)

      





Send the war file created earlier to path "/opt/tomcat/apache-tomcat-7.0.108/webapps/"

Restart tomcat service

(edited)

opstree/spring3hibernate

A java loaded application for various testing purpose

Website

https://opstree.github.io
