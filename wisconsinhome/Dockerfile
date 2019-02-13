FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["wisconsinhome/wisconsinhome.csproj", "wisconsinhome/"]
RUN dotnet restore "wisconsinhome/wisconsinhome.csproj"
COPY . .
WORKDIR "/src/wisconsinhome"
RUN dotnet build "wisconsinhome.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "wisconsinhome.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "wisconsinhome.dll"]