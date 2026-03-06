FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 5173
# Vite cần flag --host để nhận request từ ngoài container
CMD ["npm", "run", "dev", "--", "--host"]