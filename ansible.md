app.yml

---
- hosts: ansible

  tasks:
  - name: create docker image
    command: docker build -t application .

  - name: move image to dockerhub
    command: docker tag application trainerforaws/application

  - name: docker push
    command: docker push trainerforaws/application


deploy.yml

[ansadmin@ansible-server ~]$ vi deploy.yml
---
- hosts: docker

  tasks:
  - name: Stop container
    command: docker stop applicationcont

  - name: remove container
    command: docker rm applicationcont

  - name: create a container
    command: docker run -d --name applicationcont -p 7070:8080 trainerforaws/application
~
