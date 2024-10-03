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

# Create the entry point script
RUN echo "const { EufyClean } = require('./build/index.js');" > entrypoint.js && \
    echo "const email = process.env.EUFY_EMAIL;" >> entrypoint.js && \
    echo "const password = process.env.EUFY_PASSWORD;" >> entrypoint.js && \
    echo "async function main() {" >> entrypoint.js && \
    echo "    const eufyClean = new EufyClean(email, password);" >> entrypoint.js && \
    echo "    await eufyClean.init();" >> entrypoint.js && \
    echo "    const allDevices = await eufyClean.getAllDevices();" >> entrypoint.js && \
    echo "    console.log('Connected devices:', allDevices);" >> entrypoint.js && \
    echo "    const deviceConfig = { deviceId: 'your-device-id' };" >> entrypoint.js && \
    echo "    const device = await eufyClean.initDevice(deviceConfig);" >> entrypoint.js && \
    echo "    await device.connect();" >> entrypoint.js && \
    echo "    await device.setCleanParam({ cleanType: 'MOP_ONLY', cleanExtent: 'NARROW', mopMode: 'HIGH' });" >> entrypoint.js && \
    echo "    await device.sceneClean(10);" >> entrypoint.js && \
    echo "}" >> entrypoint.js && \
    echo "main().catch(err => {" >> entrypoint.js && \
    echo "    console.error('Error initializing EufyClean:', err);" >> entrypoint.js && \
    echo "    process.exit(1);" >> entrypoint.js && \
    echo "});" >> entrypoint.js

# Expose the necessary port
EXPOSE 3131

# Command to run the application
CMD ["node", "./entrypoint.js"]
