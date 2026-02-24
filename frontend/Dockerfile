# Stage 1: Build the Angular app
FROM node:18-alpine AS build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
# We use --output-path=dist to ensure we know exactly where the files go
RUN npx ng build --output-path=dist

# Stage 2: Serve with Nginx
FROM nginx:stable-alpine
# Copy everything from the dist folder created in the previous stage
COPY --from=build-stage /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]