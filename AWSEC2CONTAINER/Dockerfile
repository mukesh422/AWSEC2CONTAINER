#Use the official .NET Core SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /app

#Copy the project file ans restore any dependencies (use .csproj for the project name )
COPY *.csproj ./
RUN dotnet restore

#Copy the rest of the application code 
COPY . .

#publish the application
RUN dotnet publish -c Rellease -o out

#Build the runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app
COPY --from*build /app/out ./

#Expose the port your application will run on
EXPOSE 80

#Start the application
ENTRYPOINT ["dotnet", "AWSEC2CONTAINER.dll"]