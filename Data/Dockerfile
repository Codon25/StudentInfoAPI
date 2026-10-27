FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build

WORKDIR /src

# Copy the actual project file
COPY ["StudentAPI.csproj", "./"]

# Restore dependencies
RUN dotnet restore "StudentAPI.csproj"

# Copy all application files
COPY . .

# Publish application
RUN dotnet publish "StudentAPI.csproj" -c Release -o /app/publish --no-restore


FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS final

WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 10000

ENTRYPOINT ["sh", "-c", "exec dotnet StudentAPI.dll --urls http://0.0.0.0:${PORT:-10000}"]