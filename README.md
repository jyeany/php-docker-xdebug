# php-docker-xdebug

## Overview  
This is a sample project to show how to create a simple PHP project using a docker container with debug capabilities.

## Prerequisites
Docker installed on system with access to filesystem 

## Adjust the Configuration
Find your ip address using *ifconfig* or *ipconfig*  

Replace the ip address in *docker-php-ext-xdebug.ini* with your ip address
```
xdebug.remote_host=<your-ip-address-here>
``` 

## Creating the container
Build the container
```
docker build -t first-debug .
```
  
Run the container
```
docker run -d -p 80:80 --name first-debug first-debug
```

## VS Code Debug Configuration
Have the PHP debug extension installed:  
https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-debug  
  
Configuration for this example:
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9000,
            "log": true,
            "pathMappings": {
                "/var/www/html": "${workspaceRoot}/app"    
            }
        },
        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000
        }
    ]
}
```

## Troubleshooting
The container is setup to create a remote log in the file: */remote-log/remote.log*  

View the contents of the log file with the following commands:
```
docker exec -it first-debug /bin/bash
cat /remote-log/remote.log
```