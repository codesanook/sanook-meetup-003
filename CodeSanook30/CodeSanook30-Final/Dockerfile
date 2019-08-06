FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-stretch AS build
WORKDIR /src
COPY ["CodeSanook30-Final/CodeSanook30-Final.csproj", "CodeSanook30-Final/"]
RUN dotnet restore "CodeSanook30-Final/CodeSanook30-Final.csproj"
COPY . .
WORKDIR "/src/CodeSanook30-Final"
RUN dotnet build "CodeSanook30-Final.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CodeSanook30-Final.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CodeSanook30-Final.dll"]