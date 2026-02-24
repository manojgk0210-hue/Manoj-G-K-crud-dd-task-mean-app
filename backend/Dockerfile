# Use official Node.js runtime as a parent image
FROM node:18-alpine

# Set the working directory in the container
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application code
COPY . .

# Your backend runs on port 8080 (standard for many tutorials, adjust if needed)
EXPOSE 8080

# Command to run the application
CMD ["node", "server.js"]