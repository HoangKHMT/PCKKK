# ===== BUILD STAGE =====
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy csproj và restore
COPY ["PCM.Api/PCM.Api.csproj", "PCM.Api/"]
RUN dotnet restore "PCM.Api/PCM.Api.csproj"

# Copy toàn bộ source
COPY . .
WORKDIR "/src/PCM.Api"
RUN dotnet publish "PCM.Api.csproj" -c Release -o /app/publish

# ===== RUNTIME STAGE =====
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:10000
EXPOSE 10000
ENTRYPOINT ["dotnet", "PCM.Api.dll"]
