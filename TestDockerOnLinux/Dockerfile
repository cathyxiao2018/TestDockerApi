FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["TestDockerOnLinux/TestDockerOnLinux.csproj", "TestDockerOnLinux/"]
COPY ["TestDockerOnLinux.Domain/TestDockerOnLinux.Domain.csproj", "TestDockerOnLinux.Domain/"]
COPY ["TestDockerOnLinux.Repository/TestDockerOnLinux.Repository.csproj", "TestDockerOnLinux.Repository/"]
COPY ["TestDockerOnLinux.Core/TestDockerOnLinux.Core.csproj", "TestDockerOnLinux.Core/"]
RUN dotnet restore "TestDockerOnLinux/TestDockerOnLinux.Api.csproj"
COPY . .
WORKDIR "/src/TestDockerOnLinux"
RUN dotnet build "TestDockerOnLinux.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestDockerOnLinux.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestDockerOnLinux.Api.dll"]