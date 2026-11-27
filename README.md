# Pacote basico de infra Resgistry + Gateway

passos -> baixar -> import existing maven project -> run as java app os 2

-> http://localhost:8761 -> carrega e gateway up -> OK

-> http://localhost:8761/eureka/apps

-> http://localhost:8005 -> 404 quando sem rotas OK

-> ORDEM -> Registry -> Gateway -> restante

-> Para novos serviços:

-> 1. depencias no springInitalizer -> Eureka Discovery Client

-> 2. server.port=8001

spring.application.name=EXEMPLO-SERVICE

eureka.client.register-with-eureka=true
eureka.client.fetch-registry=true
eureka.client.service-url.defaultZone=http://localhost:8761/eureka/
eureka.instance.hostname=localhost

