# Ecommerce_AspNetCore_Container_Microservice


Ecommerce Web application using ASP.NET CORE, Microservices, docker, containers, EntityFramework


To Run the Applications, following the steps below:

Must Swicth to Linux container

1 - docker run -e ACCEPT_EULA=Y  -e SA_PASSWORD=ProductApi@123 -e MSSQL_PID=Express -p 1445:1433   --name=CatalogDb microsoft/mssql-server-linux:latest

2 - docker ps

CONTAINER ID        IMAGE                                 COMMAND                  CREATED              STATUS              PORTS                    NAMES
1d82e466713a        microsoft/mssql-server-linux:latest   "/opt/mssql/bin/sqls…"   About a minute ago   Up 59 seconds       0.0.0.0:1445->1433/tcp   CatalogDb
PS C:\Users\admin>


3 - docker exec -it CatalogDb /opt/mssql-tools/bin/sqlcmd -S localhost -U sa

4 - 
create DATABASE TestDb
 exit


5 - PS C:\Users\admin> docker exec -it CatalogDb /opt/mssql-tools/bin/sqlcmd -S localhost -U sa
Password:
1>
2>
3> create database TrialDb
4> select Name from sys.databases
5> GO
Name                                                                                                                    
--------------------------------------------------------------------------------------------------------------------------------
master                                                                                                                  
tempdb                                                                                                                  
model                                                                                                                   
msdb                                                                                                                    
TrialDb   


6 - 

"Catalog": {
    "ConnectionString": "Server=localhost,1445;Database=CatalogDb;User Id=sa;Password=ProductApi@123;MultipleActiveResultSets=true"

  },


7 - Run Nuget Microsoft.EntityFrameworkCore.Tools

8 -Check out the References in project files
<ItemGroup>
    <DotNetCliToolRefernce Include="Microsoft.EntityFrameworkCore.Tools.DotNet" Version="2.0.0" />
    <DotNetCliToolReference Include="Microsoft.VisualStudio.Web.CodeGeneration.Tools" Version="2.0.0" />
  </ItemGroup>


9 - Run

 dotnet tool install global dotnet-ef

 dotnet ef migrations add InitialMigration -o Data/Migrations    -c ShoesOnContainers.Services.ProductCatalogApi.Data.CatalogDbContext

Add nuget
Microsoft.EntityFrameworkCore.SqlServer
Microsoft.EntityFrameworkCore.Design
Microsoft.EntityFrameworkCore.Tools

10- Start catalogdb if not running
Docker start catalogdb

11- Update DB for CatalogDB container

dotnet ef database update InitialMigration -c ShoesOnContainers.Services.ProductCatalogApi.Data.CatalogDbContext

Build started...
Build succeeded.
Applying migration '20170925084431_Initial'.
Applying migration '20200927121411_InitialMigration'.
Done.


