### Objetivo
 - Entender um pouco mais sobre o ecossistema de java web com o framework Spring boot
 - Projeto para controle de estacionamento (vaga de estacionamento parking spot baseado nos projetos da Michelli Brito no Youtube)
 - Contexto: Condominio, moradores possuem Vagas fixas de acordo com o apartamento, cada morador cadastra um veiculo
   - Veiculo: placa (licensePlateCar), modelo, cor, marca, registro do cadastro do veiculo no sitema de controle
   - apartamento/bloco: identificador (numeros e letras)
   - Vaga: numero da vaga (parkingSpotNumber): campo unico, não nulo e letras enumeros

### Pré- requisitos
 - Java JDK >= 17
 - PostgresSQL
 - Postman/Insomnia

### Tecnologias
- IntelliJ IDEA (JetBrains) + Debug
- https://start.spring.io/ (Initializr) / Mavem (gerenciador de dependências) -> pom.xml (https://github.com/YagoLopesMartins/parkingspotcontrolapispring/blob/main/pom.xml)
- Java 17 and Jakarta EE 9
- Spring Boot 3:
  - Web MVC: Restful, Tomcat, MVC
  - Data JPA:
    - Java Persistence API (abstração/especificação de mapeamento objeto-relaional, consultas e apis de interações com a base de dados) and Hibernate (implementação) que utiliza o JDBC (conexões e transações)
    - Annotations: 
  - PostgreeSQL Driver: SQL
  - Validation: para testar endpoints (não nulo, strings vazias, duplicados etc)
  - Hateoas: Documentação API (hipermidias, modelo RESTful navegabilidade entre os recursos) extends representationModel
  - JUnit

### Princiapais funcionalidades
- API RESTful - modelo de maturidade (https://rivaildojunior.medium.com/modelo-de-maturidade-de-richardson-para-apis-rest-8845f93b288)
  - Http methods semantica (GET, POST, DELETE, PATCH, PUT) e retornos adequados
  - recursos bem definidos (substantivo)
  - Navegabilidade entre os recursos (manutenção)
- MVC (estruturado em pacotes)
  - ParkingModel: (atributos e metódos getter and setter)
    - Serializable para JVM
    - Annotation: @Entity @Table @Id @ GeneratedValue
  - ParkingController:
    - Annotation: @RestController,  @Autowired, @PostMapping, @RequestBody @Valid, @GetMapping, @CrossOrigin
    - Injeção de dependência: ponto (@Autowired) atributo global ParkingRepository  (2 formas d ecriar injeção de depencia, 1 com @autowired e outra via construtor)
    - POST
      - method: saveParking()
      - Recebe um parkingRecordDTO
      - Faz o parser (mapeamento) BeanUtils DTO -> Model
      - retona status CREATED e aciona o repository no metodo save
    - GET
      - method: listAllParkings() "/parkings/{id}"
        - retorna http status com o body repository method findAll()
      - method: getOneParking()
        - Recebe um id de busca
        - Acessa a base se o id existe com Optional
        - Se não existir retona NOT_FOUND
        - Se encontrar retorna status OK e o aprking pesquisado
    - PUT
        - Recebe um id de busca
        - Acessa a base se o id existe com Optional
        - Se não existir retona NOT_FOUND
        - Se encontrar transforma o objeto em model e retorna status OK echama o method save
    - DELETE
        - Recebe um id de busca
        - Acessa a base se o id existe com Optional
        - Se não existir retona NOT_FOUND
        - Se encontrar retorna status OK echama o method delete  
- DateTime format (config) @Configuration @Bean @Primary
- Paginação: @PageableDefault
      
  - ParkingRecordDTO: record (pattern) imutaveis (uma vez criado não pode ser mais alterado)
    - Annotation: @NotBlanck @NotNull
  - ParkingRepository: interface para o banco de dados o qual o JPA se encarrega de manipular com alguns metodos prontos exemplo save (CRUD API)
    - Annotation: @Repository
  - ParkingService: 
    - Annotation: @Service
    - Injeção de dependência:  final ParkingRepository  com o construtor da classe recebendo essa dependencia (duas formas de criar a injeção, 1 com @autowired e outra via construtor)
    - Criar uma interface para melhorar a usabilidade!

### Descrição
- File: application.properties: Conexão com o banco de dados (https://github.com/YagoLopesMartins/parkingspotcontrolapispring/blob/main/src/main/resources/application.properties)
- Controller->Service->Repository

### Como utilizar
- Clone the repository
- Configure banco de dados, se LOCAL
  - sudo -u postgres psql
  - CREATE DATABASE nome_do_banco;
- Executar projeto e acessar no navedagor a url: http://localhost:8080/
- Para testar todas as requisições usar Insominia ou Postman e importe o arquivo x do diretorio Y
 

### Tarefas a fazer (melhorias)
- Inserir testes (unitários e integrados)
- Inserir filtros API (paginação etc)
- Relacionamentos
- Implementar camada service junto ao controlador (regra de negocio)
- Customizar mensagens de erros
- Deploy no Render ou AWS ou GPC
- Docker
- CI/CD (Github actions) Pipelines
- Segurança (spring security, ex.: Bearer Token, Basic, OAuth2 etc)
