# Solr 5.5.3 on Windows Server Core 2016 ( UI Less)
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr
WORKDIR C:\\solr

#Download Latest JRE
add http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jre-8u111-windows-x64.exe c:\\solr\\jre-8u111-windows-x64.exe
#Install JRE
RUN Start-Process -FilePath jre-8u111-windows-x64.exe -ArgumentList "/s" -PassThru -Wait
# Remove JRE
RUN rm C:\\solr\\jre-8u111-windows-x64.exe   
# ADD Solr 5.5.3
ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip C:\\solr

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\solr\\solr-5.5.3.zip' -DestinationPath 'C:\\solr'"
 
#Cleanup
RUN rm C:\\solr\\solr-5.5.3.zip  

COPY .\\anant\\appleseed-search\\solr c:\\solr\\example\\solr
#Start Solr
RUN .\bin\solr start -f -p 8983 -s example\appleseed-search\solr -V

EXPOSE 8983

 


 
