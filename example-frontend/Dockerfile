FROM node:16

# Ensure useradd is available
RUN apt-get update && apt-get install -y passwd

# 1) Work in /app
WORKDIR /app

# 2) Copy package files and install dependencies (as root)
COPY package*.json ./
RUN npm install

# 3) Copy the rest of the code
COPY . .

# 4) Print Node.js and npm versions (for debugging)
RUN node -v
RUN npm -v

# 5) Build the frontend
ENV REACT_APP_BACKEND_URL=http://localhost:8080/
RUN npm run build

# 6) Install `serve` globally so we can serve the build
RUN npm install -g serve

# 7) Create a non-root user (named `appuser`), then chown /app
RUN useradd -m appuser
RUN chown -R appuser:appuser /app

# 8) Switch to the new user
USER appuser

# 9) Expose port 5000 (where we plan to serve the build)
EXPOSE 5000

# 10) Serve the static files
CMD ["serve", "-s", "-l", "5000", "build"]

# start with `docker build -t example-frontend .` and `docker run -p 3000:5000 example-frontend`