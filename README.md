Treinamento Web Services RESTful e Spring

Cada aula é representada por um commit que está identificado com o nome/número da aula.

<b>Aula 2.1</b> - Criando o projeto
- Criação do projeto: https://start.spring.io/

<b>Aula 2.2</b> - Modelando nosso primeiro recurso
- Criamos uma classe LivrosResources e anotamos com @RestController 
- Criamos um método chamado listar que retorna uma String (“Livro 1, Livro 2”)
- Mapeamos esse método com @RequestMapping(value=”/livros”, method=RequestMethod.GET).

<b>Aula 2.3</b> - Criando uma representação para o recurso Livro
- Criamos uma classe chamada Livro e uma classe chamada Comentario que é um dos atributos de Livro.
- Alteramos o método listar da classe LivrosResources fazendo com que o seu retorno agora seja "List<Livro>" e alteramos a implementação para retornar uma lista com dois livros com o nome preenchido.

<b>Aula 2.4</b> - Utilizando a anotação @JsonInclude
- Alteramos a classe Livro inserido acima de cada atributo a anotação @JsonInclude(Include.NON_NULL) para suprimir o campo do JSON retornado caso o valor seja nulo

<b>Aula 2.5</b> - Interagindo com banco de dados
- Altermos o pom.xml adicionando as seguintes dependências:

		<dependency>
		    <groupId>org.springframework.boot</groupId>
		    <artifactId>spring-boot-starter-data-jpa</artifactId>
		</dependency>
		
		<dependency>
		    <groupId>com.h2database</groupId>
		    <artifactId>h2</artifactId>
		    <scope>runtime</scope>
		</dependency>
		
		<dependency>
		    <groupId>org.springframework.boot</groupId>
		    <artifactId>spring-boot-devtools</artifactId>
		    <version>1.3.5.RELEASE</version>
		</dependency>

- Ao adicionar a dependencia do H2 e subir a aplicação agora é possível acessar o console do H2 na seguinte URI:

	http://localhost:8080/h2-console		

- No console que será mostrado, altere o campo "JDBC URL" para "jdbc:h2:mem:testdb" onde "testdb" é o banco de dados definido pelo Spring Boot para ser o banco de dados de teste

- Na classe Livro anotamos com @Entity, o atributo id com @Id e @GeneratedValue(strategy = GenerationType.IDENTITY) e o atributo comentarios com @Transient (por enquanto ficará assim).

- Criamos uma interface "LivrosRepository" que extende JpaRepository e injetamos essa interface na classe "LivrosResources" alterando a implementação do método listar para utilizar esse repository.

<b>Aula 2.6</b> - Salvando o recurso Livro a partir de um POST

- Criamo o método salvar na classe "LivrosRepository" e mapeamos o recurso com sendo "/livros" com Http Method POST.
- Mudamos a anotação @RequestMapping para a classe retirando dos médotos o mapeamento "/livros"

<b>Aula 2.7</b> - Buscando um livro com o uso da anotação @PathVariable

- Criamos o método buscar na classe "LivrosRepository" e mapeamos o recurso com sendo "/livros/{id}" com o Http Method GET

<b>Aula 2.8</b> - Deletando o recurso Livro com o DELETE

- Criamos o método remover na classe "LivrosRepository" e mapeamos o recurso com sendo "/livros/{id}" om o Http Method DELETE

<b>Aula 2.9</b> - PUT para atualizar o recurso Livro

- Criamos o método atualizar na classe "LivrosRepository" e mapeamos o recurso com sendo "/livros/{id}" om o Http Method PUT