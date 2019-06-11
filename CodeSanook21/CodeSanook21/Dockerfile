FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["CodeSanook21/CodeSanook21.csproj", "CodeSanook21/"]
RUN dotnet restore "CodeSanook21/CodeSanook21.csproj"
COPY . .
WORKDIR "/src/CodeSanook21"
RUN dotnet build "CodeSanook21.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CodeSanook21.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CodeSanook21.dll"]