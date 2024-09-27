# Use a specific Debian version
FROM debian:bullseye

# Set the working directory
WORKDIR /usr/src/app

# Install curl and ca-certificates
RUN apt-get update && \
    apt-get install -y ca-certificates curl

# Download Yarn's GPG key to a file to check if curl succeeds
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg -o yarn-key.gpg

# Check if the key file is downloaded and not empty
RUN ls -l yarn-key.gpg && cat yarn-key.gpg

# Add Yarn's GPG key from the file
RUN apt-key add yarn-key.gpg

# Add Yarn's repository
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Proceed with installation of yarn
RUN apt-get update && \
    apt-get install -y yarn

# Cleanup
RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Clone the eufy-clean repository
RUN git clone https://github.com/martijnpoppen/eufy-clean.git .

# Install dependencies
RUN yarn install

# Expose the necessary port
EXPOSE 3131

# Command to run the application
CMD ["node", "./build/index.js"]
