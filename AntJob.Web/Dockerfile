FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["AntJob.Web/AntJob.Web.csproj", "AntJob.Web/"]
COPY ["AntJob.Data/AntJob.Data.csproj", "AntJob.Data/"]
COPY ["AntJob/AntJob.csproj", "AntJob/"]
RUN dotnet restore "AntJob.Web/AntJob.Web.csproj"
COPY . .
WORKDIR "/src/AntJob.Web"
RUN dotnet build "AntJob.Web.csproj" -c Release -o /app/build
FROM build AS publish
RUN dotnet publish "AntJob.Web.csproj" -c Release -o /app/publish
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AntWeb.dll"]