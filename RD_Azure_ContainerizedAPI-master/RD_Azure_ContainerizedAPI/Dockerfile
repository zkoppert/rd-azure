#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["RD_Azure_ContainerizedAPI/RD_Azure_ContainerizedAPI.csproj", "RD_Azure_ContainerizedAPI/"]
RUN dotnet restore "RD_Azure_ContainerizedAPI/RD_Azure_ContainerizedAPI.csproj"
COPY . .
WORKDIR "/src/RD_Azure_ContainerizedAPI"
RUN dotnet build "RD_Azure_ContainerizedAPI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RD_Azure_ContainerizedAPI.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RD_Azure_ContainerizedAPI.dll"]