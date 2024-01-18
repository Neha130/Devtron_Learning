**Docker Commands:**

docker pull name : it take a latest image
docker images :it shows the data of images that we use
docker ps : list of running containers
docker run -d im agename : create a new container
docker stop : stop a container
docker ps -a : list a stop and running container both

docker run -p6000: port number of that container : get a same port having different container
docker exec -it eecc0cb54792 /bin/bas : to get into a container
Docker logs : This command allows you to retrieve and view this output.
 docker rmi -f backend : for removing an image from the container
docker rm -f backend : for removing container


**Run a project using manual IPAddress giving as a path:**

Build mongodb image: docker build -t mongo .
Run mongodb: docker run -d -p 27017:27017 --name  dbase mongo
Check IP Address:  docker inspect dbase | grep -i ipaddress

For Backend(node.js File)
Build mongodb image: docker build -t backend .
Run mongodb: docker run -dit -p 5000:5000 --name  backend1 backend
Check IP Address:  docker inspect backend1 | grep -i ipaddress

For Frontend(react file)
Build mongodb image: docker build -t frontend .
Run mongodb: docker run -dit -p 3000:3000 --name frontend1 frontend
Check IP Address:  docker inspect frontend1 | grep -i ipaddress

**Error : while using -it in backend then it throw an error that connection is timed out**
Solution: we use -d so that server is running in the background

**Error : while using -d in frontend then it throw an error that connection is timed out**
Solution: we use -dit so that server is interactively running 

Run a project using ENV to run directly passing the id into the command itself 

Build mongodb image: docker build -t mongo .
Run mongodb: docker run -d -p 27017:27017 --name  dbase mongo
Check IP Address:  docker inspect dbase | grep -i ipaddress

For Backend(node.js File)
Build mongodb image: docker build -t backend .
Run mongodb: docker run -dit -p 5000:5000 --name backend1 -e URL="mongodb://172.17.0.2:27017/test" backend
Check IP Address:  docker inspect backend1 | grep -i ipaddress

For Frontend(react file)
Build mongodb image: docker build -t frontend .
Run mongodb: docker run -dit -p 3000:3000 --name frontend1 -e URL="http://192.168.0.172:5000" frontend
Check IP Address:  docker inspect frontend1 | grep -i ipaddress

**Error : while using -it in backend then it throw an error that connection is timed out**
we try to  -d  but it run a server but not run for a longer time 
Solution: We use -dit so that server is running in the background

**Error : while using -d in frontend then it throw an error that connection is timed out**
Solution: we use -dit so that server is interactively running 

**Error: Db and backend server is running properly even hit an api in postman it works but while using the ui (frontend) then it give 404 error it occurs while we pass a env url in command!**
Solution: It doesnot support process.env directly in the react file. correct syntax is : process.env.REACT_API_URL(url is name)
In docker's file the name of the env variable is ENV REACT_API_URL =  and it's work

Docker Volume: It is used to get backup of a container

**Backup of a  container:**
Step 1: We have created a container that stores data in 'sample-volume'
Command in Example: docker run -d --name sample-container -v sample-volume:/data ubuntu
Step 2: Now, we will create a backup file 'sample-backup' of 'sample-volume' at the path of our choice on the host system by starting a temporary container and removing it using the 'rm' option once the backup is created. We created the 'sample-backup' at 'C:\Users\my-username]\Documents'

Cvaf : creating a tar file
Command in Example:
docker run --rm --volumes-from sample-container -v C:\Users\\*my-username*\]\Documents:/backup-dir ubuntu tar cvzf /backup-dir/sample-backup.tar.gz /data

**Steps to restore a Docker volume**

Step 1: We have created a temporary container to mount the volume and backup file(i.e., 'sample-backup') and then extract the backup content into the volume(i.e., 'restored-volume'.
Command in Example: docker run --rm -v sample-volume:/data -v C:\Users\\username\]\Documents:/backup-dir ubuntu tar xvzf /backup-dir/sample-backup.tar.gz -C /data

Note: It is important to note that while restoring the volume, it should not be in use by any container.


Tmpfs (temporary file system) Mount is a special type of mount that allows you to create a temporary file system in memory.

**Multi Staging:**
A multistage build allows you to use multiple images to build a final product.
It reduce the size of image
First we create a dockerfile then build it 
In first docker file we just use to generate a zar file 
In second docker file we just use run that file taking a reference from the first docker file
(FROM alpine
COPY - - from = builder //source…..
EXPOSE…..
ENTRYPOINT[......]) then build it.

Creating a Docker volume : docker  volume create
Docker  volume create  - - name sample-volume –driver local
Inspect docker volume :  docker volume inspect sample-volume
Removing docker volume: docker volume rm sample-volume
Listing of container : docker volume ls
Remove all unused file : docker volume prune // it remove the container that is not in use locally



Container registry  it just like docker hub

Inbound: there are always restrictions on inbound traffic. Everybody cares about incoming traffic and protects their network.

Outbound: there are no restrictions on outbound traffic. It means that containers can communicate easily with the outside world (or the internet). 









