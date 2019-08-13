# Wkhtmltopdf.NetCore

![NuGet](https://buildstats.info/nuget/Wkhtmltopdf.NetCore)
[![Build status](https://ci.appveyor.com/api/projects/status/uws43d45pusuhq3a?svg=true)](https://ci.appveyor.com/project/fpanaccia/wkhtmltopdf-netcore-qft6o)

This project implements the library wkhtmltopdf for asp net core, working in windows and linux and docker.

For more information about how to use it, go to https://github.com/fpanaccia/Wkhtmltopdf.NetCore.Example

# But i dont want too see another repository

You will need to put this files with this following structure, this need to be done because nuget cant copy those files, only puts a link with the full path and will only work on your computer.

The structure will need to be on the folder of your project

        .
        ├── Example
        |   ├── Example.csproj
        |   └── Rotativa
        |   |   ├── Linux
        |   |   |   └── wkhtmltopdf
        |   |   └── Windows
        |   |       └── wkhtmltopdf.exe
        └── Example.sln

Those files will need to be included in your project with the propierty "Copy Always", then add to your Startup.cs in ConfigureServices method, this line "services.AddWkhtmltopdf();", like this

        // This method gets called by the runtime. Use this method to add services to the container.
        public void ConfigureServices(IServiceCollection services)
        {
            services.AddMvc().SetCompatibilityVersion(CompatibilityVersion.Version_2_1);
            services.AddWkhtmltopdf();
        }
        
If you are using the docker container for net core provided from microsoft, you need to add this line to the dockerfile "RUN apt-get update -qq && apt-get -y install libgdiplus libc6-dev", like this

        FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
        WORKDIR /app
        RUN apt-get update -qq && apt-get -y install libgdiplus libc6-dev
        EXPOSE 80

In linux you also need to install the same libraries used in the dockerfile, they are libgdiplus, libc6-dev


For more information, see the example project -> https://github.com/fpanaccia/Wkhtmltopdf.NetCore.Example
