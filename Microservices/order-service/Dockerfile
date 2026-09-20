FROM node:22-slim
WORKDIR /app/order-service
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3002
CMD ["node", "app.js"]