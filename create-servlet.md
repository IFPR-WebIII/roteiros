
# Exemplo de Servlet (sem auxílio de editores ou IDE's)

A criação de um projeto Java para web deve seguir uma estrutura, que segue uma especificação bem definida. 
Criar essa estrutura sem apoio de uma IDE's só tem sentido para fins acadêmicos.


A estrutura de uma aplicação JAVA para web, de acordo com a especificação.

 - **O Servlet:** a classe java que manipula as rquisições HTTP; 
 - **Descritor de implementação web.xml** . Arquivo informando como o webapp deve ser interagido como o padrão de url 
 - **Arquivo jar do Servlet** – Este é o jar manipulando a mágica da interação com a web para o servlet.

## Estrutura do webapp

Um aplicativo web requer uma estrutura fundamental. A parte mais importante será a do diretório WEB-INF onde serão listadas as classes compiladas finais. É uma boa prática listar as classes e bibliotecas necessárias para o aplicativo da web nesta pasta.


## Etapas para criar uma aplicação JAVA web - Etapa 1
Crie a estrutura de diretório, conforme orientações abaixo:

	META-INF
	WEB-INF
	– web.xml
	– classes
	– lib
	– – javax.servlet-api-4.1.0.jar
	src
	– com
	–– ifpr
	——– HelloServlet.java

## Etapas para criar uma aplicação JAVA web - Etapa 2

 - Baixe a API do Servlet neste [link](https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api/4.0.1) . Procure por "Files" e selecione o **jar**;
 - Mova o arquivo baixado para a pasta adequada;


##  Etapas para criar uma aplicação JAVA web - Etapa 3

Adicione o  seguinte conteúdo no arquivo web.xml: 
	
<?xml version="1.0" encoding="UTF-8"?>
	<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
	  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	  xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_5_0.xsd"
	  version="5.0">
	  <display-name>Hello Servlet</display-name>

	  <servlet>
	    <servlet-name>helloservlet</servlet-name>
	    <servlet-class>com.ifpr.HelloServlet</servlet-class>
	  </servlet>

	  <servlet-mapping>
	    <servlet-name>helloservlet</servlet-name>
	    <url-pattern>/show</url-pattern>
	  </servlet-mapping>

	</web-app>


O arquivo `web.xml` acima informa que quando você clicar em localhost:8080/<nome_app>/show, ele seguirá para o HelloServlet e "servirá" o conteúdo requisitado.

##  Etapas para criar uma aplicação JAVA web - Etapa 4

Adicione o seguinte conteúdo em HelloServlet.java

```
package com.ifpr;
   
import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloServlet extends HttpServlet {

   public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException  {
       PrintWriter writer = response.getWriter();
       writer.println("hey");
   }
}
```

Este código será executado quando uma requisição for realizada para /show. Simplesmente será impresso **"hey"** quando digitar esse endereço no navegador  

#### Observações 

 - Antes é necessário compilar e implantá-lo no servidor web;
 - Como se pode ver, a maioria das importações vem do arquivo jar que você baixou;

Assumindo que você seguiu tudo corretamente, a próxima etapa é compilar o projeto e garantir que nenhum problema esteja acontecendo.

## Etapas para criar uma aplicação JAVA web - Etapa 5


Estando na pasta raiz da aplicação, execute o seguinte comando:
```
javac -classpath WEB-INF/lib/javax.servlet-api-4.0.1.jar src/com/ifpr/HelloServlet.java -d WEB-INF/classes
```
O comando acima diz ao java para compilar (`javac`) o Servlet e usar o arquivo jar que baixamos durante a compilação. 
A instrução `-d` por sua vez, indicará onde colocar os arquivos de classe para uso futuro. Se não for fornecido, por padrão, o diretório atual é usado.

Agora nosso simples exemplo de Servlet está pronto para ser empacotado como **war**.

## Etapas para criar uma aplicação JAVA web - Etapa 6

Execute o seguinte comando para obter o arquivo war – web archive

`jar -cvf app.war *`

Apenas certifique-se de incluir o arquivo inteiro por enquanto. Cabe mencionar que, em casos não educacionais, você não precisa do arquivo java real e outras coisas.

Agora você tem-se o arquivo **war** para poder implantá-lo no servidor da web de sua escolha, como o Tomcat, por exemplo.
