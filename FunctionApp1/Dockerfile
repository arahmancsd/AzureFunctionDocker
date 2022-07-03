# FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
# RUN apt-get update
# RUN apt-get -y install curl gnupg
# RUN curl -fsSL https://deb.nodesource.com/setup_14.x | bash -
# RUN apt-get -y install nodejs
# RUN npm i -g azure-functions-core-tools@4 --unsafe-perm true
# RUN apt-get install -y unzip
# RUN curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l ~/vsdbg


# FROM mcr.microsoft.com/azure-functions/dotnet:3
FROM mcr.microsoft.com/dotnet/sdk:6.0 as build
EXPOSE 80
RUN apt-get update
RUN apt-get -y install curl gnupg
RUN curl -fsSL https://deb.nodesource.com/setup_14.x | bash -
RUN apt-get -y install nodejs
RUN npm i -g azure-functions-core-tools@4 --unsafe-perm true
RUN apt-get install -y unzip
RUN curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l ~/vsdbg
RUN apt-get update && apt-get install -y coreutils
WORKDIR /src
COPY ["FunctionApp1.csproj", "FunctionApp1/"]
RUN dotnet restore "FunctionApp1/FunctionApp1.csproj"
COPY . .
WORKDIR "/src/FunctionApp1"
RUN cat "host.json"
ENTRYPOINT ["func", "host", "start", "--verbose"]
# dotnet watch msbuild /t:RunFunctions
ENV AzureWebJobsScriptRoot=/home/site/wwwroot \
    AzureFunctionsJobHost__Logging__Console__IsEnabled=true