### ANSIBLE ASSIGNMENT-1

#### UserManager:

Create a group:
   
      ansible server1 -m group -a "name=team1"

   ![Screenshot from 2023-10-09 22-56-48](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/dbfea3b0-74f0-40e8-b89c-2387e4f5e903)


Add the user Nitish to the team1 group and create the home directory:

      ansible server1 -m user -a "name=Nitish group=team1 createhome=yes"

   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/4dcbc9a9-af8c-464d-8176-bc8526efb57e)

Ensure the user Nitish has read, write, and execute access to the home directory:

      ansible server1 -m file -a "path=/home/Nitish owner=Nitish group=team1 mode=0755"

   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/b90e75f4-a00f-442f-a4f5-d5db507c34d8)

Ensure that all users of the same team have read and execute access to the home directory of fellow team members:

   - For the 'team' directory

         ansible server1 -m file -a "path=/home/Nitish/team owner=Nitish group=team1 mode=0770 state=directory"

      ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/baa9f56c-3fe0-4505-a53b-351d1d4307a3)

   - For the 'ninja' directory

         ansible server1 -m file -a "path=/home/Nitish/ninja owner=Nitish group=team1 mode=0777 state=directory"

      ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/985257a1-7ac4-4390-94aa-9bf7567738e6)


#### Additional Features:

Change user Shell -

      ansible server1 -m user -a "name=Nitish shell=/bin/bash" -b

   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/c3d5f7b2-b33a-4d7f-88ab-ebfd25edd8e5)

Change user password -

    ansible server1 -m user -a "name=Nitish password='{{ '12345' | password_hash('sha512') }}'" -b
    
   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/158c3e97-f1c4-462c-9b31-befd2fb1b5e1)

Delete user -

    ansible server1 -m user -a "name=Nitish state=absent remove=true " -b

   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/63089b8e-748e-4bc3-98dd-6b183ba4039b)

Delete Group - 

    ansible server1 -m group -a "name=team1 state=absent " -b

   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/2d42d375-e2c0-4863-b47e-89090d61431e)

List user or Team - 

    ansible server1 -m shell -a "getent group"

   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/a9205443-b57b-468e-8b50-fcde7cb31e2d)

    ansible server1 -m shell -a "getent passwd"
   
   ![image](https://github.com/HarshitSingh-Codes/Ansible_Practice/assets/67234531/9dfd18d3-bb1e-4917-85d9-65772e2df224)
