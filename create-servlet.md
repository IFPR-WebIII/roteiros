## Exemplo de Servlet (sem auxílio de editores ou IDE's)

A criação de um projeto Java para web deve seguir uma estrutura, que segue uma especificação bem definida. 
Criar essa estrutura sem apoio de uma IDE's só tem sentido para fins acadêmicos.


A estrutura de uma aplicação JAVA para web, de acordo com a especificação.

1 - O Servlet: a classe java que manipula as rquisições HTTP;
2 - Descritor de implementação web.xml . Arquivo informando como o webapp deve ser interagido como o padrão de url
3 - Arquivo jar do servlet – Este é o jar manipulando a mágica da interação com a web para o servlet.

Estrutura do webapp

O aplicativo da web requer alguma estrutura básica para criar nosso servlet simples ou qualquer outro grande.

A parte mais importante será a do diretório WEB-INF onde serão listadas as classes compiladas finais. É uma boa prática listar as classes e bibliotecas necessárias para o aplicativo da web nesta pasta

  META-INF
  WEB-INF
  –web.xml
  –classes
  –lib
  —-javax.servlet-api-3.1.0.jar
  src
  –com
  —-gullele
  ——simple
  ——–LightServlet.java

Etapas para criar um servlet simples
1. Vá em frente e baixe a API do servlet aqui . Procure por download e pegue o jar

2. Crie a estrutura de diretório acima na pasta simple-servlet.

3. Adicione o seguinte no arquivo web.xml


  <!DOCTYPE web-app PUBLIC
    "-//Sun Microsystems, Inc.//DTD Web Application 2.3//EN"
    "http://java.sun.com/dtd/web-app_2_3.dtd" >
   
   <web-app>
     <display-name>Simple Servlet Webapp</display-name>
     <servlet>
       <servlet-name>simpleservlet</servlet-name>
       <servlet-class>com.gullele.simple.LightServlet</servlet-class>
    </servlet>
  
    <servlet-mapping>
      <servlet-name>simpleservlet</servlet-name>
      <url-pattern>/show</url-pattern>
    </servlet-mapping>
  </web-app>
O descritor acima informa que quando você clicar em localhost:8080/simpleservlet/show, ele seguirá para o LightServlet e fornecerá o conteúdo.

4. Adicione o seguinte conteúdo em LightServlet.java


   package com.gullele.simple;
   
   import javax.servlet.http.HttpServlet;
   import javax.servlet.http.HttpServletRequest;
   import javax.servlet.http.HttpServletResponse;
   import java.io.PrintWriter;
   import java.io.IOException;
   
   public class LightServlet extends HttpServlet {
  
      public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException  {
          PrintWriter writer = response.getWriter();
          writer.println("hey");
      }
  }
Este é o código que seria chamado quando você clicar em /show em seu navegador. Como você pode ver, a maioria das importações vem do arquivo jar que você baixou e outras são do arquivo java.io.

Ele simplesmente imprimirá hey quando você clicar em localhost:8080/simple/show mais tarde, quando terminar de compilar e implantá-lo no servidor web tomcat.

5. Agora tudo deve estar bem, assumindo que você seguiu tudo corretamente. A próxima parte é compilar o projeto e garantir que nenhum problema esteja acontecendo.

Estando em sua pasta raiz, ou seja, um servlet simples, execute o seguinte

javac -classpath WEB-INF/lib/javax.servlet-api-3.1.0.jar src/com/gullele/simple/LightServlet.java -d WEB-INF/classes

O comando acima diz ao java para compilar javaco servlet e usar o arquivo jar que baixamos durante a compilação. E o -d dirá onde colocar os arquivos de classe para uso. Se não for fornecido, por padrão, o diretório atual é usado.

Agora nosso simples exemplo de servlet está pronto para ser empacotado como war

6. Execute o seguinte comando para obter o arquivo war – web archive

jar -cvf simple-servlet.war *

Apenas certifique-se de incluir o arquivo inteiro por enquanto. No caso real, você não precisa do arquivo java real e outras coisas. Mas, por enquanto, você pode adicionar todos. O arquivo de guerra final espera as pastas META-INFe WEB-INF.

Agora você tem o arquivo war para poder implantá-lo no servidor da Web de sua escolha, como o Tomcat.
