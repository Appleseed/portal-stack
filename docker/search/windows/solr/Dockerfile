# Solr 5.5.3 on Windows Server Core 2016 ( UI Less)
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr ;\
    MD C:\\Tempsoft ;\
    MD C:\\elastic
    
WORKDIR C:\\solr

#Download Latest JRE
add http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jre-8u111-windows-x64.exe C:\\Tempsoft\\jre-8u111-windows-x64.exe
#Install JRE
RUN CD C:\\Tempsoft ;\
    Start-Process -FilePath jre-8u111-windows-x64.exe -ArgumentList "/s" -PassThru -Wait
# Remove JRE
RUN rm C:\\Tempsoft\\jre-8u111-windows-x64.exe   
# ADD Solr 5.5.3
ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip C:\\Tempsoft
#
#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\solr-5.5.3.zip' -DestinationPath 'C:\\solr'"
 
#Cleanup
RUN rm C:\\Tempsoft\\solr-5.5.3.zip  

#Add Core
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.1.1.0/appleseed-search.core.zip C:\\Tempsoft
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\appleseed-search.core.zip' -DestinationPath 'C:\\Tempsoft'"
COPY C:\\Tempsoft\\appleseed-search\\solr c:\\solr\\solr-5.5.3\\example\\solr
#Start Solr
RUN c:\\solr\solr-5.5.3\\bin\\\solr start -f -p 8983 -s example\\appleseed-search\solr -V

EXPOSE 8983

 


 
