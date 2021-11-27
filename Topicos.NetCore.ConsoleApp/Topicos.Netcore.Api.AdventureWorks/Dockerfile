FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 35080

ENV ASPNETCORE_URLS=http://+:35080

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["Topicos.Netcore.Api.AdventureWorks.csproj", "./"]
RUN dotnet restore "Topicos.Netcore.Api.AdventureWorks.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Topicos.Netcore.Api.AdventureWorks.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Topicos.Netcore.Api.AdventureWorks.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Topicos.Netcore.Api.AdventureWorks.dll"]
