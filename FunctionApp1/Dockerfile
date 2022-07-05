# FROM mcr.microsoft.com/azure-functions/dotnet:3 as base
FROM mcr.microsoft.com/dotnet/sdk:6.0
RUN apt-get update
RUN apt-get -y install curl gnupg
RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get -y install nodejs
RUN npm i -g azure-functions-core-tools@4 --unsafe-perm true
RUN apt-get install -y unzip
RUN curl -sSL https://aka.ms/getvsdbgsh | /bin/sh /dev/stdin -v latest -l ~/vsdbg
# RUN apt-get update && apt-get install -y coreutils
RUN apt-get install -y tini
WORKDIR /src
COPY ["FunctionApp1.csproj", "FunctionApp1/"]
RUN dotnet restore "FunctionApp1/FunctionApp1.csproj"
WORKDIR "/src/FunctionApp1"
# COPY . .
# ENTRYPOINT ["func", "host", "start", "--verbose"]
# ENTRYPOINT ["func", "host", "start", "--verbose"]
ENTRYPOINT ["/usr/bin/tini","--"]
CMD ["dotnet" ,"watch", "msbuild", "/t:RunFunctions"]