FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["CodeSanook21-Final/CodeSanook21-Final.csproj", "CodeSanook21-Final/"]
RUN dotnet restore "CodeSanook21-Final/CodeSanook21-Final.csproj"
COPY . .
WORKDIR "/src/CodeSanook21-Final"
RUN dotnet build "CodeSanook21-Final.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CodeSanook21-Final.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CodeSanook21-Final.dll"]