FROM mcr.microsoft.com/dotnet/sdk:6.0-alpine as build
WORKDIR /app

COPY src/MyWeb/*.csproj src/MyWeb/MyWeb.csproj
RUN  dotnet restore src/MyWeb

COPY src/MyWeb src/MyWeb
RUN dotnet publish src/MyWeb -c Release -o out

FROM mcr.microsoft.com/dotnet/aspnet:6.0-alpine as runtime
WORKDIR /app

ENV TZ='Asia/Bangkok'
RUN apk add --no-cache tzdata

COPY --from=build /app/out ./

ENTRYPOINT [ "dotnet", "MyWeb.dll" ]