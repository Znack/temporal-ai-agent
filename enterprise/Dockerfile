# Dockerfile for .NET Enterprise Worker
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj and restore as distinct layers
COPY TrainSearchWorker.csproj ./
RUN dotnet restore TrainSearchWorker.csproj

# Copy the rest of the source files
COPY . ./
RUN dotnet publish TrainSearchWorker.csproj -c Release -o /app/publish

# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "TrainSearchWorker.dll"]
