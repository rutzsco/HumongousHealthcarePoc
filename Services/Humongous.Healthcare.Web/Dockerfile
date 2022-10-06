#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Humongous.Healthcare.Web.csproj", "."]
RUN dotnet restore "./Humongous.Healthcare.Web.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "Humongous.Healthcare.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Humongous.Healthcare.Web.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Humongous.Healthcare.Web.dll"]