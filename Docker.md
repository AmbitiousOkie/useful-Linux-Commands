# Installing Docker and a Docker Image

## Installing Docker

Docker can be installed as a GUI application or as a CLI application.
https://docs.docker.com/engine/install/ubuntu/
The two main flavors are:
* Docker Desktop
* Docker Engine

The Docker Desktop is easier to use, but Docker Engine is good to learn for the CLI commands that will be used on enterprise servers.  We will be using the Docker Engine through the CLI to help guide our way through the hard path.

### Docker Desktop
We'll be following these instructions:
https://docs.docker.com/desktop/setup/install/linux/
https://docs.docker.com/desktop/setup/install/linux/ubuntu/

1. Setup the APT repository for Docker as seen here: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository by running the following commands:
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
2. Download the latest DEB install package for Docker Desktop. https://desktop.docker.com/linux/main/amd64/docker-desktop-amd64.deb?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-linux-amd64
3. Update the APT repositories `sudo apt update`
4. Install the DEB file using `apt` by typing `sudo apt install ./docker-dkestop-amd64.deb`
5. Remember, hackers don't rely on GUIs.


### Docker Engine
We'll be following these instructions:
https://docs.docker.com/engine/install/ubuntu/

To fully install the Docker Engine, we will use the instructions for the APT repoistory, as seen here: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

1. Setup the APT repository for Docker as seen here: https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository by running the following commands:
```
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```
2. Install the Docker packages using the following commands by running the following command: `sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin`
3. Check to see if the Docker service has started: `sudo systemctl status docker`
4. If it has not started, start the service with the following: `sudo systemctl start docker`
5. Verify the installation by running `sudo docker run hello-world`

## Installing the Juice-Shop Docker Container
Here are the main instructions we'll be following: https://hub.docker.com/r/bkimminich/juice-shop

1. With Docker installed and the service active, run: `docker pull bkimminich/juice-shop`. If you get a `permission denied` error, then run it again as `sudo docker pull bkimminich/juice-shop`. This command downloads all the necessary Docker images down to your computer. Images can be used to create containers.
2. Run a new instance of the Juice-Shop Docker container. `docker run --rm -p 3000:3000 bkimminich/juice-shop` There's a lot happening here, so let's break it down.
  - `docker run` means we're going to run a new container
  - `--rm` means that the docker container and any remnants are removed from the file system once the container closes.
  - `-p 3000:3000` stands for "publish". It's basically port fowarding. The format is `HOST_PORT:CONTAINER_PORT`. So, 3000:3000 connects port 3000 on your machine to port 3000 inside the container where the Juice Shop application is listening.
3. Open a browser and navigate to `http://localhost:3000`. You should see that OWASP Juice-Shop opened up. 
4. If you want to know more about Docker containers, and which ones are running on your system, run the following commands in another terminal window while your Juice-Shop Docker container (or really any other container is running).
  - `sudo docker ps` - You should see your running container, the container ID, the image name, the command executed within the container, when the container was created, the duration running (status), and the ports in use (e.g. 0.0.0.0:3000 -> 3000/tcp which means that the Host operating system is now listening on all interfaces on TCP port 3000 and any connections to TCP port 3000 will be sent to the Docker container.)
  - `sudo ss -auntp` Here's a universally helpful tool that will allow you to see all active TCP/UDP ports on your system and which binaries are communicating on those ports. See if you can find TCP port 3000 in the list.
  - `sudo docker inspect XXXXXXXXXXXX` And if you really want to know what the Docker container is doing, you can inspect the running container. To get the current container ID, run `sudo docker ps`, find your container and container ID (e.g. `d8f71ac367db`), and then run `sudo docker inspect d8f71ac367db`.
5. You can connect to the OWASP Juice-Shop and interact with the application (running in the container) by going to `http://localhost:3000` in your browser. Download Burp Suite Community Edition by Portswigger and have fun finding all the bugs and vulnerabilities. https://portswigger.net/burp/communitydownload
6. To `kill` the Docker container, simply press `CTRL+C` on the terminal window running the Docker container.