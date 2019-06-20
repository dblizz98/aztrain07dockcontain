FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["aztrain07dockcontain/aztrain07dockcontain.csproj", "aztrain07dockcontain/"]
RUN dotnet restore "aztrain07dockcontain/aztrain07dockcontain.csproj"
COPY . .
WORKDIR "/src/aztrain07dockcontain"
RUN dotnet build "aztrain07dockcontain.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "aztrain07dockcontain.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "aztrain07dockcontain.dll"]