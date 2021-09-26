FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["testapi/testapi.csproj", "testapi/"]
RUN dotnet restore "testapi/testapi.csproj"
COPY . .
WORKDIR "/src/testapi"
RUN dotnet build "testapi.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "testapi.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "testapi.dll"]
