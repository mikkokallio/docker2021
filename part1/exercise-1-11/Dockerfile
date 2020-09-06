FROM node:current-slim
WORKDIR /usr/src/app
ENV FRONT_URL=http://192.168.99.100:5000
COPY package.json .
RUN npm install
EXPOSE 8000
CMD [ "npm", "start" ]
COPY . .