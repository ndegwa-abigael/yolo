# Base Image
FROM node:14-alpine 
#Container will run from the following location
WORKDIR /usr/src/app
#Copy package-lock.json-dependancies
COPY package*.json ./
#Run npm Install into the container from the image
RUN npm install
#Copy from local directory into what our image should contain
COPY . .
#Expose port: 5000 to local host:5000 after npm start command
EXPOSE 5000
#Run application
CMD ["npm", "start"]