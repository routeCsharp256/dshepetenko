﻿FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build

WORKDIR .

COPY ["MerchandiseService/MerchandiseService.csproj","MerchandiseService/"] 

RUN dotnet restore "MerchandiseService/MerchandiseService.csproj"

COPY .. .

WORKDIR "MerchandiseService"

RUN dotnet build "MerchandiseService.csproj" -c Release -o /app/build

FROM build AS publish

RUN dotnet publish "MerchandiseService.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:5.0 as runtime

WORKDIR /app
EXPOSE 80

FROM runtime as final
WORKDIR /app

COPY --from=publish /app/publish .

ENTRYPOINT ["dotnet", "MerchandiseService.dll"]
