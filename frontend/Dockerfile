FROM node:18-alpine

WORKDIR /app

# Copy everything
COPY . .

# Install dependencies
RUN npm install

EXPOSE 3000

# Run in dev mode (faster, no build needed)
CMD ["npm", "run", "dev"]