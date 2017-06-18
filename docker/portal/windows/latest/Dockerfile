# Uses Latest Appleseed.Portal Build 
# This file compiles the github.com/portal Repositiory

FROM microsoft/iis

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Install .NET 4.6.1 / IIS Management Tools

RUN Install-WindowsFeature NET-Framework-45-ASPNET ;\
    Install-WindowsFeature Web-Asp-Net45 ;\
	Install-WindowsFeature Web-Scripting-Tools 
	

#Setup Working Directories
RUN MD C:\\Appleseed ;\
    MD C:\\Services
	
WORKDIR C:\\Appleseed

# Using Add for now.  To-do : Should use wget 
ADD https://github.com/Appleseed/portal/releases/download/v1.5.142.485/Appleseed.Portal.1.5.142.485.zip c:\\Appleseed

#Unzip the main archive
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Appleseed\\Appleseed.Portal.1.5.142.485.zip' -DestinationPath 'c:\\Appleseed\\Portal'"
 
#Cleanup
RUN rm c:\\Appleseed\\Appleseed.Portal.1.5.142.485.zip

#Remove the default IIS site and install Appleseed.Portal
RUN Remove-WebSite -Name 'Default Web Site' 
RUN  New-Website   -Name 'Appleseed.Portal' -Port 80 -PhysicalPath 'c:\Appleseed\Portal' -ApplicationPool '.NET v4.5'

#Make Web.config writable only for App Pool User
RUN $Acl = Get-Acl 'C:\Appleseed\Portal\Web.config' ;\
    $Ar = New-Object  system.security.accesscontrol.filesystemaccessrule('IIS_IUSRS','Write','Allow') ;\
	$Acl.SetAccessRule($Ar) ;\
	Set-Acl 'C:\Appleseed\Portal\Web.config' $Acl
	
EXPOSE 80

#STMP
# ADD STMP Client
ADD https://downloads.sourceforge.net/project/blat/Blat%20Full%20Version/64%20bit%20versions/blat3217_64.full.zip?r=&ts=1487698431&use_mirror=superb-dca2 c:\\Services

#Unzip the Client
RUN powershell -executionpolicy bypass -Command "expand-archive -Path 'c:\\Services\\blat3217_64.full.zip' -DestinationPath 'c:\\Services\\Mail'"

#Cleanup
RUN rm c:\\Services\\blat3217_64.full.zip