FROM node:16.18

# Install wget to allow health check to work
RUN apt-get update 
RUN apt-get install -y gcc
RUN apt-get install -y wget

ENV PORT=3000

COPY . /frontend-react-js
WORKDIR /frontend-react-js
RUN npm install
EXPOSE ${PORT}
CMD ["npm", "start"]