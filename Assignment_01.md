ANSIBLE ASSIGNMENT-1

UserManager:

1. Create a group:
   
   ansible server1 -m group -a "name=team1"

2. Add the user Nitish to the team1 group and create the home directory:

   ansible server1 -m user -a "name=Nitish group=team1 createhome=yes"


3. Ensure the user Nitish has read, write, and execute access to the home directory:

   ansible server1 -m file -a "path=/home/Nitish owner=Nitish group=team1 mode=0755"


4. Ensure that all users of the same team have read and execute access to the home directory of fellow team members:

   For the 'team' directory

   ansible server1 -m file -a "path=/home/Nitish/team owner=Nitish group=team1 mode=0770 state=directory"

   For the 'ninja' directory

   ansible server1 -m file -a "path=/home/Nitish/ninja owner=Nitish group=team1 mode=0777 state=directory"


These ad hoc commands perform the same tasks as the tasks defined in your Ansible playbook but are executed individually on the command line.

Additional Features:

Change user Shell -

    ansible server1 -m user -a "name=Nitish shell=/bin/bash" -b

Change user password -

    ansible server1 -m user -a "name=Nitish password='{{ '12345' | password_hash('sha512') }}'" -b

Delete user -

    ansible server1 -m user -a "name=Nitish state=absent remove=true " -b

Delete Group - 

    ansible server1 -m group -a "name=team1 state=absent " -b

List user or Team - 

    ansible server1 -m shell -a "getent group"
    
    ansible server1 -m shell -a "getent passwd"
