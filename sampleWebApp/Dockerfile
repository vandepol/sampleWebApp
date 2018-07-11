FROM microsoft/dotnet:2.1-aspnetcore-runtime
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.1 AS build
WORKDIR /src
COPY sampleWebApp.sln ./
COPY sampleWebApp/sampleWebApp.csproj sampleWebApp/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/sampleWebApp
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "sampleWebApp.dll"]
