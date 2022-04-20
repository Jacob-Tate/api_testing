FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build-env

WORKDIR /app

# Pull the csproj
COPY *.csproj ./

# Download packages
RUN dotnet restore

# Pull rest of project
COPY . ./

# Build the project
RUN dotnet publish -c Release -o out


FROM mcr.microsoft.com/dotnet/aspnet:6.0

WORKDIR /app

# Pull the sdk build into our runtime environment
COPY --from=build-env /app/out .

# Set the entrypoint to our built application
ENTRYPOINT [ "dotnet", "PlatformService.dll"]