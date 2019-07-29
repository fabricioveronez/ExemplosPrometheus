FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["AspNetWebSite/AspNetWebSite.csproj", "AspNetWebSite/"]
RUN dotnet restore "AspNetWebSite/AspNetWebSite.csproj"
COPY . .
WORKDIR "/src/AspNetWebSite"
RUN dotnet build "AspNetWebSite.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "AspNetWebSite.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetWebSite.dll"]
