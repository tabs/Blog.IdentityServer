FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /app

# copy csproj and restore as distinct layers
COPY ./*.csproj ./Blog.IdentityServer/
RUN dotnet restore "Blog.IdentityServer/Blog.IdentityServer.csproj"

# copy everything else and build app
COPY ./ ./Blog.IdentityServer/
WORKDIR /app/Blog.IdentityServer
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS runtime
WORKDIR /app
COPY --from=build /app/Blog.IdentityServer/out ./
EXPOSE 5004 
ENTRYPOINT ["dotnet", "Blog.IdentityServer.dll","-b","0.0.0.0"]