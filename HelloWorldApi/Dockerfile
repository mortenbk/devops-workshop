FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["HelloWorldApi.csproj", "HelloWorldApi/"]
RUN dotnet restore "HelloWorldApi/HelloWorldApi.csproj"
COPY . .
WORKDIR "/src/HelloWorldApi"
RUN dotnet build "HelloWorldApi.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "HelloWorldApi.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "HelloWorldApi.dll"]