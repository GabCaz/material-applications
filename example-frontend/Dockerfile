FROM node:16

# Set working directory inside container
WORKDIR /app

# Copy package.json and package-lock.json for better caching
COPY package*.json ./

# Install dependencies
RUN npm install


# Copy rest of the frontend source code
COPY . .

# Print Node.js and npm versions (for debugging)
RUN node -v
RUN npm -v

# Build the frontend
ENV REACT_APP_BACKEND_URL http://localhost:8080/
RUN npm run build


# 8️⃣ Install `serve` globally to serve static files
RUN npm install -g serve

# Expose the port the app runs on
EXPOSE 5000

# Serve the static files
CMD ["serve", "-s", "-l", "5000", "build"]

# start with `docker build -t example-frontend .` and `docker run -p 3000:5000 example-frontend`