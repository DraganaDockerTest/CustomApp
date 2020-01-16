FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 5000
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["CustomApp.csproj", "./"]
RUN dotnet restore "./CustomApp.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "CustomApp.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "CustomApp.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CustomApp.dll"]