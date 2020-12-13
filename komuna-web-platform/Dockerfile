#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["komuna-web-platform/komuna-web-platform.csproj", "komuna-web-platform/"]
RUN dotnet restore "komuna-web-platform/komuna-web-platform.csproj"
COPY . .
WORKDIR "/src/komuna-web-platform"
RUN dotnet build "komuna-web-platform.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "komuna-web-platform.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "komuna-web-plattform.dll"]