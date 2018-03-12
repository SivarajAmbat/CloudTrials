# Index

- Deploying a simple HTML website on Windows Container
- Deploying a simple HTML website on Linux Container
- Deploying a simple Node.js app on Windows Container
- Deploying a simple Node.js app on Linux Container
- Deploying an ASP.NET application on Windows Container
- Deploying an ASP.NET Core application on Windows Container
- Deploying an ASP.NET Core application on Linux Container



# Details


### Deploying a simple HTML website on Windows Container
Tested :+1:
```
FROM microsoft/windowsservercore
RUN powershell –Command Add-WindowsFeature Web-Server
COPY index.htm /inetpub/wwwroot
EXPOSE 80
CMD [“cmd”]
```

### Deploying a simple HTML website on Linux Container
TESTED: NO
[ ] This is an incomplete item


### Deploying a simple Node.js app on Windows Container
TESTED: NO
[ ] This is an incomplete item


### Deploying a simple Node.js app on Linux Container
TESTED: NO
```
FROM mhart/alpine-node

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install app dependencies
COPY server/package.json /usr/src/app/
RUN npm install

# Bundle app source
COPY server/ /usr/src/app/

ENV PORT 80

CMD["npm", "start"]
```

### Deploying an ASP.NET application on Windows Container
Tested: NO
```
FROM microsoft/iis:latest
SHELL ["powershell"]
RUN Install-WindowsFeature NET-Framework-45-ASPNET; \
		 Install-WindowsFeature Web-Asp-Net45
COPY WebApp WebApp
RUN Remove-WebSite -Name 'Default Web Site'
RUN New-Website -Name 'WebApp' -Port 80 \
		 -PhysicalPath 'C:\WebApp' -ApplicationPool '.NET v4.5'
EXPOSE 80
CMD ["ping","-t","localhost"]
```


Tested: :+1:

```
FROM microsoft/aspnet
COPY ./bin/Release/PublishOutput /inetpub/wwwroot
```

### Deploying an ASP.NET Core application on Windows Container
Tested: NO
```
FROM microsoft/aspnetcore:1.1
ARG source
WORKDIR /app
COPY ${source:-obj/Docker/publish}
ENTRYPOINT[“dotnet”, “FirstDockerAPI.dll”]

```
### Deploying an ASP.NET Core application on Linux Container
Tested: NO

[ ] This is an incomplete item
