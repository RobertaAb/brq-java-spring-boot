# Tutorial 

Este tutorial destina-se aos workshops sobre tecnologias

* Maven
* Json
* Rest
* Java
* Spring MVC
* Spring Boot

## Criando nosso primeiro projeto Maven

Vamos criar um projeto utilizando a ferramenta de linha de comando do maven. Este projeto terá sua estrutura com base no arquétipo de inicio rápido que nos dara uma classe para App e um caso de teste AppTest.

```
mvn archetype:generate  \
-DgroupId=com.brq.digital.workshop  \
-DartifactId=maven-simple-example \
-DarchetypeArtifactId=maven-archetype-quickstart  \
-DinteractiveMode=false
```

Agora, acessamos a pasta criada, `cd maven-simple-example`, e executamos uma limpeza no projeto, utilizando `mvn clean`, o goal `clean`, apaga a pasta target, que contém todos os arquivos gerados durante o ciclo de vida de build.

Apõs o processo de limpeza, vamos executar `mvn package`, que serã responsável por gerar o pacote de acordo com a configuração do `pom.xml`.

No caso de sucesso o nosso pacote estára compilado e disponível para execução.

```
java -cp target/maven-simple-example-1.0-SNAPSHOT.jar com.brq.digital.workshop.App
```

Como vimos, o nosso pacote foi corretamente compilado, mas não estará disponível para ser utilizado pelos demais projetos que poderemos contruir para utilizá-lo. Para instalar ele em nosso repositório local, na pasta `.m2`, precisaremos utilizado os seguinte comando: `mvn install`.

O maven disponibiliza um comando que gera uma documentação em html. Podemos utilizar o comando `mvn site`, que disponibilizará esse conteúdo na pasta `target/site`, que poderá ser acessado via browser.

## Criando um projeto múltiplo


### Criando o projeto parent

Quando montamos uma arquitetura "foda", e desejamos que todo projeto tenha acesso as componentes que fazem parte dela, podemos criar um projeto parent, do tipo POM, que será responsáveis por fornecer aos projetos filhos todas as dependências necessárias para gerar a estrutura.

Vamos criar esse projeto parent da seguinte forma.

```
mvn archetype:generate \
-DarchetypeGroupId=org.codehaus.mojo.archetypes \
-DarchetypeArtifactId=pom-root \
-DarchetypeVersion=RELEASE \
-DgroupId=com.brq.digital.workshop \
-DartifactId=simple-parent
```

include

```
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.3.RELEASE</version>
		<relativePath />
	</parent>
```


```
    <dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>org.mockito</groupId>
			<artifactId>mockito-core</artifactId>
			<scope>test</scope>
		</dependency>

		<dependency>
			<groupId>org.jmockit</groupId>
			<artifactId>jmockit</artifactId>
			<version>1.33</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
```		

```
	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>
```

```
	<plugin>
		<groupId>org.apache.maven.plugins</groupId>
		<artifactId>maven-compiler-plugin</artifactId>
		<version>${maven-compiler-plugin.version}</version>
		<inherited>true</inherited>
		<configuration>
			<source>1.8</source>
			<target>1.8</target>
		</configuration>
	</plugin>
```

```
	<plugin>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-maven-plugin</artifactId>
	</plugin>
```

```
mvn archetype:generate  \
-DgroupId=com.brq.digital.workshop  \
-DartifactId=book-rest \
-DarchetypeArtifactId=maven-archetype-quickstart  \
-DinteractiveMode=false 
```

`delete App.java`

`delete AppTest.java`

create Application.java

create HelloController.java

create HelloControllerTest.java

```
mvn archetype:generate  \
-DgroupId=com.brq.digital.workshop  \
-DartifactId=book-service \
-DarchetypeArtifactId=maven-archetype-quickstart  \
-DinteractiveMode=false 
```

```
mvn archetype:generate -DgroupId=com.brq.digital.workshop \
-DartifactId=book-app \
-DarchetypeArtifactId=maven-archetype-webapp \
-DinteractiveMode=false
```

`mvn eclipse:eclipse -Dwtpversion=2.0`

create Application

update web.xml
