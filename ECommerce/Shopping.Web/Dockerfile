#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Shopping.Web/Shopping.Web.csproj", "Shopping.Web/"]
RUN dotnet restore "Shopping.Web/Shopping.Web.csproj"
COPY . .
WORKDIR "/src/Shopping.Web"
RUN dotnet build "Shopping.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Shopping.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Shopping.Web.dll"]