FROM debian:bullseye

# Set the working directory
WORKDIR /usr/src/app

# Install curl and ca-certificates
RUN apt-get update && \
    apt-get install -y ca-certificates curl gnupg

# Download Yarn's GPG key
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg -o /usr/share/keyrings/yarnkey.gpg

# Add Yarn's repository with signed-by option
RUN echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

# Install Yarn
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
