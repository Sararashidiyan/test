# ---------- BUILD ----------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy everything in this folder
COPY . .

# Restore & publish the project explicitly
RUN dotnet restore docker.csproj
RUN dotnet publish docker.csproj -c Release -o /out /p:UseAppHost=false


# ---------- RUNTIME ----------
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

COPY --from=build /out .

EXPOSE 8080
ENTRYPOINT ["dotnet", "docker.dll"]


