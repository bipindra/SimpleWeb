#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["SimpleWeb/SimpleWeb.csproj", "SimpleWeb/"]
RUN dotnet restore "SimpleWeb/SimpleWeb.csproj"
COPY . .
WORKDIR "/src/SimpleWeb"
RUN dotnet build "SimpleWeb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SimpleWeb.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimpleWeb.dll"]