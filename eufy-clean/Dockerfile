FROM debian:bullseye

# Set the working directory
WORKDIR /usr/src/app

# Install dependencies
RUN apt-get update && \
    apt-get install -y ca-certificates curl gnupg git && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | gpg --dearmor -o /usr/share/keyrings/yarnkey.gpg && \
    echo "deb [signed-by=/usr/share/keyrings/yarnkey.gpg] https://dl.yarnpkg.com/debian/ stable main" > /etc/apt/sources.list.d/yarn.list && \
    curl -fsSL https://deb.nodesource.com/setup_16.x | bash -
    
RUN apt-get update && \
    apt-get install -y nodejs yarn && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Clone the eufy-clean repository
RUN git clone https://github.com/martijnpoppen/eufy-clean.git /usr/src/app/eufy-clean

# Set the working directory to the cloned repository
WORKDIR /usr/src/app/eufy-clean

# Check contents of the directory and attempt to install dependencies
RUN ls -al /usr/src/app/eufy-clean && \
    yarn install --verbose

# Build the application if applicable
# Add this if there's a build script in package.json
RUN yarn build



# Expose the necessary port
EXPOSE 3131

# Command to run the application
CMD ["node", "./build/index.js"]
