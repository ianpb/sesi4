FROM node:14

WORKDIR /api
COPY package.json .
RUN npm install express sequelize mysql2 body-parser cors dotenv --save 
COPY . .
CMD [ "node", "server.js" ]

#FROM node:14
#COPY package.json /api/
#WORKDIR /api
#RUN npm install
#ENV PATH /api/node_modules/.bin:$PATH

#COPY . /api/app/
#WORKDIR /api/app/
#CMD [ "node", "/api/app/server.js" ]
