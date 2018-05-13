FROM microsoft/aspnetcore-build:2.0 AS build-env
WORKDIR /app
RUN git clone git://github.com/v1996-96/kms.git .
COPY appsettings.json .
RUN dotnet restore
RUN dotnet publish -c Release -o dist

FROM microsoft/aspnetcore:2.0
RUN apt-get update && apt-get install -y wget

ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
    && rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

WORKDIR /app
COPY --from=build-env /app/dist .
EXPOSE 5000
ENTRYPOINT ["dockerize", "-wait", "tcp://database:5432", "dotnet", "kms.dll"]