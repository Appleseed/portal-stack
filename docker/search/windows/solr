# Solr 5.5.3 on Windows Server Core
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr
WORKDIR C:\\solr

ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip C:\\solr

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\solr\\solr-5.5.3.zip' -DestinationPath 'C:\\solr'"
    
#Cleanup

RUN rm C:\\solr\\solr-5.5.3.zip   


 
