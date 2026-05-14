FROM node:20 AS ui-build

WORKDIR /usr/src/app

COPY client/package*.json ./client/
WORKDIR /usr/src/app/client

RUN npm install

COPY client/ .

RUN npm run build


FROM node:20 AS server-build

WORKDIR /usr/src/app

COPY nodeapi/package*.json ./nodeapi/
WORKDIR /usr/src/app/nodeapi

RUN npm install

COPY nodeapi/ .


FROM node:20

WORKDIR /usr/src/app

COPY --from=server-build /usr/src/app/nodeapi/ ./
COPY --from=ui-build /usr/src/app/client/dist ./client/dist

EXPOSE 4200
EXPOSE 5000

CMD ["npm", "start"]