FROM node:current-slim
WORKDIR /usr/src/app
COPY package.json .
RUN npm i
EXPOSE 5000
CMD [ "npm", "start" ]
COPY . .