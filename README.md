# Doc_Servers
Documentação para configuração de servidores


## Configurando IIS para Django (Python)

### Preparando o ambiente
Para que o projeto em Django (Python) rode no servidor, precisamos instalar algumas dependências listadas abaixo:

1. Instalar o Python:
   * a) Efetuar o download do Python: https://www.python.org/downloads;
   * b) Instalar o Python no servidor, de preferência apontar a pasta de instalação para c:/Python;
2. Instalar o HttpPlatformHandler:
   * a) Efetuar o download do HttpPlatformHandler: https://www.iis.net/downloads/microsoft/httpplatformhandler;
   * b) Instalar o HttpPlatformHandler, instalação padrão;
3. Instalar as Ferramentas de Desenvolvedor C++ 
   * a) Instalar Ferramentas de Desenvolvedor C++, caso seja necessário baixe o exe do visual studio: https://visualstudio.microsoft.com/pt-br/free-developer-offers;
   * b) Instalar o Oracle Client 64bit, caso seja necessário verifique a versão do banco e baixe no site da oracle: https://www.oracle.com/br/database/technologies/instant-client/winx64-64-downloads.html;
4. Instalar a Redistribuição C++ 2013
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

### Projeto Django
Para publicar o projeto siga os passos abaixo:

1. Copiar o **código do projeto Django**, sem a pasta **venv** (ambiente virtual) da máquina local para a pasta do site criado acima;
2. Abrir o **Powershell** como adim na pasta do projeto;
3. Criar o ambiente virtual (.venv): **python -m venv .venv**;
4. Ativar o ambiente virtual (.venv): **.\.venv\Scripts\activate**;
5. Instale as bibliotecas que estão no arquivo de requerimento o requirements.txt rodando o comando: **pip install -r requirements.txt**;
6. Caso apresente erro na instalação dos pacotes, verifique o retorno do erro e instale a parte as pendências;
  * a) Exemplo: ERROR: Cannot install -r requirements.txt (line 25);
  * b) Execute no terminal: pip install "pacote da linha 25 no aquivo requirements.txt";
7. Após isso verificar o arquivo .env pois ele direciona o acesso ao banco que quais URLs podem ser buscar os dados via API:
  * a) Exemplo de arquivo .env:
       ``` AMBIENTE=PROD

       # Caminho no sistema de arquivos para o cache do Django.
       FS_CACHE_LOCATION="D:\inetpub\wwwroot\IntranetBackend\cache\"

       # Para usuário da intranet/aplicação.
       DB_INTRANET_USERNAME=user
       DB_INTRANET_PASSWORD="pass"

       # Para usuário de banco "consinco", usado para obter models.
       DB_CONSINCO_SCHEMA=schema
       DB_CONSINCO_USERNAME=user
       DB_CONSINCO_PASSWORD=pass

       # Configurações gerais do servidor do banco de dados da intranet.
       DB_NAME=orcl
       DB_HOST=xx.xx.x.xx
       DB_PORT=1521

       # Configurações do AD.
       DOMINIO_AD="domain.lan"
       USUARIO_AD_INTRANET="user"
       SENHA_USUARIO_AD_INTRANET="pass"

       # Configurações de domínios das aplicações WEB.

       DOMINIO_DJANGO="site.dominan.lan"
       PORTA_DJANGO="7002"
       DOMINIO_REACT="site.domain.lan"
       PORTA_REACT="3000" ```


