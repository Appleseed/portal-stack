# portal-stack
This is a containerized stack for Appleseed Portal Platform ( part of the Appleseed Framework ) : https://github.com/Appleseed/portal/

Uses Windows 2016 Server, IIS, ASPNet, SQL Server


#Quickstart :#

Configure and Install docker-machine, docker, and docker-compose on your machine or server. Windows 2016 Servers have Docker built-in.

- `docker build https://raw.githubusercontent.com/Appleseed/portal-stack/master/docker/dotnet/Dockerfile -t portal`
- `docker run -d -p 80:80 --name appleseed portal`
- `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" appleseed`

#Databases#
- TODO: SQL Server (disabled, for internal needs, tests)
- TODO: AzureDB ( under development)
