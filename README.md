# Pacote basico de infra Resgistry + Gateway

passos -> baixar -> import existing maven project -> run as java app os 2

-> http://localhost:8761 -> carrega e gateway up -> OK

-> http://localhost:8761/eureka/apps

-> http://localhost:8005 -> 404 quando sem rotas OK

-> ORDEM -> Registry -> Gateway -> restante

-> Para novos serviços:

-> 1. depencias no springInitalizer -> Eureka Discovery Client

-> 2. dentro do novo serviço application.properties

exemplo:

server.port=8001 <br>

spring.application.name=EXEMPLO-SERVICE <br>

eureka.client.register-with-eureka=true <br>
eureka.client.fetch-registry=true <br>
eureka.client.service-url.defaultZone=http://localhost:8761/eureka/ <br>
eureka.instance.hostname=localhost <br>

-> cada um com uma porta e nome correto

-> 3. alterar rotas no gateway .properties, os nomes em maiusculo DEVEM SER IGUAIS

spring.cloud.gateway.server.webflux.routes[0].id=EXEMPLO-SERVICE <br>
spring.cloud.gateway.server.webflux.routes[0].uri=lb://EXEMPLO-SERVICE <br>
spring.cloud.gateway.server.webflux.routes[0].predicates[0]=Path=/exemplos/** <br>

-> 4. programar o resto das funcionalidades do serviço

-> 5. Test Restman:

requisição direta <br>
GET http://localhost:8001/exemplos 

requisição gateway <br>
GET http://localhost:8005/exemplos 

Content-Type <br>
application/json <br>

notas adicionais <br>
atenção com os tipos diferentes de serviços novos:

Cenário A — Serviço com persistência em banco de dados que consulta outro microsserviço
- Dependências: Spring Web, Eureka Discovery Client, Lombok, Spring Data JPA, H2 Database, Spring Cloud LoadBalancer.
- Equivalente no gabarito: acoes-service.
- Classe principal: @Bean + @LoadBalanced + RestTemplate.

Cenário B — Serviço que consulta uma API externa, sem persistência
- Dependências: Spring Web, Eureka Discovery Client, Lombok.
- Equivalente no gabarito: cotacoes-service.
- Classe principal: @Bean + RestTemplate

quando for classe com h2 -> atualizar .properties com as coisas de banco, copiar de acoes-service

Arquivo	e Anotações típicas

Application.java	@SpringBootApplication, @Bean, @LoadBalanced <br>
Controller.java	@RestController, @RequestMapping, @Autowired, @GetMapping, @PostMapping, @RequestBody <br>
Service.java	@Service, @Autowired <br>
Repository.java	@Repository <br>
Model.java	@Entity, @Id, @GeneratedValue, @Column, Lombok <br>
DTO.java	Lombok <br>

verificar o verisionamento no .pom, para 3.5.6, já que o Initializr gera a 4.0 <br>
no caso mudar:

#<version>3.5.6</version> <br>

#<properties>
    <java.version>21</java.version>
    <spring-cloud.version>2025.0.3</spring-cloud.version>
#</properties>
