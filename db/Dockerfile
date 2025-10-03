FROM mysql:5.7
ENV MYSQL_ROOT_PASSWORD=pass@123
ENV MYSQL_DATABASE=facebook
COPY init.sql /docker-entrypoint-initdb.d/
EXPOSE 3306
