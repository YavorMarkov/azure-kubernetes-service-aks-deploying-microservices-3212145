# Install dependencies and build the source code
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Run the app
FROM node:16-alpine AS runner
WORKDIR /app
ENV NODE_ENV production
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm install --omit=dev

USER node

EXPOSE 3000

ENV PORT 3000

CMD ["npm", "start"]


# # Install dependencies and build the source code
# FROM node:16-alpine AS builder
# WORKDIR /app
# COPY package*.json ./  # Copy package.json and package-lock.json to the working directory
# RUN npm ci  # Install the dependencies using npm ci (clean install)
# COPY . .  # Copy the entire application to the working directory
# RUN npm run build  # Build the source code

# # Run the app
# FROM node:16-alpine AS runner
# WORKDIR /app
# ENV NODE_ENV production  # Set the NODE_ENV environment variable to "production"
# COPY --from=builder /app/dist ./dist  # Copy the /app/dist directory from the builder stage to the runner stage
# COPY --from=builder /app/package*.json ./  # Copy package.json and package-lock.json to the working directory
# RUN npm install --omit=dev  # Install only production dependencies, excluding dev dependencies

# USER node  # Set the user to run the container with non-root privileges

# EXPOSE 3000  # Expose port 3000

# ENV PORT 3000  # Set the environment variable PORT to 3000

# CMD ["npm", "start"]  # Run the command "npm start" when the containe