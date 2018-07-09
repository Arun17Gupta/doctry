FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 62113
EXPOSE 44383

FROM microsoft/dotnet:2.1-sdk-nanoserver-1709 AS build
WORKDIR /src
COPY doctry/doctry.csproj doctry/
RUN dotnet restore doctry/doctry.csproj
COPY . .
WORKDIR /src/doctry
RUN dotnet build doctry.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish doctry.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "doctry.dll"]
