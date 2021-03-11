# ==========================
# To Build with Docker Desktop: 
# docker build -t react .
# ==========================

# ==========================
# Builder Stage
# ==========================
FROM public.ecr.aws/bitnami/node:14.16.0 as builder

# Set a work directory
WORKDIR /app
ENV PATH /app/node_modules/.bin:$PATH

# Copy over the 
COPY package.json .
COPY ./yarn.lock .

RUN yarn --silent

COPY . .

RUN yarn build

# ==========================
# Runner Stage
# ==========================
FROM public.ecr.aws/nginx/nginx:1.18-alpine

COPY --from=builder /app/build /usr/share/nginx/html

# RUN rm /etc/nginx/conf.d/default.conf

# COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
