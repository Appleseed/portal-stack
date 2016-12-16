# portal-stack
Appleseed Portal Stack Docker composition : https://github.com/Appleseed/portal/

Uses DotNet, ASPNet, SQL Server


* Instructions 

`docker build https://raw.githubusercontent.com/Appleseed/portal-stack/master/docker/dotnet/Dockerfile -t portal`
`docker run -d -p 80:80 --name appleseed portal`
