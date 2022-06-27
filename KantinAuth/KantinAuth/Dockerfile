FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["KantinAuth/KantinAuth.csproj", "KantinAuth/"]
RUN dotnet restore "KantinAuth/KantinAuth.csproj"
COPY . .
WORKDIR "/src/KantinAuth"
RUN dotnet build "KantinAuth.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "KantinAuth.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "KantinAuth.dll"]
