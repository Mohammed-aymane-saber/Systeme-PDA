# frontend/Dockerfile
FROM node:18

# Set working directory
WORKDIR /app

# Install dependencies first (cached layer)
COPY package*.json ./
RUN npm install

# Copy app files
COPY . .

# Start React dev server (hot-reload)
CMD ["npm", "start"]

EXPOSE 9000