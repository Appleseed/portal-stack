# Testing on 1.1.0.0 Release located : https://github.com/Appleseed/portal/releases
 
FROM microsoft/iis
SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Install .NET 4.6.1 / IIS Management Tools
RUN Install-WindowsFeature NET-Framework-45-ASPNET ; \  
    Install-WindowsFeature Web-Asp-Net45 ;\
    Import-Module ServerManager ;\
    Install-WindowsFeature Web-Scripting-Tools ;\
    Import-Module WebAdministration

#Setup Working Directories
RUN MD C:\\Appleseed
WORKDIR C:\\Appleseed

# Using Add for now.  To-do : Should use wget 
ADD https://github.com/Appleseed/portal/releases/download/v1.1.0.0/Appleseed.Portal.1.1.0.0.zip c:\\Appleseed

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Appleseed\\Appleseed.Portal.1.1.0.0.zip' -DestinationPath 'c:\\Appleseed\\Portal'"

#Remove the default IIS site and install Appleseed.Portal
RUN Remove-WebSite -Name 'Default Web Site'  
RUN New-Website -Name 'Appleseed.Portal' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Portal' -ApplicationPool '.NET v4.5'

#Set Application Pool to Value 2 : Network Service
RUN Set-ItemProperty "IIS:\AppPools\.NET v4.5" -name processModel.identityType -value 2   

#Make Web.config writable only for Network Service
RUN $Acl = Get-Acl "C:\Appleseed\Portal" 
RUN $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule("NETWORK SERVICE","Write","Allow") 
RUN $Acl.SetAccessRule($Ar) 
RUN Set-Acl "C:\Appleseed\Portal" $Acl
    
EXPOSE 80

#Make sure IIS comes up
CMD Write-Host IIS Started... ; \  
    while ($true) { Start-Sleep -Seconds 3600 }
    
#Cleanup

RUN rm c:\\Appleseed\\Appleseed.Portal.1.1.0.0.zip


 
