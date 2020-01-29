FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Service/Rest.API/Rest.API.csproj", "Service/Rest.API/"]
RUN dotnet restore "Service/Rest.API/Rest.API.csproj"
COPY . .
WORKDIR "/src/Service/Rest.API"
RUN dotnet build "Rest.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Rest.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Rest.API.dll"]