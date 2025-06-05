FROM node:21.6.0-alpine3.18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . . 
EXPOSE 8088
CMD ["node", "server.js"]