FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["CoreMVCSampleApp/CoreMVCSampleApp.csproj", "CoreMVCSampleApp/"]
RUN dotnet restore "CoreMVCSampleApp/CoreMVCSampleApp.csproj"
COPY . .
WORKDIR "/src/CoreMVCSampleApp"
RUN dotnet build "CoreMVCSampleApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CoreMVCSampleApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreMVCSampleApp.dll"]