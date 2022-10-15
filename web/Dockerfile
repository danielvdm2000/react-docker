FROM node:16-alpine as build

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

RUN npm run build

FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html/

# --- React-Router 404 fix ---
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d
# --- React-Router 404 fix ---

CMD ["nginx", "-g", "daemon off;"]