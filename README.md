version: "3.9"
services:
  mongodb:
    image: naveenreddy369/mongodb:v1
    container_name: mongodb
  catalogue:
    image: naveenreddy369/catalogue:v1
    container_name: catalogue
    depends_on:
      - mongodb
  web:
    image: naveenreddy369/web:v1
    container_name: web
    ports:
      - "80:80"
    depends_on:
      - catalogue
      - user
      - cart
      - mysql
      - shipping
  redis:
    image: redis
  user:
    image: naveenreddy369/user:v1
    container_name: user
    depends_on:
      - mongodb
      - redis
  cart:
    image: naveenreddy369/cart:v1
    container_name: cart
    depends_on:
      - redis
      - catalogue
  mysql:
    image: naveenreddy369/mysql:v1
    container_name: mysql
  shipping:
    image: naveenreddy369/shipping:v1
    container_name: shipping
    depends_on:
      - mysql
  rabbitmq:
    image: rabbitmq
    container_name: rabbitmq
  payment:
    image: naveenreddy369/payment:v1
    container_name: payment
    depends_on:
      - rabbitmq
  ratings:
    image: naveenreddy369/ratings:v1
    container_name: ratings
    depends_on:
      - mysql
networks:
  roboshop:
    driver: bridge# Below code will download the images from the dockerhub and create the containers.
# docker-compose.yaml
