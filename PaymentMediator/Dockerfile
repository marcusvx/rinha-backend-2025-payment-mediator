#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["PaymentMediator.csproj", "."]
RUN dotnet restore "./PaymentMediator.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "PaymentMediator.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PaymentMediator.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PaymentMediator.dll"]
