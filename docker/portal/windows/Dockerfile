# Uses Appleseed.Portal Build 1.2.43.305 | 12/19/2016
 
FROM microsoft/iis

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Install .NET 4.6.1 / IIS Management Tools
RUN Install-WindowsFeature NET-Framework-45-ASPNET ;\
    Install-WindowsFeature Web-Asp-Net45 ;\
    Install-WindowsFeature Web-Scripting-Tools ;\
    Install-WindowsFeature smtp-server
    
#Setup Working Directories
RUN MD C:\\Appleseed
WORKDIR C:\\Appleseed

# Using Add for now.  To-do : Should use wget 
ADD https://github.com/Appleseed/portal/releases/download/1.2.43.305/Appleseed.Portal.1.2.43.305.zip c:\\Appleseed

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Appleseed\\Appleseed.Portal.1.2.43.305.zip' -DestinationPath 'c:\\Appleseed\\Portal'"
    
#Remove the default IIS site and install Appleseed.Portal
RUN Remove-WebSite -Name 'Default Web Site'  
RUN  New-Website   -Name 'Appleseed.Portal' -Port 80 -PhysicalPath 'c:\Appleseed\Portal' -ApplicationPool '.NET v4.5'
  

#Make Web.config writable only for App Pool User
RUN $Acl = Get-Acl 'C:\Appleseed\Portal\Web.config' ;\
    $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule('IIS_IUSRS','Write','Allow') ;\
    $Acl.SetAccessRule($Ar) ;\
    Set-Acl 'C:\Appleseed\Portal\Web.config' $Acl
    
EXPOSE 80

#Cleanup

RUN rm c:\\Appleseed\\Appleseed.Portal.1.2.43.305.zip

#Make sure IIS comes up
CMD Write-Host IIS Started... ;\
    while ($true) { Start-Sleep -Seconds 3600 }
    



 
