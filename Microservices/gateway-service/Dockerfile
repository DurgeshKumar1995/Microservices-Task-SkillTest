FROM node:22-slim
WORKDIR /app/gateway-service

COPY package*.json ./
RUN npm install 
COPY . .
EXPOSE 3003
CMD ["node", "app.js"]