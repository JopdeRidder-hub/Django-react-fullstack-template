# Use the official Node.js image as a base
FROM node:18-alpine

# Set the working directory inside the container
WORKDIR /app

# Install pnpm globally
RUN npm install -g pnpm

# Copy package.json and pnpm-lock.yaml to the container
COPY package.json pnpm-lock.yaml* ./

# Install application dependencies
RUN pnpm install

# Copy the rest of the application source code to the container
COPY . ./

# Build the application
RUN pnpm run build

# Expose the port that the app will run on
EXPOSE 3000

# Serve the built application using Vite's preview command
CMD ["pnpm", "preview", "--host"]
