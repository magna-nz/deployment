#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Deployment/Deployment.csproj", "Deployment/"]
RUN dotnet restore "Deployment/Deployment.csproj"
COPY . .ƒ
WORKDIR "/src/Deployment"
RUN dotnet build "Deployment.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Deployment.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Deployment.dll"]
