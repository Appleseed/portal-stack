# Uses Latest Appleseed.Portal Build 
# This file compiles the github.com/portal Repositiory

FROM microsoft/iis

SHELL ["powershell"]

MAINTAINER ANANT Corporation www.anant.us | Report Issues : https://github.com/Appleseed/portal-stack/issues

#Install .NET 4.6.1 / IIS Management Tools

RUN Install-WindowsFeature NET-Framework-45-ASPNET ;\
    Install-WindowsFeature Web-Asp-Net45 ;\
	Install-WindowsFeature Web-Scripting-Tools 