FROM mcr.microsoft.com/dotnet/sdk:8.0.3 AS build
WORKDIR /app

# Copy everything at once (simpler and safer)
COPY . .

# Restore from solution file
RUN dotnet restore eShopOnWeb.sln

# Publish Web project
WORKDIR /app/src/Web
RUN dotnet publish -c Release -o /app/publish

# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0.3 AS runtime
WORKDIR /app
COPY --from=build /app/publish .

ENTRYPOINT ["dotnet", "Web.dll"]
