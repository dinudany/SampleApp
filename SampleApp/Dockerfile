FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY SampleApp/SampleApp.csproj SampleApp/
RUN dotnet restore SampleApp/SampleApp.csproj
COPY . .
WORKDIR /src/SampleApp
RUN dotnet build SampleApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish SampleApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SampleApp.dll"]
