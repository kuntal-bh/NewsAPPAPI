FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY NewsAppApi/NewsAppApi.csproj NewsAppApi/
RUN dotnet restore NewsAppApi/NewsAppApi.csproj
COPY . .
WORKDIR /src/NewsAppApi
RUN dotnet build NewsAppApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish NewsAppApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "NewsAppApi.dll"]
