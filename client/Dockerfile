# Base Image
FROM node:14-alpine AS build
#Container will run from the following location
WORKDIR /usr/src/app
#Copy package-lock.json-dependancies
COPY package*.json ./
#Run npm Install into the container from the image
RUN npm install
#Copy from local directory into what our image should contain
COPY . .
# As demonstrated on the Readme we  need to run npm run build
RUN npm run build
#With reference to the initial build stage
FROM node:14-alpine
WORKDIR /usr/src/app
#copy optimized from build stage
COPY --from=build /usr/src/app ./
#Expose port: 3000 to local host:3000 after npm start command
EXPOSE 3000
#Run application
CMD ["npm", "start"]