FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 8080
ENV ASPNETCORE_URLS=http://+:8080

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["cart.csproj", "./"]
RUN dotnet restore "cart.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "cart.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "cart.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "cart.dll"]
