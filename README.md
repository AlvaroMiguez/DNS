## Tarea DNS

1. Hacer el compose
~~~
services:
  asir_bind9:
    container_name: asir_bind9
    image: internetsystemsconsortium/bind9:9.16
    ports:
      - 53:53
    networks:
      bind9_subnet:
        ipv4_address: 172.28.5.1
    volumes:
      - ./config:/etc/bind
      - ./lib:/var/lib/bind
  asir_cliente:
    container_name: asir_cliente
    image: alpine
    networks:
      - bind9_subnet
    stdin_open: true # docker run -i
    tty: true # docker run -t
    dns:
      - 172.28.5.1 # el contenedor dns server
networks:
  bind9_subnet:
    external: true
~~~
2. Crear la red para el DNS
~~~
docker network create   
    --driver=bridge   
    --subnet=172.28.0.0/16   
    --ip-range=172.28.5.0/24   
    --gateway=172.28.5.254   
bind9_subnet
~~~
3. configurar los archivos
4. docker compose up