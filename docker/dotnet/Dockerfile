# Testing on 1.0.9 Release located : https://github.com/Appleseed/portal/releases
# Since Powershell has weak Unzip ability, simply unzip the latest zip package into
# the folder before running this docker File

FROM microsoft/iis:windowsservercore 
SHELL ["powershell"]

MAINTAINER ANANT Corporation <info@anant.us>

#Install .NET 4.6.1
RUN Install-WindowsFeature NET-Framework-45-ASPNET ; \  
    Install-WindowsFeature Web-Asp-Net45

#Seup Env for Unzip
RUN MD C:\\Appleseed
WORKDIR C:\\Appleseed
RUN [System.Reflection.Assembly]::LoadWithPartialName("System.IO.Compression.FileSystem") | Out-Null

# Using Add for now.  To-do : Should use wget 
ADD https://github.com/Appleseed/portal/releases/download/v1.1.0.0/Appleseed.Portal.1.1.0.0.zip c:\\Appleseed

RUN [System.IO.Compression.ZipFile]::ExtractToDirectory("c:\\Appleseed\\Appleseed.Portal.1.1.0.0.zip", "c:\\Appleseed\Portal")

RUN Remove-WebSite -Name 'Default Web Site'  
RUN New-Website -Name 'Appleseed.Portal' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Portal' -ApplicationPool '.NET v4.5'
EXPOSE 80

CMD Write-Host IIS Started... ; \  
    while ($true) { Start-Sleep -Seconds 3600 }
