FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

COPY ["FileStoringService.csproj", "./"]
RUN dotnet restore "./FileStoringService.csproj"

COPY . .

WORKDIR "/src/"
RUN dotnet publish "FileStoringService.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app

COPY --from=build /app/publish .
ENV ASPNETCORE_URLS=http://+:80
ENTRYPOINT ["dotnet", "FileStoringService.dll"]
