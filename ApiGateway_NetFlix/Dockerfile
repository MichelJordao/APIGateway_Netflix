FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["ApiGateway_NetFlix/ApiGateway_NetFlix.csproj", "ApiGateway_NetFlix/"]
RUN dotnet restore "ApiGateway_NetFlix/ApiGateway_NetFlix.csproj"
COPY . .
WORKDIR "/src/ApiGateway_NetFlix"
RUN dotnet build "ApiGateway_NetFlix.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ApiGateway_NetFlix.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ApiGateway_NetFlix.dll"]