# Testing on 1.1.0.0 Release located : https://github.com/Appleseed/portal/releases
 
FROM microsoft/iis
SHELL ["powershell"]

MAINTAINER ANANT Corporation <info@anant.us>

#Install .NET 4.6.1
RUN Install-WindowsFeature NET-Framework-45-ASPNET ; \  
    Install-WindowsFeature Web-Asp-Net45

#Setup Working Directories
RUN MD C:\\Appleseed
WORKDIR C:\\Appleseed

#Setup Unzip
#RUN [System.Reflection.Assembly]::LoadWithPartialName("System.IO.Compression.FileSystem") 
RUN Add-Type -Path "C:\\Windows\\Microsoft.NET\\Framework64\\v4.0.30319\\System.IO.Compression.FileSystem.dll"

# Using Add for now.  To-do : Should use wget 
ADD https://github.com/Appleseed/portal/releases/download/v1.1.0.0/Appleseed.Portal.1.1.0.0.zip c:\\Appleseed

#Unzip the main archive
RUN [System.IO.Compression.ZipFile]::ExtractToDirectory("c:\\Appleseed\\Appleseed.Portal.1.1.0.0.zip", "c:\\Appleseed\\Portal")

#Remove the default IIS site and install Appleseed.Portal
RUN Remove-WebSite -Name 'Default Web Site'  
RUN New-Website -Name 'Appleseed.Portal' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Portal' -ApplicationPool '.NET v4.5'
EXPOSE 80

#Make sure IIS comes up
CMD Write-Host IIS Started... ; \  
    while ($true) { Start-Sleep -Seconds 3600 }

 
