#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ./src . 

WORKDIR "/src/TechBlog.News.API"
RUN dotnet restore "TechBlog.News.API.csproj"
RUN dotnet build "TechBlog.News.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "TechBlog.News.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
EXPOSE 80
ENTRYPOINT ["dotnet", "TechBlog.News.API.dll"]