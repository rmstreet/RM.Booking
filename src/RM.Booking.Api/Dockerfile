FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["src/RM.Booking.Api/RM.Booking.Api.csproj", "src/RM.Booking.Api/"]
RUN dotnet restore "src/RM.Booking.Api/RM.Booking.Api.csproj"
COPY . .
WORKDIR "/src/src/RM.Booking.Api"
RUN dotnet build "RM.Booking.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "RM.Booking.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RM.Booking.Api.dll"]