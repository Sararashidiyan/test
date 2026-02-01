# -------- BUILD STAGE --------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY . .
RUN dotnet restore docker.csproj
RUN dotnet publish docker.csproj -c Release -o /app/publish /p:UseAppHost=false


# -------- RUNTIME STAGE --------
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

# Copy published output
COPY --from=build /app/publish .

# Expose port (change if needed)
EXPOSE 8080

# Start the app
ENTRYPOINT ["dotnet", "docker.dll"]

