# Elastic 5.1.1 on Windows Server Core 2016 ( UI Less)
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\Tempsoft ;\
    MD C:\\elastic
    
WORKDIR C:\\elastic

#Install chocolatey
RUN $env:chocolateyUseWindowsCompression = 'false' ;\
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) ;\
    chocolatey feature enable -n=allowGlobalConfirmation ;\
    choco install jdk8
 
# ADD Elastic 5.1.1
ADD https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.1.1.zip C:\\Tempsoft

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\elasticsearch-5.1.1.zip' -DestinationPath 'C:\\elastic'"
 
#Cleanup
RUN rm C:\\Tempsoft\\elasticsearch-5.1.1.zip  

#Start Elastic
#RUN c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat

EXPOSE 9200

ENTRYPOINT ["c:\\elastic\\elasticsearch-5.1.1\\bin\\elasticsearch.bat"]
 


 
