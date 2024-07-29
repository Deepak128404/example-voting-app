# Build stage
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /source

# Copy csproj and restore dependencies
COPY *.csproj .

# Explicitly update System.Drawing.Common before restore
RUN dotnet add package System.Drawing.Common --version 7.0.0

RUN dotnet restore

# Copy the rest of the code and publish
COPY . .
RUN dotnet publish -c release -o /app --self-contained false --no-restore

# Runtime stage
FROM mcr.microsoft.com/dotnet/runtime:7.0
WORKDIR /app
COPY --from=build /app .

ENTRYPOINT ["dotnet", "Worker.dll"]
