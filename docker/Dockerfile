# ============================
# 1) Build stage
# ============================
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY docker/docker.csproj docker/ 
RUN dotnet restore docker/docker.csproj

# Copy the rest of the project files
COPY . ./

# Build the project
RUN dotnet publish docker/docker.csproj -c Release -o /app/publish

# ============================
# 2) Runtime stage
# ============================
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app

# Copy published output
COPY --from=build /app/publish .

# Expose port (optional)
EXPOSE 8080

# Start the application
ENTRYPOINT ["dotnet", "MyApp.dll"]