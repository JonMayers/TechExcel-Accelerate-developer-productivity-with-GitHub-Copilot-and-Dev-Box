# Use the official .NET 8 SDK image as a build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the remaining files and build the project
COPY . ./
RUN dotnet publish -c Release -o out

# Use the official .NET 8 runtime image as a runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/out .

# Set the environment variable for the ASP.NET Core port
ENV ASPNETCORE_HTTP_PORTS=8080

# Set the entry point for the application
ENTRYPOINT ["dotnet", "RazorPagesTestSample.dll"]