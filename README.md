# docker-sagashi
Will update some notices and integrate them into dockerfile


##### sagashi means exploring.......


##### A. About Docker Volume:
There are two methods to use docker volume ,  mac os demo:<br>
 1. docker run -it --name test -v ~/temp:/data ubuntu /bin/bash <br>
 2. in Dockerfile use VOLUME command , such as VOLUME ["/data" , "/var/lib/postgresql", "/home/app"] 

The diff between 1 and 2:<br>
 1.I can specify a directory to become a volume directory in the host machine with the first method.<br>
 2.If we not use -v flag to start container, in the first menthod we can't get data mount effection. But when we write VOLUME into Dockerfile, and start conainer without -v flag ,we still have destination url records that can use docker container_id inspect command to checkout.<br>

##### B. About Docker -p -P EXPOSE:
1. EXPOSE is Dockerfile command , such as EXPOSE 5432 ,it's a official and standard to stuff your Dockerfile ,but just a expression or statement in the Dockerfile, you need use -P to expose 5432 port real.
2. -P ,when you need to use with "EXPOSE" command docker imgea or use some official docker images. such as docker run -it -P --name pg postgresql:9.6  .Then you host xxx port already connect to the docker container 5432 port.
3. -p , using at docker runtime. such as: docker run -it -p 127.0.0.1:3000:3000 rails:latest . manually set host port and container port.
##### C. About ADD and VOLUNE:
1.What is ADD ? ADD means I can add whatever ,it can be a file or floder, add into docker image!<br>
<br>
When I use ADD command ? a. requeirement list file such as: ADD ./gemlist.txt /gemlist.txt  and need use it in the docker build-time...that mean next step is RUN pip intstall /gemlist.txt    b.use my app code and make app to be a work directory and do smoe commands, such as: ADD ./ usr/local/home/app  WORKDIR /usr/local/home/app  CMD python utils/say_hi.py <br>

2.What is VOLUNE ? VOLUNE means you can mount directory, you can have a access to paths on local host machine.But cann't use VOLUME files in the build-time, not access at build-time but will be accessible at rum-time.<br>

When I use VOLUME command ? a.when docker container is running and makes logs in var/log/app .I need logs can be accessible on the machine, and is saved there when container is removed. such as: VOLUME /var/log/app and then docker run -v /host/log/dir/app:/var/log/app/ image.    b.some diff env config file or secret file in local need setting into container. such as: VOLUME /etc/settings/setting  and docker run -v /host/settings/dir/setting:/etc/settings/setting image.
##### D. About FATAL: Listen error: unable to monitor directories for changes.
1.The answer : *https://github.com/guard/listen/wiki/Increasing-the-amount-of-inotify-watchers for info on how to fix this.*
2.on bash: `echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc/sysctl.conf && sudo sysctl -p`

##### E. About CMD and ENTRYPOINT
1. they can both in the Dockerfile, such as: FROM xxxx  ENTRYPOINT ["/bin/ping"] CMD ["localhost"]
2. only last ENTRYPOINT and CMD can work in Dockerfile.
3. The ENTRYPOINT specifies a command that will always be executed when the container starts. The CMD specifies arguments that will be fed to the ENTRYPOINT. such as:" FROM xxxx  ENTRYPOINT ["/bin/ping"] CMD ["localhost"] "and "docker run -it myimage " it will show PING localhost xxxxxxxx.
##### F. About "dev" directory in Dockerfile ,cann't be find in MAC docker.... 
1. when I use COPY dev/bla/bla var/bla/bla ,it will show docker container path...
2. docker cp command not work with /dev ,/sys/ ,/proc directory.
