# Use Node.js LTS
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm install --production

# Copy source code
COPY . .

# Expose API port
EXPOSE 5000

# Run backend
CMD ["npm", "start"]
