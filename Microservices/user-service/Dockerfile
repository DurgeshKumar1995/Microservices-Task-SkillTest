FROM node:22-slim
WORKDIR /app/user-service

COPY package*.json ./
RUN npm install

COPY . .
EXPOSE 3000
CMD ["node", "app.js"]