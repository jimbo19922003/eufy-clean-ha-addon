# Use an official Node.js runtime as a parent image
FROM node:16-alpine

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and yarn.lock to the container
COPY package.json yarn.lock ./

# Install app dependencies
RUN yarn

# Copy the rest of the application code
COPY . .

# Compile TypeScript to JavaScript
RUN yarn build

# Expose port if necessary (adjust if your app uses a specific port)
EXPOSE 3131

# Define environment variables for email and password
ENV EUFY_EMAIL="jimbo19922003@gmail.com"
ENV EUFY_PASSWORD="Done2Day!"

# Start the application (adjust the start command if necessary)
CMD ["node", "dist/main.js"]
