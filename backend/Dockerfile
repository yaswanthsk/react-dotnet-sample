# Use the .NET SDK image to build the app
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /app

COPY backend/*.csproj ./backend/
RUN dotnet restore ./backend/Backend.csproj

COPY backend/. ./backend/
WORKDIR /app/backend
RUN dotnet publish -c Release -o out

# Use the .NET runtime image to run the app
FROM mcr.microsoft.com/dotnet/aspnet:8.0

WORKDIR /app
COPY --from=build /app/backend/out .

EXPOSE 5000

ENTRYPOINT ["dotnet", "Backend.dll"]
