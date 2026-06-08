FROM node:18-alpine
WORKDIR /app
COPY *.json ./
RUN npm install
COPY . .
EXPOSE 5000
CMD ["node","server.js"]