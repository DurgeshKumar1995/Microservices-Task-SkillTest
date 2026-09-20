FROM node:22-slim
WORKDIR /app/product-service
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3001
CMD ["node", "app.js"]