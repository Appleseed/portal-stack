# portal-stack
This is a containerized stack for Appleseed Portal Platform ( part of the Appleseed Framework ) : https://github.com/Appleseed/portal/

Uses Windows 2016 Server, IIS, ASPNet 4.6.1, SQL Server 2016


##Quickstart :##

Configure and Install docker-machine, docker, and docker-compose on your machine or server. If you are using Windows 2016 Server, the OS now has Docker built-in.

### Windows Docker Composure
- `git clone https://github.com/Appleseed/portal-stack.git`
- `cd .\portal-stack\docker\compose\`
- `docker-compose -f .\docker-compose.windows.yml build`
- `docker-compose -p portal-stack -f .\docker-compose.windows.yml up -d`
- `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" portalstack_db-mssql-express-2016_1`
- `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" portalstack_web-appleseed-portal_1`

### Portal Docker Build
- `docker build https://raw.githubusercontent.com/Appleseed/portal-stack/master/docker/portal/windows/Dockerfile -t portal`
- `docker run -d -p 80:80 --name appleseed portal`
- `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" appleseed`

##Databases##
- TODO: SQL Server (disabled, for internal needs, tests)
- TODO: AzureDB ( under development)
