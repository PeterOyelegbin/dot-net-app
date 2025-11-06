# dot-net-app
ASP Dot Net App

1. dotnet new sln -o HelloWorldApp
2. cd HelloWorldApp
3. dotnet new mvc -n HelloWorldApp.Web
4. dotnet sln HelloWorldApp.sln add HelloWorldApp.Web/HelloWorldApp.Web.csproj
5. dotnet restore
6. dotnet build --no-restore --configuration release
7. dotnet publish --no-build --configuration release
8. 
