# -------------------------
# Build Stage
# -------------------------
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

WORKDIR /app

# Copy everything
COPY . .

# Restore solution
RUN dotnet restore eShopOnWeb.sln

# Publish Web project
WORKDIR /app/src/Web
RUN dotnet publish -c Release -o /app/publish

# -------------------------
# Runtime Stage
# -------------------------
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

WORKDIR /app

# Copy published output
COPY --from=build /app/publish .

EXPOSE 80

ENTRYPOINT ["dotnet", "Web.dll"]
