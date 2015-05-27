# verigreen-hook-on-stash
Stash docker container with Verigreen's external pre-receive hook pre-installed. Should be used with [Verigreen](https://github.com/organizations/Verigreen/verigreen)

Dockerized Stash
===================
This repository contains all you need to run your own stash container

Pre-requisites/assumptions:
-----
- Requires a computer(real or virtual) running ubuntu
- Must have docker installed 
- Must have a configuration file called config.yml with all needed values(or you can modify the included file to fit your particular installation)

- If you are behind a proxy you must have your settings properly configured so that docker can retrieve the official stash image (if you want to build the image from the Dockerfile)
- Must have a database container properly configured with a user and a database for stash

Usage:
------
- Create a text file called plugins.txt which contains a list of plugins to install in the following format: <plugin name>:<plugin version>
- Move the following files to your configuration directory:
   - config.yml
   - RSA_key.pub
   - plugins.txt

``` 
sudo docker run -d -p <host http port>:7990 -p <host ssh port>:7999 \
-v <path to your configuration directory in the host>:/var/stash/config \
--link <name of database container>:<name of database container> \
verigreen/stash
```   

- Wait a few seconds (about a minute or two should be more than enough)  for tomcat to initialize
  - You can also use the provided python program `test.py` to tell you when stash is ready to use.
- Point your browser to localhost:5000 (or whatever port you defined as the stash http port)
- If everything went well you should have a working stash container with your project and repository already created and all your plugins and hooks installed.
- Enjoy!
