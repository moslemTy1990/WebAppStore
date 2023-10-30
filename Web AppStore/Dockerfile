FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Web AppStore/Web AppStore.csproj", "Web AppStore/"]
RUN dotnet restore "Web AppStore/Web AppStore.csproj"
COPY . .
WORKDIR "/src/Web AppStore"
RUN dotnet build "Web AppStore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Web AppStore.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Web AppStore.dll"]
