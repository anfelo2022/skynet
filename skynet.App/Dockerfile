FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["skynet.App/skynet.App.csproj", "skynet.App/"]
RUN dotnet restore "skynet.App/skynet.App.csproj"
COPY . .
WORKDIR "/src/skynet.App"
RUN dotnet build "skynet.App.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "skynet.App.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "skynet.App.dll"]
