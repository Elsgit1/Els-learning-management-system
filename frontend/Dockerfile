# Stage 1: Compile and Build angular codebase

# Use official node image as the base image
FROM node:20-bullseye-slim as build

# Set the working directory
WORKDIR /usr/local/app

# Add the source code to app
COPY ./ /usr/local/app/

# Clean npm cache
RUN npm cache clean --force

# Install all the dependencies
RUN npm install

# Generate the build of the application
RUN npm run build


# Stage 2: Serve app with nginx server

# Use official nginx image as the base image
FROM nginx:1.27.1

# Copy the nginx configuration file to replace the default one
COPY /.nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy the build output to replace the default nginx contents.
COPY --from=build /usr/local/app/dist/utoronto /usr/share/nginx/html

# Expose port 80
EXPOSE 80
