#---Stage-1--Build---
FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .

#--Stage-2---Production---
FROM node:18-alpine
WORKDIR /app
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app ./
ENV NODE_ENV=production
EXPOSE 5001
USER appuser
CMD ["npm", "start"]
