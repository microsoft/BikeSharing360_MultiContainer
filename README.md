# Bikesharing360
Demo from Connect() 2016, where Donovan Brown opened an existing, "more complex" application than https://github.com/SteveLasker/Bikesharing360-Single to demonstrate seetting up Continuous Delivery with Visual Studio 2017 RC. 
The project was then deployed to Azure Container Services, through the Azure Container Registry.

# Building the project in a container
To validate the VSTS Build Steps will sucessfuly build the project, in a container, you can validate this locally:

How this works:

* when you call `docker-compose -f docker-compose.ci.build.yml up`, the image `microsoft/aspnetcore:1.0.1-sdk` is attempted to be instanced. 
* The first time, `microsoft/aspnetcore:1.0.1-sdk` isn't available compose up will build the image using  `.\build\Dockerfile` 
* The root of the solution is volume mapped in
* `dotnet restore`, `dotnet publish -c release` are executed

In the same folder as this readme.md file, call:
```
docker-compose -f docker-compose.ci.build.yml up
```

## directly on your dev machine

Once built, `cd .\bin\Release\publishoutput\`
From the published directory, `dotnet marketing.dll`
This will run the site at http://localhost:5000

## run in a container

Once built, `docker-compose up -d`
Find the dynamically assigned port: `docker ps`
```
 IMAGE                   PORTS
 bikesharing/marketing   0.0.0.0:32786->8080/tcp
```
http://localhost:32767
