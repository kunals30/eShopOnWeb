FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
 
# Copy solution
COPY eShopOnWeb.sln .
 
# Copy project files
COPY src/ApplicationCore/ApplicationCore.csproj src/ApplicationCore/
COPY src/Infrastructure/Infrastructure.csproj src/Infrastructure/
COPY src/Web/Web.csproj src/Web/
 
# Restore
RUN dotnet restore eShopOnWeb.sln
 
# Copy everything else
COPY . .
 
WORKDIR /src/src/Web
RUN dotnet publish -c Release -o /app/publish
 
# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
 
ENTRYPOINT ["dotnet", "Web.dll"]
