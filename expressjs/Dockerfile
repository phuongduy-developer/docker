# Comment
FROM node:24

LABEL description="This is expressjs image" \
    version="1.0" \ 
    author="Duy"

WORKDIR /app

COPY package*.json ./

RUN npm i 

RUN npm run build

COPY . .

# ENV APP_NAME='Unicode' \
#     APP_VERSION='1.0' 

EXPOSE 3000

CMD ["npm", "start"]