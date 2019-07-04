FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["Veritas.csproj", ""]
RUN dotnet restore "Veritas.csproj"
COPY . .
WORKDIR "/src/"
RUN dotnet build "Veritas.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Veritas.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Veritas.dll"]