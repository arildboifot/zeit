FROM microsoft/dotnet:2.1-sdk-alpine AS build
WORKDIR /app

# copy csproj and restore as distinct layers
#COPY *.sln .
COPY web/*.csproj ./web/
RUN dotnet restore web

# copy everything else and build app
COPY web/. ./web/
WORKDIR /app/web
RUN dotnet publish -c Release -o out


FROM microsoft/dotnet:2.1-aspnetcore-runtime-alpine AS runtime
WORKDIR /app
COPY --from=build /app/web/out ./
ENTRYPOINT ["dotnet", "zeit.dll"]