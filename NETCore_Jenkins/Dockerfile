FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["NETCore_Jenkins/NETCore_Jenkins.csproj", "NETCore_Jenkins/"]
RUN dotnet restore "NETCore_Jenkins/NETCore_Jenkins.csproj"
COPY . .
WORKDIR "/src/NETCore_Jenkins"
RUN dotnet build "NETCore_Jenkins.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "NETCore_Jenkins.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "NETCore_Jenkins.dll"]