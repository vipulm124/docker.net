FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["DockerHelloWorld/DockerHelloWorld.csproj", "DockerHelloWorld/"]
RUN dotnet restore "DockerHelloWorld/DockerHelloWorld.csproj"
COPY . .
WORKDIR "/src/DockerHelloWorld"
RUN dotnet build "DockerHelloWorld.csproj" -c Release -o /app/build


FROM build As publish
RUN dotnet publish "DockerHelloWorld.csproj" -c Release -o /app/publish


FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerHelloWorld.dll"]