# Solr 5.5.3 on Windows Server Core 2016 ( UI Less)
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr ;\
    MD C:\\Tempsoft 
       
WORKDIR C:\\solr

#Install chocolatey
RUN $env:chocolateyUseWindowsCompression = 'false' ;\
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) ;\
    chocolatey feature enable -n=allowGlobalConfirmation ;\
    choco install jdk8 ;\
    choco install 7zip.install
 
# ADD Solr 5.5.3
ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip  C:\\Tempsoft
#Unzip the main archive
#RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\solr-5.5.3.zip' -DestinationPath 'C:\\solr'"
RUN cd $env:programfiles\\7-Zip\\ ;\
   ./7z x  C:\\Tempsoft\\solr-5.5.3.zip -oc:\\solr

#Cleanup
RUN rm  C:\\Tempsoft\\solr-5.5.3.zip  

#Add Core
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.1.1.0/appleseed-search.core.zip C:\\Tempsoft
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\appleseed-search.core.zip' -DestinationPath 'C:\\Tempsoft\\appleseed-search'"

RUN CD  C:\\Tempsoft ;\
        DIR;\
        CD C:\\Tempsoft\\appleseed-search  ;\
        DIR ;\
        CD c:\\solr ;\
        DIR ;\
        cd c:\\solr\\solr-5.5.3\\example ;\
        dir ;\
        
        
#COPY C:\\Tempsoft\\appleseed-search\\solr c:\\solr\\solr-5.5.3\\example\\solr
#Start Solr
RUN 'c:\\solr\\solr-5.5.3\\bin\\solr start -f -p 8983 -s example\\appleseed-search\\solr -V'

EXPOSE 8983

 


 
