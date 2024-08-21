FROM node:14

WORKDIR /app

COPY package.json .

RUN npm install 

COPY . .

# server.js app.listen(3000);
EXPOSE 3000

CMD ["node", "server.js"]

