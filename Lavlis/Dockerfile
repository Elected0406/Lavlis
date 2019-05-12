FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["Lavlis/Lavlis.csproj", "Lavlis/"]
RUN dotnet restore "Lavlis/Lavlis.csproj"
COPY . .
WORKDIR "/src/Lavlis"
RUN dotnet build "Lavlis.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Lavlis.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Lavlis.dll"]