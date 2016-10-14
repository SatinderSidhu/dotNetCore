# dotNetCore

A simple introduction to Dot Net Core & ASP.Net core. We will be creating the console application without Visual Studio or any other editor. It will be purely from DOS prompt (Old school way - Believe me its so much fun)

# my first dotNetCore application

### Step 1 - [Download](https://go.microsoft.com/fwlink/?LinkID=827524) the DotNet Core SDK.

### Step 2- Open command prompt & Create a folder DotNetCore on your C Drive (You can make a different directory of your choice of location). We will be using this folder to hold all of our examples & demo

    C:\>md dotNetCore
    C:\>cd dotNetCore
    C:\>dotNetCore>

###  Step 3- Create another folder inside this & name it as firstConsoleApp

    C:\dotNetCore>md firstConsoleApp
    C:\dotNetCore>cd firstConsoleApp
    C:\dotNetCore>firstConsoleApp>

> The folding structure matters here. the folder we will be using for creating the application counts for name space of the project name & assembly name here.

### Step 4
You have installed dotNetCore by now and have a folder to work with also. Now its the time to create first project. Lets try out first by checking if dotNetCore is successfully installed

Try the following command

    C:\dotNetCore>firstConsoleApp>dotnet

If every thing works fine, it should give version and build number. As of today I got following with some more detail 

    Microsoft .NET Core Shared Framework Host
      Version  : 1.0.1
      Build    : cee57bf6c981237d80aa1631cfe83cb9ba329f12

    Usage: dotnet [common-options] [[options] path-to-application]
    
    Common Options:
      --help                           Display .NET Core Shared Framework Host help.
      --version                        Display .NET Core Shared Framework Host version.

    Options:
      --fx-version <version>           Version of the installed Shared Framework to
    use to run the application.
      --additionalprobingpath <path>   Path containing probing policy and assemblies to probe for.

    Path to Application:
      The path to a .NET Core managed application, dll or exe file to execute.
    
    If you are debugging the Shared Framework Host, set 'COREHOST_TRACE' to '1' in y
    our environment.
    
    To get started on developing applications for .NET Core, install .NET SDK from:
      http://go.microsoft.com/fwlink/?LinkID=798306&clcid=0x409


### Step 5 - Awesome, now we have everything ready, Lets create our first project. Write the command "dotnet new"

    C:\dotnetcore\firstconsoleapp>dotnet new
    Created new C# project in C:\dotnetcore\firstconsoleapp.

You will see 2 files created in the folder. 

    C:\dotnetcore\firstconsoleapp>dir
     Volume in drive C is OS
     Volume Serial Number is 5698-08AD
    
     Directory of C:\dotnetcore\firstconsoleapp
    
    10/14/2016  03:02 PM    <DIR>          .
    10/14/2016  03:02 PM    <DIR>          ..
    09/20/2016  12:08 AM               214 Program.cs
    09/20/2016  12:08 AM               367 project.json
                   2 File(s)            581 bytes
                   2 Dir(s)  101,743,194,112 bytes free


Let's see the content of these two files. Program.cs actually contains the application entry point. 

    C:\dotnetcore\firstconsoleapp>type program.cs
    @using System;
    
    namespace ConsoleApplication
    {
        public class Program
        {
            public static void Main(string[] args)
            {
                Console.WriteLine("Hello World!");
            }
        }
    }


Project.json replaces the .csproj file and now it contains a list of all dependencies, environments, publish details etc.

    C:\dotnetcore\firstconsoleapp>type project.json
    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {},
      "frameworks": {
        "netcoreapp1.0": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.0.1"
            }
          },
          "imports": "dnxcore50"
        }
      }
    }

That's it. We have created our first console application. Let's compile it and run it now.

### Step 6 Restore the nuGet packages for application

Before we compile the application we need to restore all the packages and dependencies. To do that, lets run a restore commands, Its a kind of mandatory if you add any high level dependency to the project.json. 

    C:\dotnetcore\firstconsoleapp>dotnet restore
    log  : Restoring packages for C:\dotnetcore\firstconsoleapp\project.json...
    log  : Writing lock file to disk. Path: C:\dotnetcore\firstconsoleapp\project.lock.json
    log  : C:\dotnetcore\firstconsoleapp\project.json
    log  : Restore completed in 1477ms.

Project.lock.json, What is this? So what restore process actually did? It went into project.json and looked for all framework, build options and created a list of all dependencies and loaded them into project.lock.json. So project.lock.json pretty much depends on project.json but it contains more detail. Take a look on project.lock.json it will have much more information

    C:\dotnetcore\firstconsoleapp>type project.lock.json

> Any time you add any dependency to project.json you need to restore the project. If you are using any IDE like visual studio code or visual studio they will do it for you when you build the project.

### Step 7 Build the project
Yes now its the time to build the project. Issue the following command "dotnet run". 

    C:\dotnetcore\firstconsoleapp>dotnet build
    Project firstconsoleapp (.NETCoreApp,Version=v1.0) will be compiled because expected outputs are missing
    Compiling firstconsoleapp for .NETCoreApp,Version=v1.0
    
    Compilation succeeded.
        0 Warning(s)
        0 Error(s)
    
    Time elapsed 00:00:01.5589169

If you view the directory now, it would have created two new folder (bin, obj) as part of the build process

    C:\dotnetcore\firstconsoleapp>dir
     Volume in drive C is OS
     Volume Serial Number is 5698-08AD
    
     Directory of C:\dotnetcore\firstconsoleapp
    
    10/14/2016  03:21 PM    <DIR>          .
    10/14/2016  03:21 PM    <DIR>          ..
    10/14/2016  03:21 PM    <DIR>          bin
    10/14/2016  03:21 PM    <DIR>          obj
    09/20/2016  12:08 AM               214 Program.cs
    09/20/2016  12:08 AM               367 project.json
    10/14/2016  03:14 PM           290,574 project.lock.json
                   3 File(s)        291,155 bytes
                   4 Dir(s)  101,726,756,864 bytes free

### Step 8 Run the project - Yey its the time to run the application

    C:\dotnetcore\firstconsoleapp>dotnet run
    Project firstconsoleapp (.NETCoreApp,Version=v1.0) was previously compiled. Skipping compilation.
    Hello World!

So we see the output "Hello World". Just a reminder that the reason we don't need to provide any project name to run because its considering only one project in the parent folder

### Step 9 Publish the project (Windows)
The final step of any application building process is publish. So issue the "dotnet publish" command, It will take all the required settings from project.json and publish the project for specific runtime (Default is windows).

    C:\dotnetcore\firstconsoleapp>dotnet publish
    Publishing firstconsoleapp for .NETCoreApp,Version=v1.0
    Project firstconsoleapp (.NETCoreApp,Version=v1.0) was previously compiled. Skipping compilation.
    publish: Published to C:\dotnetcore\firstconsoleapp\bin\Debug\netcoreapp1.0\publish
    Published 1/1 projects successfully

>So what is special in dotNetCore as compared to ASP.Net, Yes its modular, fast and everything but the biggest advantage is same application can run on Linix, OSX. So now lets publish this application for Linux

### Step 9 Publish the project for other run times 

Lets make some changes publish process so that we can target different runtimes i.e. Linux or OSX. To do that we need to specify in project.json that about our target runtimes. Its called Runtime identifier & Here is the list of some [codes](https://docs.microsoft.com/en-us/dotnet/articles/core/rid-catalog) for each of the runtime. There are 2 steps which you need to follow. Add the following entry to project.json at root level

    "runtimes": {"win81-x64": {}}

Remove the following entry from "Microsoft.NETCore.App" object.
    "type": "platform",

So your final config will look like following Download the sample here

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {},
      "frameworks": {
        "netcoreapp1.0": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "version": "1.0.1"
            }
          },
          "imports": "dnxcore50"
        }
      },
    "runtimes": {"win81-x64": {}}
    }

[Download Window 7 Project.json](https://github.com/Satindersatty/dotNetCore/blob/gh-pages/project.json_Window7Runtime)
[Download OSX project.json])https://github.com/Satindersatty/dotNetCore/blob/gh-pages/Project.json_OSX)

Run the restore and publish it. You are all set

    C:\dotnetcore\firstconsoleapp>dotnet restore
    log  : Restoring packages for C:\dotnetcore\firstconsoleapp\project.json...
    log  : Writing lock file to disk. Path: C:\dotnetcore\firstconsoleapp\project.lock.json
    log  : C:\dotnetcore\firstconsoleapp\project.json
    log  : Restore completed in 944ms.
    
    C:\dotnetcore\firstconsoleapp>dotnet publish
    Publishing firstconsoleapp for .NETCoreApp,Version=v1.0/win81-x64
    Project firstconsoleapp (.NETCoreApp,Version=v1.0) will be compiled because inputs were modified
    Compiling firstconsoleapp for .NETCoreApp,Version=v1.0
    
    Compilation succeeded.
        0 Warning(s)
        0 Error(s)
    
    Time elapsed 00:00:01.3415627


    publish: Published to C:\dotnetcore\firstconsoleapp\bin\Debug\netcoreapp1.0\win81-x64\publish
    Published 1/1 projects successfully



Thanks for reading the blog.
