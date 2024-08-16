FROM node

# Set working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application files
COPY . /app

# Expose the port on which the app will run
EXPOSE 80

# Run the application
CMD ["node", "server.js"]

