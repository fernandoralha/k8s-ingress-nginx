# Application Docker file Configuration
# Visit https://docs.docker.com/engine/reference/builder/
# Using multi stage build

# Prepare the image when build
# also use to minimize the docker image
FROM node:20-alpine as builder

WORKDIR /app
COPY package*.json ./
COPY tsconfig.json ./
RUN npm install
COPY . .
RUN npm run build


# Build the image as production
# So we can minimize the size
FROM node:20-alpine

WORKDIR /app
COPY package*.json ./
COPY tsconfig.json ./
ENV PORT=4000
ENV NODE_ENV=Production
RUN npm install
COPY --from=builder /app/dist ./dist
EXPOSE ${PORT}

CMD ["npm", "run", "start"]



# FROM node:20-alpine As development

# WORKDIR /app

# COPY package*.json ./

# RUN npm install --legacy-peer-deps --only=development

# COPY . .

# RUN npm run build

# FROM node:20-alpine as production

# ARG NODE_ENV=production
# ENV NODE_ENV=${NODE_ENV}

# WORKDIR /app

# COPY package*.json ./

# RUN npm install --legacy-peer-deps --only=production

# COPY . .

# COPY --from=development /app/dist ./dist

# CMD ["node", "dist/main"]