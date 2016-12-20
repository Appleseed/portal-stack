# Solr 5.5.3 on Windows Server Core 2016 ( UI Less)
 
FROM microsoft/windowsservercore

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Setup Working Directories
RUN MD C:\\solr ;\
    MD C:\\Tempsoft ;\
    MD C:\\Appleseed\\Proxy
       
WORKDIR C:\\solr

#Install .NET 4.6.1 / IIS Management Tools
RUN Install-WindowsFeature NET-Framework-45-ASPNET ; \  
    Install-WindowsFeature Web-Asp-Net45 ;\
    Install-WindowsFeature Web-Scripting-Tools ;\
    Install-WindowsFeature Web-Static-Content
    

#Install chocolatey and any required tools
RUN $env:chocolateyUseWindowsCompression = 'false' ;\
    iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1')) ;\
    chocolatey feature enable -n=allowGlobalConfirmation ;\
    choco install jdk8 ;\
    choco install 7zip.install ;\
    choco install urlrewrite ;\
    choco install nssm
  
#Pull down Proxy
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.1.1.0/solr.proxy.config.zip C:\\Appleseed\\Proxy    
    
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Appleseed\\Proxy\\solr.proxy.config.zip' -DestinationPath ' C:\\Appleseed\\Proxy'" ;\
    rm C:\\Appleseed\\Proxy\\solr.proxy.config.zip

#Create an IIS Proxy
RUN Remove-WebSite -Name 'Default Web Site'  ;\
    New-Website -Name 'Appleseed.Search.Proxy' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Proxy' -ApplicationPool '.NET v4.5'
    
 
# ADD Solr 5.5.3
ADD http://apache.mirrors.ionfish.org/lucene/solr/5.5.3/solr-5.5.3.zip  C:\\Tempsoft
#Unzip the main archive
#Solr is so large it needs 7zip to unzip and not error
RUN cd $env:programfiles\\7-Zip\\ ;\
   ./7z x  C:\\Tempsoft\\solr-5.5.3.zip -oc:\\solr

#Cleanup
RUN rm  C:\\Tempsoft\\solr-5.5.3.zip  

#Add Core
ADD https://github.com/Appleseed/portal-stack/releases/download/v1.1.1.0/appleseed-search.core.zip C:\\Tempsoft
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'C:\\Tempsoft\\appleseed-search.core.zip' -DestinationPath 'C:\\Tempsoft'" 
#add core example
RUN CP C:\\Tempsoft\\appleseed-search c:\\solr\\solr-5.5.3\\example
#Start Solr
RUN cd c:\\solr\\solr-5.5.3\\bin ;\
    dir ;\
    cd c:\\solr\\solr-5.5.3\\example ;\
    dir ;\
    cd c:\\solr\\solr-5.5.3\\example\\appleseed-search ;\
    dir
  # ./solr start -f -p 8983 -s c:\\solr\\solr-5.5.3\\example\\appleseed-search\\solr -V

#ENTRYPOINT ["C:\\solr\\solr-5.5.3\\bin\\solr.cmd" ]

#CMD ["start -f -p 8983 -s example\\appleseed-search\\solr -V"]
#nssm install 'solr5' 'C:\\solr\\solr-5.5.3\\bin\\solr.cmd' 'start -f -p 8983 -s example\\appleseed-search\\solr -V'
EXPOSE 8983

 


 
