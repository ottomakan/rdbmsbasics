# Oracle Container Registry

Oracle Container Registry contains container images for popular Oracle software like Database (RDBMS), Java releases, Oracle Middleware, Oracle Blockchain and more. We are going to use it to download and run Oracle Database software using the Docker containerization solution. There are other container solutions as well. Besides Docker, Podman is another solution that is quite popular.

Go to [https://container-registry.oracle.com/ords/f?p=113:10:16097243703257](https://container-registry.oracle.com/ords/f?p=113:10:16097243703257):::::  
Click on the Database tile   
On the next page, click on [adb-free](https://container-registry.oracle.com/ords/f?p=113:4:16097243703257:::4:P4_REPOSITORY,AI_REPOSITORY,AI_REPOSITORY_NAME,P4_REPOSITORY_NAME,P4_EULA_ID,P4_BUSINESS_AREA_ID:2223,2223,Oracle%20Autonomous%20Database%20Free,Oracle%20Autonomous%20Database%20Free,1,0&cs=3Nm7sevqRvYc-vY7FpimhWkrfue8NL_pUgPDoD1vAdXr_OiZ0Qvfa7iTmMXzsi8yfv_v4hVhjJ80I3iMOYPCe6Q). This page has the instructions you need to set up Oracle RDBMS software under docker (or podman).

On this page you will see the version of Oracle RDBMS software as image names

| Database version | Latest image tag | Specific release image tag |
| ----- | ----- | ----- |
| 23ai | latest-23ai | 24.11.4.2-23ai |
| 19c | latest | 24.9.3.2 |

We will use the latest version of Oracle RDBMS image.

Remember, an image is used to create the container. Once the container is up, you technically no longer need the image unless you are going to create more containers from it or for some reason need to destroy and recreate the existing container.

Terms to know:  
ADB: Autonomous Database (just a name Oracle has come up for their Database for the Cloud, to differentiate with their legacy on-premise version).  
ATP: Autonomous database for Transaction Processing. Basically it is ADB with configuration settings for a transaction processing system.  
ADW: Autonomous Database for Data Warehouse purposes.

It makes no difference to us which ADB config (ATP or ADW) we use. This differentiation for now is just meant to be informational. 

Make sure Docker desktop is installed on your laptop. If not, you can use homebrew to install it.  
  `brew install --cask docker`

Now run the docker command to create the container from the image. Note, this command will pull the image from the oracle container registry first since the image is not locally available on your laptop.

`docker run -d \`  
  `-p 1521:1522 \`  
  `-p 1522:1522 \`  
  `-p 8443:8443 \`  
  `-p 27017:27017 \`  
  `-e WORKLOAD_TYPE='ADW' \`  
  `-e WALLET_PASSWORD='scottT!G3ress' \`  
  `-e ADMIN_PASSWORD='scottT!G3ress' \`  
  `--cap-add SYS_ADMIN \`  
  `--device /dev/fuse \`  
  `--name local-db \`  
  `-v /Users/vik/docker/binds/oracle/data/local-db:/u01/data \`  
  `container-registry.oracle.com/database/adb-free:latest-23ai`

You need to adjust the paths for your laptop.

