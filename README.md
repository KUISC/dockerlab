# Docker Lab

## Getting Started

1. Open vcenter.kuisc.com
2. Login
3. Click on VMs and Templates
4. Open Lawrence -> Security Club -> yourname-dockerlab
5. Right Click on yourname-dockerlab
6. Hover over Power
7. Click on Power On
8. Click on the Square that shows the current screen of the VM. Should be black with little white lines.
9. Once the VM is spun on click on the user Docker
10. Enter the password `workshop`
11. You should see the desktop screen
    - If you don't please let me know
12. On the left hand side of the sceen you should see a black rectangle with a >\_. Click that.
13. Once the terminal is open maximize it so you can see more of it.
14. Type `docker --version`
    - You should see `Docker version 18.06.1-ce, build e68fc7a`

## Images

1. Type `cd ~ && mkdir webserver && cd webserver`
2. Type `touch Dockerfile`
3. Type `sudo nano Dockerfile`
4. Inside this new document we will write the following. I'll explain what each line does as we go.

```
FROM ubuntu
RUN apt-get update
RUN apt-get install -y apache2
RUN apt-get install -y apache2-utils
RUN apt-get install -y nano
RUN apt-get clean
RUN mv /var/www/html/index.html /var/www/html/index.old
EXPOSE 80
CMD ["apache2ctl", "-D", "FOREGROUND"]
```

8. To exit type ctrl+x, y, then enter.
9. Type `sudo docker build -t="webserver" .`
10. After that completes type `docker image ls`
    - This shows all the images running.

## Containers

1. Now that the image is built we can create a container for it.
2. In the terminal run `sudo docker run -d -p 80:80 --name web webserver`
3. Type `docker ps`
   - This shows all the containers currently running.
4. Type `docker exec -it web /bin/bash`
5. Type `nano /var/www/html/index.html`
6. In that file type `<h1>Hello World</h1>`
7. Ctrl+x, y, enter
8. After that, open Firefox and go to 0.0.0.0:80 to see your hello world page.

## Cleaning up

1. Type `exit` in the terminal to exit the bash shell on the Docker container.
2. Type `sudo docker stop web && sudo docker rm web`
3. Type `sudo docker rmi -f webserver`
4. Type `sudo docker rmi -f ubuntu`

## Questions?
