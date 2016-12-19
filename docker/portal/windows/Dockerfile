# Testing on 1.1.0.0 Release located : https://github.com/Appleseed/portal/releases
 
FROM microsoft/iis

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Install .NET 4.6.1 / IIS Management Tools
RUN Install-WindowsFeature NET-Framework-45-ASPNET ; \  
    Install-WindowsFeature Web-Asp-Net45 ;\
    Install-WindowsFeature Web-Scripting-Tools ;\
    Install-WindowsFeature Web-Static-Content
    

#Setup Working Directories
RUN MD C:\\Appleseed
WORKDIR C:\\Appleseed

# Using Add for now.  To-do : Should use wget 
ADD https://github.com/Appleseed/portal/releases/download/1.2.43.305/Appleseed.Portal.1.2.43.305.zip c:\\Appleseed

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Appleseed\\Appleseed.Portal.1.1.0.0.zip' -DestinationPath 'c:\\Appleseed\\Portal'"

#Set Application Pool to Value 2 : Network Service
# The below code seems to only work on local.  Doesnt work inside of a container.  Need to investigate.
#RUN Import-Module WebAdministration ;\
#    Set-ItemProperty 'IIS:\AppPools\.NET v4.5' -name processModel.identityType -value 2 ;\
#    iisreset
    
#Remove the default IIS site and install Appleseed.Portal
RUN Remove-WebSite -Name 'Default Web Site'  ;\
    New-Website -Name 'Appleseed.Portal' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Portal' -ApplicationPool '.NET v4.5'
  

#Make Web.config writable only for App Pool User
RUN $Acl = Get-Acl 'C:\Appleseed\Portal\Web.config' ;\
    $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule('IIS_IUSRS','Write','Allow') ;\
    $Acl.SetAccessRule($Ar) ;\
    Set-Acl 'C:\Appleseed\Portal\Web.config' $Acl
    
EXPOSE 80

#Make sure IIS comes up
CMD Write-Host IIS Started... ; \  
    while ($true) { Start-Sleep -Seconds 3600 }
    
#Cleanup

RUN rm c:\\Appleseed\\Appleseed.Portal.1.1.0.0.zip


 
