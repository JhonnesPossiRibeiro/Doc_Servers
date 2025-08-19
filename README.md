# Doc_Servers
Documentação para configuração de servidores


## Configurando IIS para Django (Python)

### Preparando o ambinte
Para que o projeto em Django (Python) rode no servidor, precisamos instalar algumas dependências listadas abaixo:

1. Instar o Python:
   * a) Efetuar o download do Python: https://www.python.org/downloads;
   * b) Instalar o Python no servidor, de preferência apontar a pasta de instalação para c:/Python;
   * c) Efetuar o download do HttpPlatformHandler: https://www.iis.net/downloads/microsoft/httpplatformhandler;
   * d) Instalar o HttpPlatformHandler, instalação padrão;
   * e) Instalar Ferramentas de Desenvolvedor C++, caso seja necessário baixe o exe do visual studio: https://visualstudio.microsoft.com/pt-br/free-developer-offers;
   * f) Instalar o Oracle Client 64bit, caso seja necessário verifique a versão do banco e baixe no site da oracle: https://www.oracle.com/br/database/technologies/instant-client/winx64-64-downloads.html;
   * g) Efetue o download da Redistribuição C++ 2013: https://www.microsoft.com/en-us/download/details.aspx?id=40784;
   * h) Instalar o pacote da Redistribuição C++ 2013, instalação padrão.

### Criar um site:
Para criar um site no IIS para backend em Django (Python) siga os passos abaixo:

1. Botão direito do mouse sobre o **Sites**, escolha a opção **Add WebSites**;
2. Informe um nome para o site **Site name**;
3. A **Application pool** será criada com o mesmo nome do site;
4. Em **Physical path** selecione a pasta em que ficará o código fonte do projeto;
5. Em **Binding** em **Type** escolha o protocolo, em **Port** informe uma porta para o site;
6. Caso escolher o protocolo **https** informe o **Host name**. Obs: em conjunto com o time de infra, gerar um certificado, o **Host name** será o mesmo informado para o certificado;
7. Em **SSL certificate** informe o certificado intalado no servidor para o protocolo https;
8. Confirme a criação em "OK".


