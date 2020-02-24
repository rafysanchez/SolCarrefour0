FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MovtosFinanceirosAPI/MovtosFinanceirosAPI.csproj", "MovtosFinanceirosAPI/"]
RUN dotnet restore "MovtosFinanceirosAPI/MovtosFinanceirosAPI.csproj"
COPY . .
WORKDIR "/src/MovtosFinanceirosAPI"
RUN dotnet build "MovtosFinanceirosAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "MovtosFinanceirosAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MovtosFinanceirosAPI.dll"]
