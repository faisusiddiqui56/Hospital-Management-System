This branch adds Dockerfiles for the frontend (Angular static + nginx) and backend (ASP.NET Core) plus a docker-compose.yml for local testing.

Files added:
- Hospital Management System/Frontend/Dockerfile
- Hospital Management System/Frontend/nginx.conf
- Hospital Management System/Backend/AppointMentBooking/Dockerfile
- docker-compose.yml

Notes:
- The backend Dockerfile listens on the PORT environment variable (ASPNETCORE_URLS) so it works on platforms like Render that inject $PORT.
- The frontend Dockerfile builds the Angular app and serves it with nginx (SPA fallback enabled).
- The docker-compose.yml is for local testing only; update ConnectionStrings__constr and secrets before using in production.

Next steps (recommended):
1. Review the files and adjust any paths or project names if your Angular project outputs to a folder other than dist/Frontend.
2. Push this branch to GitHub (already done by commit) and open a Pull Request to merge into your main branch when ready.
3. On Render:
   - Create a Static Site for the frontend (recommended) using build command:
     bash -lc "cd 'Hospital Management System/Frontend' && (npm ci || npm install) && npm run build"
     and Publish Directory: Hospital Management System/Frontend/dist/Frontend
   - Create a Web Service (Docker) for the backend and point Render to the backend Dockerfile path:
     Hospital Management System/Backend/AppointMentBooking/Dockerfile
   - Set environment variables on Render (ConnectionStrings__constr, Jwt__Key, Jwt__Issuer, Jwt__Audience).

If you want, I can also open a Pull Request for this branch.
