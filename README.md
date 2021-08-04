# ms-course-configs
Configurações remotas e centralizadas do projeto https://github.com/frabelovix/ms-course/tree/docker , do curso Microsserviços Java com Spring Boot e Spring Cloud - Prof. Nelio Alves


# Criar rede para rodar os serviços

docker network create hr-net

# Subir os bancos Postgress

docker run -p 5432:5432 --name hr-worker-pg12 --network hr-net -e POSTGRES_PASSWORD=1234567 -e POSTGRES_DB=db_hr_worker postgres:12-alpine

docker run -p 5432:5432 --name hr-user-pg12 --network hr-net -e POSTGRES_PASSWORD=1234567 -e POSTGRES_DB=db_hr_user postgres:12-alpine


# Subir servidor de configuração usando as configurações deste repositório

docker run -p 8888:8888 --name hr-config-server --network hr-net -e GITHUB_USER=frabelovix -e GITHUB_PASS= hr-config-server:v1


# Subir Eureka server

docker run -p 8761:8761 --name hr-eureka-server --network hr-net hr-eureka-server:v1


# Subir hr-worker, hr-user e hr-payrool (Portas dinâmicas)

docker run -P --network hr-net hr-worker:v1

docker run -P --network hr-net hr-user:v1

docker run -P --network hr-net hr-payroll:v1


# Subir o servidor de autorização

docker run -P --network hr-net hr-oauth:v1


# Subir o servço do api gateway zuul

docker run -p 8765:8765 --name hr-api-gateway-zuul --network hr-net hr-api-gateway-zuul:v1

