# Étape de build
FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /app

# Copie du fichier projet et restauration des dépendances
COPY src/Worker/Worker.csproj src/Worker/
RUN dotnet restore "src/Worker/Worker.csproj"

# Copie du reste du code source
COPY . .

# Build de l'application
WORKDIR "/app/src/Worker"
RUN dotnet build "Worker.csproj" -c Release -o /app/build

# Publication de l'application
FROM build AS publish
RUN dotnet publish "Worker.csproj" -c Release -o /app/publish

# Exécution
FROM mcr.microsoft.com/dotnet/core/runtime:3.1 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Worker.dll"]


# docker build -t worker .
