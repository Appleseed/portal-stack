# Testing on 1.0.9 Release located : https://github.com/Appleseed/portal/releases
# Since Powershell has weak Unzip ability, simply unzip the latest zip package into
# the folder before running this docker File

FROM microsoft/iis:windowsservercore 
SHELL ["powershell"]

MAINTAINER ANANT Corporation <info@anant.us>

RUN Install-WindowsFeature NET-Framework-45-ASPNET ; \  
    Install-WindowsFeature Web-Asp-Net45


COPY Appleseed.Portal.1.0.9.0 c:\Appleseed\Portal

RUN Remove-WebSite -Name 'Default Web Site'  
RUN New-Website -Name 'Appleseed.Portal' -Port 80 \  
    -PhysicalPath 'c:\Appleseed\Portal' -ApplicationPool '.NET v4.5'
EXPOSE 80

CMD Write-Host IIS Started... ; \  
    while ($true) { Start-Sleep -Seconds 3600 }
