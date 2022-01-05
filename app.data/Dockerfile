FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["app.data/app.data.csproj", "app.data/"]
RUN dotnet restore "app.data/app.data.csproj"
COPY . .
WORKDIR "/src/app.data"
RUN dotnet build "app.data.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "app.data.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "app.data.dll"]
