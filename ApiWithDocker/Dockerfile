FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

ENV ASPNETCORE_URLS=http://+:5000

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ApiWithDocker.csproj", "./"]
RUN dotnet restore "ApiWithDocker.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "ApiWithDocker.csproj" -c Release -o /app/build

FROM build as publish
RUN dotnet publish "ApiWithDocker.csproj" -c Release -o /app/publish

FROM base as final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ApiWithDocker.dll"]
