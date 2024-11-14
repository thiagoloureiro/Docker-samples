# Step 1: Build the application
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the .csproj and restore any dependencies (via dotnet restore)
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application code
COPY . ./

# Publish the application to the /out directory
RUN dotnet publish -c Release -o /out

# Step 2: Create a minimal runtime container
FROM mcr.microsoft.com/dotnet/aspnet:9.0

# Set the working directory inside the container
WORKDIR /app

# Copy the published application from the build stage
COPY --from=build /out .

# Expose the port that the app will run on (by default, the app runs on 80)
EXPOSE 8080

# Set the entry point to run the application
ENTRYPOINT ["dotnet", "MyDotnetApp.dll"]
