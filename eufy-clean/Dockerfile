# Use an official Node.js runtime as a parent image
FROM node:latest

# Set the working directory
WORKDIR /usr/src/app

# Clone the eufy-clean repository
RUN git clone https://github.com/martijnpoppen/eufy-clean.git .

# Install dependencies
RUN yarn install

# Expose the port the app runs on, if applicable (adjust if necessary)
EXPOSE 3131

# Command to run the application
CMD ["node", "./build/index.js"]  # Replace 'your-app-start-file.js' with the actual start file, if applicable
