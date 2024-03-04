# Tutorial: Seu primeiro aplicativo Java EE
Este tutorial descreve como criar uma aplicação web  usando Java Enterprise Edition (Java EE) no IntelliJ IDEA. A aplicação incluirá uma única página JSP que mostra `Hello, World!`e um link para um servlet Java que também mostra `Hello, World!`.

Este tutorial te orientará a criar um novo projeto Java EE usando o modelo de aplicativo da web, informando ao IntelliJ IDEA onde seu **servidor de aplicações** está localizado e, em seguida, usará uma configuração de execução para construir o artefato, iniciar o servidor e implementar o artefato nele.

Aqui está o que você precisa:

 - [**IntelliJ IDEA Ultimate**](https://github.com/IFPR-WebIII/roteiros/blob/main/licenca_estudante_jetbrains.md)
 - **Java SE Development Kit (JDK) versão 11 ou posterior**

> Você pode obter o JDK diretamente do IntelliJ IDEA conforme descrito no [Java Development Kit (JDK)](https://www.jetbrains.com/help/idea/sdk.html#jdk) ou fazer download e instalá-lo manualmente, por exemplo: [Oracle JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html) ou [OpenJDK](https://openjdk.java.net/) .

 - **Apache Tomcat**: o servidor de aplicativos [Tomcat](http://tomcat.apache.org/) versão 10 ou posterior.

> Este tutorial usa JDK 17, Jakarta EE 10 e Tomcat 10.1. Para obter mais informações sobre a compatibilidade entre outras versões do Tomcat, Java e Jakarta EE, consulte [https://tomcat.apache.org/ whichversion.html](https://tomcat.apache.org/whichversion.html) .

 - **Navegador da Web**: Você precisará de um navegador da web para visualizar seu aplicativo da web.

### Crie um novo projeto Java Enterprise﻿

O IntelliJ IDEA inclui um assistente dedicado para criar projetos Java Web. Neste guia, criaremos uma aplicação web simples:

**1.**  No menu principal, vá em Arquivo | Novo | Projeto, ou Novo Projeto caso esteja na tela inicial.

**2.**  Na caixa de diálogo Novo Projeto , selecione Jakarta EE.
    
**3.**  Informe um nome para o seu projeto:  `JavaEEHelloWorld`.
    
**4.**  Selecione o modelo "Web application",  Maven  como ferramenta de construção e selecione Java 17 como [SDK](https://www.jetbrains.com/help/idea/sdk.html) para o projeto. Nesse guia testei com sucesso a versão Jetbrains Runtime Version 17.0.7  

**5.**  Não selecione nenhum servidor de aplicação, faremos isso mais adiante.

![enter image description here](https://resources.jetbrains.com/help/img/idea/2023.3/java_enterprise_new_project_step_1_web.png)
    
Clique em **Próximo** para continuar.
    
**5.**  No campo Versão , selecione Jakarta EE 10 porque é com ele que o Tomcat 10.1 usado neste tutorial é compatível.
    
>Para Tomcat 9, selecione Java EE 8 . Para Tomcat 10, selecione Jakarta EE 9.1 .
    
Na lista Dependências , você pode ver que o modelo de aplicativo da web inclui apenas a estrutura do Servlet em Especificações .

![enter image description here](https://resources.jetbrains.com/help/img/idea/2023.3/java_enterprise_new_project_step_2_web_jakarta_10.png)    

    
2.  Clique em **Criar** .
    

### Explore a estrutura padrão do projeto﻿

O IntelliJ IDEA cria um projeto que já traz um código padrão de exemplo, permitindo construir e implantar com o projeto. Sua estrutura de pasta também é criada de acordo com as especificações da JEE. O principais arquivos criados para esse projeto são:

-   **pom.xml**: é arquivos de configurações do projeto com informações que inclui as configuração do Maven (no gerenciador de implantação e dependências), incluindo dependências e plug-ins necessários para implantar o projeto. Você pode encontrar esse arquivo na raiz do projeto.
    ```
    pom.xml
    ```
-   **index.jsp** é a página inicial do seu aplicativo que abre quando você acessa o URL do diretório raiz. Ele renderiza `Hello World!`e um link para `/hello-servlet`. Você pode encontrar esse arquivo em:
    
    ```
    src/main/webapp/index.jsp
    ```
    
-   A classe **`HelloServlet`** estende (herda) `HttpServlet`e é anotada com `@WebServlet`. Ele processa solicitações para a URL `/hello-servlet`: uma solicitação GET retorna código HTML que é renderizado `Hello World!`. Você pode encontrar esse arquivo em:
    
    ```
    src/main/java/com/example/JavaEEHelloWorld/HelloServlet.java
    ```
    
Use a janela de ferramentas **`Projeto`** para navegar e abrir arquivos em seu projeto ou pressione **`Ctrl+Shift+N`** e digite o nome do arquivo.

### Configurar o servidor Tomcat

Informe ao IntelliJ IDEA onde o servidor de aplicativos Tomcat está localizado (Você já deve ter baixado).

**1**.  No menu principal, vá em Executar (Run) | Editar configurações.    

![enter image description here](https://raw.githubusercontent.com/IFPR-WebIII/roteiros/main/imagens/config_server_1.png)

**2**.  Clique em Adicionar Novo e selecione **`Tomcat Server > Local`**. **Cuidado para não selecionar TomcatEE server**.
    
**3**.  Em Servidor de Aplicação, clique em configurar e especifique o caminho para o local onde foi baixado servidor Tomcat. O IntelliJ detecta e define o nome e a versão adequadamente.
![enter image description here](https://raw.githubusercontent.com/IFPR-WebIII/roteiros/main/imagens/config_server_2.png)

    
### Criar uma configuração de execução﻿

O IntelliJ IDEA precisa de uma configuração de execução para construir os artefatos e implantá-los em seu servidor.

**2**.  Na janela em que está, verifique que existe a seguinte mensagem:

![enter image description here](https://resources.jetbrains.com/help/img/idea/2023.3/rest_ws_glassfish_run_config_warning.png)
    
 Clique em corrigir. Você precisará corrigir o seguinte:
    
**2**.  Na guia Implementação , adicione o artefato que você deseja implementar:`JavaEEHelloWorld:war exploded`

**3**. No  campo **`Contexto de Aplicação`** mude a URL se desejar. Caso não mude, a URL do seu projeto parecerá com algo como:  
        
   ```http://localhost:8080/JavaEEHelloWorld_war_exploded/```
    
   
**4**. Clique em **OK** para salvar a configuração de execução.
    
6.  Procure em sua IDEA o botão de play ![enter image description here](https://resources.jetbrains.com/help/img/idea/2023.3/app.expui.run.run.svg) ou pressione `Alt+Shift+F10` e selecione a configuração do servidor criada. Depois de seleciona, `Shift+F10` já irá executar seu projeto.
        
A configuração de execução que fizemos agora cria os artefatos, inicia o servidor Tomcat e implementa os artefatos no servidor. Você deverá ver a saída correspondente na janela da ferramenta Serviços .

![Servidor Tomcat iniciado e aplicativo implantado na janela da ferramenta Serviços](https://resources.jetbrains.com/help/img/idea/2023.3/rest_ws_tomcat_run_tool_window.png "Servidor Tomcat iniciado e aplicativo implantado na janela da ferramenta Serviços")

Feito isso, o IntelliJ IDEA abre o URL especificado em seu navegador.

![Saída do aplicativo implantado no navegador da web](https://resources.jetbrains.com/help/img/idea/2023.3/rest_ws_tomcat_web_browser_output.png "Saída do aplicativo implantado no navegador da web")

Caso contrário, tente abrir o URL você mesmo: [JavaEEHelloWorld_war_exploded](JavaEEHelloWorld_war_exploded)

### Modifique sua Aplicação

Sempre que você alterar o código-fonte do aplicativo, poderá reiniciar a configuração de execução para ver as alterações. Mas isso nem sempre é necessário, principalmente quando não é possível reiniciar o servidor (por exemplo, quando um sistema já estiver online e não puder ser parado). A maioria das alterações são pequenas e não exigem a reconstrução dos artefatos, a reinicialização do servidor e assim por diante. Vamos alterar a página JSP da aplicação.

1.  Abra index.jsp e altere a saudação de `Hello, World!` para `A better greeting`.
    
2.  Clique no botão  ![O botão Atualizar aplicativo](https://resources.jetbrains.com/help/img/idea/2023.3/app-client.expui.javaee.updateRunningApplication.svg "O botão Atualizar aplicativo")ou pressione `Shift+F10`.
    
3.  Na caixa de diálogo Atualizar , selecione Atualizar recursos (update resources) porque a página JSP é um recurso estático. Clique **OK**.
    
4.  Atualize o URL do aplicativo em seu navegador. Você deverá ver agora a frase: `A better greeting.`
    
## Solução de problemas﻿

Tivemos alguns problemas para criação do projeto em aula. De forma geral, listo aqui alguns desses problemas e sua solução:

 - **As pasta webapp não aparece:** você pode ter selecionado o modelo errado no momento de criar o projeto. Será necessário criar um novo projeto.
 - **Ao clicar em `fix`, nas configurações do servidor, não aparecem as opções para criação do artefato automaticamente:** esse problema ocorre, de forma geral, devido a incompatibilidade entre as versões do Java e do Tomcat. Ainda que seja possível reconfigurar as propriedade do projeto, pode ser um pouco trabalhoso. Minha sugestão é recriar o projeto novamente com as configurações descritas nesse guia. Testei com diversos computadores e Sistemas operacionais e todos funcionaram.
 - **O projeto não é executado ao clicar em play (1):** por algum motivo (versões, permissões e etc) o Maven não é adicionado ao projeto é necessário manualmente clicar com o botão direito sobre o arquivo `pom.xml`  e selecionar a opção **Add Maven support to an existing project**. Se essa opção não aparece, não é esse o problema.
 - **O projeto não é executado ao clicar em play (2): ** Se estiver usando Linux, isso pode ser problemas de permissão. Caso a pasta `webapps` encontrada dentro da pasta do Tomcat não tenha permissão de escrita e execução por outros, o Intellij não poderá implantar automaticamente o projeto. Dê permissão a essa pasta.

