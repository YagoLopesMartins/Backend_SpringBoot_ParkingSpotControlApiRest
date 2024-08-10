### Objetivo
 - Entender um pouco mais sobre o ecossistema de java web com o framework Spring boot
 - Projeto para controle de estacionamento (vaga de estacionamento parking spot)

### Pré- requisitos
 - Java JDK >= 17
 - PostgresSQL

### Tecnologias
- IntelliJ IDEA (JetBrains)
- https://start.spring.io/ (Initializr) / Mavem (gerenciador de dependências) -> pom.xml (https://github.com/YagoLopesMartins/parkingspotcontrolapispring/blob/main/pom.xml)
- Java 17 and Jakarta EE 9
- Spring Boot 3:
  - Web MVC: Restful, Tomcat, MVC
  - Data JPA: Java persistence API and Hibernate
  - PostgreeSQL Driver: SQL
  - Validation: 
  - Hateoas:

### Princiapais funcionalidades
- API RESTful - modelo de maturidade (https://rivaildojunior.medium.com/modelo-de-maturidade-de-richardson-para-apis-rest-8845f93b288)
- MVC (estruturado em pacotes)
  - ParkingModel: (atributos e metódos getter and setter)
    - Serializable para JVM
    - Annotation: @Entity @Table @Id @ GeneratedValue
  - ParkingController:
    - Annotation: @RestController
    - Injeção de dependência: ponto (@Autowired) atributo global ParkingRepository
   
      
  - ParkingRecordDTO: record (pattern) imutaveis (uma vez criado não pode ser mais alterado)
    - Annotation: @NotBlanck @NotNull
  - ParkingRepository: interface para o banco de dados o qual o JPA se encarrega de manipular com alguns metodos prontos exemplo save (CRUD API)
    - Annotation: @Repository

### Descrição
- File: application.properties: Conexão com o banco de dados (https://github.com/YagoLopesMartins/parkingspotcontrolapispring/blob/main/src/main/resources/application.properties)

### Como utilizar
- Clone the repository

### Tarefas a fazer
- Inserir testes
- Deploy no Render ou AWS ou GPC
- Docker
- CI/CD
