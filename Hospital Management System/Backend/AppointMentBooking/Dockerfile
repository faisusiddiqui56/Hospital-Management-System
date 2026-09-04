FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

# Copy the project file(s) from the repository root into the build context
COPY ["Hospital Management System/Backend/AppointMentBooking/AppointMentBooking.csproj", "AppointMentBooking/"]
RUN dotnet restore "AppointMentBooking/AppointMentBooking.csproj"

# Copy the rest of the backend source and publish
COPY ["Hospital Management System/Backend/AppointMentBooking/", "AppointMentBooking/"]
RUN dotnet publish "AppointMentBooking/AppointMentBooking.csproj" -c Release -o /app/publish

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS runtime
WORKDIR /app

# Bind to the port Render provides via the PORT environment variable
ENV ASPNETCORE_URLS=http://+:${PORT:-5000}

COPY --from=build /app/publish .
EXPOSE 5000
ENTRYPOINT ["dotnet", "AppointMentBooking.dll"]
