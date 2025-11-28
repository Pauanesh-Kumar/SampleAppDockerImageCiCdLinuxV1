# Dockerfile — OFFICIAL MICROSOFT .NET 9 MVC PATTERN (2025)
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 8080

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy project file
COPY *.csproj ./
RUN dotnet restore

# Copy source code
COPY . ./

# Publish — THIS LINE IS CRITICAL FOR MVC VIEWS
RUN dotnet publish -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app

# Copy published output (includes Views, wwwroot, everything)
COPY --from=build /app/publish ./

# Set correct permissions for Windows runner
USER ContainerAdministrator

ENTRYPOINT ["dotnet", "SampleAppDockerImageCiCdLinuxV1.dll"]