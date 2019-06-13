FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY MyTest/MyTest.csproj MyTest/
RUN dotnet restore MyTest/MyTest.csproj
COPY . .
WORKDIR /src/MyTest
RUN dotnet build MyTest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish MyTest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MyTest.dll"]
