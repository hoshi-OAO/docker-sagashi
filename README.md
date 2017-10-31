# docker-sagashi
Will update some notices and integrate them into dockerfile


##### sagashi means exploring.......


###### A. About Docker Volume:
There are two methods to use docker volume ,  mac os demo:<br>
 1. docker run -it --name test -v ~/temp:/data ubuntu /bin/bash <br>
 2. in Dockerfile use VOLUME command , such as VOLUME ["/data" , "/var/lib/postgresql"] 

The diff between 1 and 2:<br>
 1.I can specify a directory to become a volume directory in the host machine with the first method.

###### B. About Docker -p -P EXPOSE:
1. EXPOSE is Dockerfile command , such as EXPOSE 5432 ,it's a official and standard to stuff your Dockerfile ,but just a expression or statement in the Dockerfile, you need use -P to expose 5432 port real.
2. -P
