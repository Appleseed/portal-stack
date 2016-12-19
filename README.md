# portal-stack
This is a Docker containerized stack for the Appleseed Portal Platform : https://github.com/Appleseed/portal/

It allows enthusiasts, IT Pros, developers, and designers to quickly bring up Appleseed Portal enterprise configured containers.  The stack uses Windows 2016 Server Core, IIS, ASPNet 4.6.1, SQL Server 2016 Express.


##Quickstart :##

Configure and Install docker-machine, docker, and docker-compose on your machine or server. 

If you are using Windows 2016 Server, the OS now has Docker built-in (but you may have to install compose).
- [Get Docker ](https://www.docker.com/products/overview)
- [Windows Container Docs ](https://aka.ms/WindowsContainers)

### Windows Docker Portal-Stack Composure
- `git clone https://github.com/Appleseed/portal-stack.git`
- `cd .\portal-stack\docker\compose\`
- `docker-compose -f .\docker-compose.windows.yml build`
- `docker-compose -p portal-stack -f .\docker-compose.windows.yml up -d`
- `docker-compose -p portal-stack -f .\docker-compose.windows.yml ps`
- `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" portalstack_db-mssql-express-2016_1`
- `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" portalstack_web-appleseed-portal_1`

### Appleseed.Portal Docker Build
- `docker build https://raw.githubusercontent.com/Appleseed/portal-stack/master/docker/portal/windows/Dockerfile -t portal`
- `docker run -d -p 80:80 --name appleseed portal`
- `docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" appleseed`

### Appleseed.Search Docker Build
- TODO: Add Appleseed.Search Integration with Appleseed.Portal

### Database Docker Build
- TODO: SQL Server - Attach working fresh database file
- TODO: AzureDB - Add Scripts to create empty AzureDB


