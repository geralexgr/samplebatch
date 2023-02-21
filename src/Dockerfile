#FROM mcr.microsoft.com/dotnet/core/runtime:3.1-buster-slim AS base
FROM mcr.microsoft.com/dotnet/runtime:7.0 AS base
WORKDIR /app

#FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build


WORKDIR /src
COPY ["samplebatch/samplebatch.csproj", "samplebatch/"]
RUN dotnet restore "samplebatch/samplebatch.csproj"
COPY . .
WORKDIR "/src/samplebatch"
RUN dotnet build "samplebatch.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "samplebatch.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "samplebatch.dll"]