# -------- BUILD STAGE --------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
 
# Copy solution and project files
COPY ../../eShopOnWeb.sln .
COPY ../ApplicationCore/ApplicationCore.csproj ApplicationCore/
COPY ../Infrastructure/Infrastructure.csproj Infrastructure/
COPY Web.csproj Web/
 
# Restore dependencies
RUN dotnet restore Web/Web.csproj
 
# Copy everything
COPY . .
WORKDIR /src/Web
 
# Publish app
RUN dotnet publish -c Release -o /app/publish
 
# -------- RUNTIME STAGE --------
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "Web.dll"]
