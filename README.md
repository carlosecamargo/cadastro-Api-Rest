# cadastro-Api-Rest
Criando cadastro simples utilizando uma Rest/Api
Criando uma Api-Rest-Spring / PROJETO BASE


- projeto MAVEN/JAVA(SPRINGBOOT - ultima Versão)
	-Group - expertostech
	-Artifact - tutorial-rest-api
	-Description - tutorial-rest-api
	-Package name - expertostech.tutorial.rest.api
-
	packaging - jar
	java - 11
...........................................
	dependencias
	- Spring Web
	- Spring data JPA - permite acesso ao banco de dados
	- MySQL Driver - permite acesso ao banco de dados MySql
............
	
...............................Utilizei o INTELJ
Deixar o projeto existente
	- File/New/Module from Existing Sources... 
	- na pasta Projeto, selecione e clique seguir.
		- import module from external model/ Maven - Finish
....
Se já houver um projeto principal ir na pagina principal e adcionar o comando Ctrl+Shift+A
	- digitar no localizador project from existing sources
		- clicar import module from external model/ Maven
.............................

O projeto principal estará dentro da pasta/ main / java / expertostech.tutorial.rest.api / tutorialRestApiApplication
	- quando aparecer a marcação em vermelho, esperar baixar todas as dependencias.
............................

Para criar um pacote Controller/ botão direito no expertostech.tutorial.rest.api / new / Package = nome: expertostech.tutorial.rest.api.controller
	- dentro da pasta controller criar uma classe java / botão direto / expertostech.tutorial.rest.api.controller / new / classeJava /nome: StatusController
/*
package expertostech.tutorial.rest.api.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController - esta dizendo que é uma aplicação REST
public class StatusController {

    @GetMapping(path = "/api/status") //vai dizer que é um metodo que vai ser executado quando houver uma requesição. 
    public String check(){
        return "online";
    }
}
*/ JPA é o cmponente do java que executa coexão com o banco de dados.


...............
TODA ALTERAÇÂO QUE REALIZO NO PROJETO VOU NO MENU MAVEN E FAÇO o RELOAD ALL MAVEN PROJECTS
-
A PORTA 8080 é e a porta oficial do TOMCAT
..............

- Para Criar um usuario para esse projeto
 	Para criar um pacote Model(que é nosso modelo dados)/ botão direito no expertostech.tutorial.rest.api / new / Package = nome: expertostech.tutorial.rest.api.model
	- dentro da pasta Model criar uma classe java / botão direto / expertostech.tutorial.rest.api.model / new / classeJava /nome: UsuarioModel


/*
package expertostech.tutorial.rest.api.model;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity(name = "usuario")  // podemos dizer que essa classe é um entidade de banco de dados, para desabilitar a seleção verde/ file / Settings / digitar Spelling / configure Spelling e desabilita todas as caixas do Proofreading.
public class UsuarioModel {

    @Id //criar as anotações para dizer que os atributos são campos de banco de dados.
    public Integer codigo; // criar os Gets e Sets - botão direito Generate/ clicar Gets e Sets e selecionar todos os atributos criados.

    @Column(nullable = false, length = 50) // dizer que é uma coluna e que não pde ser falsa e campo é limitado 50
    public String  nome;

    @Column(nullable = false, length = 10)
    public String login;

    @Column(nullable = false, length = 10)
    public String senha;

    public Integer getCodigo() {
        return codigo;
    }

    public void setCodigo(Integer codigo) {
        this.codigo = codigo;
    }

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public String getLogin() {
        return login;
    }

    public void setLogin(String login) {
        this.login = login;
    }

    public String getSenha() {
        return senha;
    }

    public void setSenha(String senha) {
        this.senha = senha;
    }
}
*/
..............

- Para Criar um Repositorio para esse projeto
 	Para criar um pacote Repository/ botão direito no expertostech.tutorial.rest.api / new / Package = nome: expertostech.tutorial.rest.api.repository
	- dentro da pasta Repository criar uma interface / botão direto / expertostech.tutorial.rest.api.Repository / new / classeJava /nome: UsuarioRepository

/*
package expertostech.tutorial.rest.api.repository;

import expertostech.tutorial.rest.api.model.UsuarioModel;
import org.springframework.data.repository.CrudRepository;

public interface UsuarioRepository extends CrudRepository<UsuarioModel, Integer> { //necessario criar um crud  para fazer as conexões para banco de dados
}
*/

- dentro da pasta controller criar uma classe java / botão direto / expertostech.tutorial.rest.api.controller / new / classeJava /nome: UsuarioController
/*

package expertostech.tutorial.rest.api.controller;

import com.sun.xml.bind.v2.runtime.reflect.Lister;
import expertostech.tutorial.rest.api.model.UsuarioModel;
import expertostech.tutorial.rest.api.repository.UsuarioRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController 
public class UsuarioController {

    @Autowired  
    private UsuarioRepository repository;

    @GetMapping(path = "/api/usuario/{codigo}") // para conseguir fazer acesso ao banco de dados
    public ResponseEntity consultar(@PathVariable("codigo") Integer codigo){ // criar metodo de consulta

        return repository.findById(codigo) // metodo que já vem no repositorio por padrão
                .map(record -> ResponseEntity.ok().body(record)) // se por acaso ele retorna alguma coisa, vai montar o corpo da requisição com registro
                .orElse(ResponseEntity.notFound().build()); // caso contrario vai retornar um notFaund e fazer o build
    }

    @PostMapping(path = "/api/usuario/salvar")// preciso dizer que um metodo post 
    public UsuarioModel salvar(@RequestBody UsuarioModel usuario){ // salvar dizendo que um requestBody
        return repository.save(usuario);
    }

}
*/"
..............................................
 PARA CONFIGURAR MEU BANCO DE DADOS VOU NA PASTA / MAIN / RESOURCE / application.properties

/*
spring.datasource.url=jdbc:mysql://localhost:3306/mysql?useTimezone=true&serverTimezone=UTC
spring.datasource.username=dev
spring.datasource.password=!Lipebia9

spring.jpa.hibernate.ddl-auto=update
*/

...................................................................

APOS IMPLEMENTADO ABRIR O POSTMAN PARA TESTAR O API REST SPRINGBOOT


+ / GET / localhost:8080/api/status
+ / POST/ localhost:8080/api/usuario/salvar - body/raw / JSON
	{
		"codigo": 1,
		"nome": "Maria da Silva",
		"login": "maria",
		"senha": "123"
	}
	- Send
+ /GET/localhost:8080/api/1 // consulta com codigo 1
				

