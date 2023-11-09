# Используем официальный образ Nginx
FROM nginx:latest

# Заменяем стандартную страницу Nginx
COPY index.html /usr/share/nginx/html/index.html

# Запускаем Nginx
CMD ["nginx", "-g", "daemon off;"]
