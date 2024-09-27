# Use an official Node.js runtime as a parent image
FROM debian:latest

# Install Git
RUN apt-get update && \
    apt-get install -y git

# Install Yarn
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -y yarn

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
