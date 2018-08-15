FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 57597
EXPOSE 44319

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Pinboard.API/Pinboard.API.csproj", "Pinboard.API/"]
RUN dotnet restore "Pinboard.API/Pinboard.API.csproj"
COPY . .
WORKDIR "/src/Pinboard.API"
RUN dotnet build "Pinboard.API.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Pinboard.API.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Pinboard.API.dll"]