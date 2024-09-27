# Use a specific Debian version to avoid potential issues with 'latest'
FROM debian:bullseye

# Set the working directory
WORKDIR /usr/src/app

# Install necessary packages
RUN apt-get update && \
    apt-get install -y ca-certificates git curl

# Add Yarn's GPG key
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -

# Add Yarn's repository
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Install Yarn
RUN apt-get update && \
    apt-get install -y yarn

# Clean up to reduce image size
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*

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
