FROM mcr.microsoft.com/dotnet/aspnet:8.0-bookworm-slim AS base
WORKDIR /app
EXPOSE 80/tcp
EXPOSE 443/tcp

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# WORKDIR /src/elsa-studio/src/hosts/Elsa.Studio.Host.Wasm/
# COPY ./elsa-studio/src/hosts/Elsa.Studio.Host.Wasm/Elsa.Studio.Host.Wasm.csproj .
# RUN dotnet restore "Elsa.Studio.Host.Wasm.csproj"

WORKDIR /src/elsa-studio
COPY ./elsa-studio .
WORKDIR /src/elsa-studio/src/hosts/Elsa.Studio.Host.Wasm
RUN dotnet build "Elsa.Studio.Host.Wasm.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Elsa.Studio.Host.Wasm.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Elsa.Studio.Host.Wasm.dll"]
