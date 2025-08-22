<h1>Implementando servidores Web IIS para projetos Python</h1>

<p>Documentação para configuração de servidores</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.11-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Oracle-DB-red?style=for-the-badge&logo=oracle&logoColor=white"/>
  <img src="https://img.shields.io/badge/IIS-Server-lightgrey?style=for-the-badge&logo=microsoft&logoColor=white"/>
  <img src="https://img.shields.io/badge/WSL-Enabled-green?style=for-the-badge&logo=linux&logoColor=white"/>
  <img src="https://img.shields.io/badge/Ubuntu-Linux-orange?style=for-the-badge&logo=ubuntu&logoColor=white"/>
  <img src="https://img.shields.io/badge/Redis-Cache-red?style=for-the-badge&logo=redis&logoColor=white"/>
  <img src="https://img.shields.io/badge/Celery-TaskQueue-darkgreen?style=for-the-badge&logo=celery&logoColor=white"/>  
  <img src="https://img.shields.io/badge/NSSM-Services-blueviolet?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Git_Bash-Terminal-orange?style=for-the-badge&logo=git&logoColor=white"/>
  <img src="https://img.shields.io/badge/License-MIT-brightgreen?style=for-the-badge"/>
</p>

## 📌 Status do Projeto  
:warning: **Em desenvolvimento**

## Tópicos
➤ [Configurando IIS para Django (Python)](#configurando-iis-para-django-python)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Preparando o ambiente](#preparando-o-ambiente)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Criar um site](#criar-um-site)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Projeto Django](#projeto-django)  

➤ [Redis](#redis)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Ativar o Wsl no servidor e instalar o Ubuntu](#ativar-o-wsl-no-servidor-e-instalar-o-ubuntu)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Instalando e testando o Redis](#instalando-e-testando-o-redis)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Testando o redis no servidor](#testando-o-redis-no-servidor)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Executando o Redis automaticamente](#executando-o-redis-automaticamente)  

➤ [Nssm](#nssm)   
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Instalando Nssm](#instalando-nssm)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Gerenciando o Nssm](#gerenciando-o-nssm)  

➤ [Celery](#redis)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Celery](#celery)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Instalando o pacote Celery](#instalando-o-pacote-celery)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Configurando o Celery](#configurando-o-celery)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Executando o CeleryWork automaticamente](#executando-o-celeryWork-automaticamente)  

➤ [Github](#github)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Instalando o Git bash](#instalando-o-git-bash)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Configurando o Git bash](#configurando-o-git-bash)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Gerando a chave SSH](#gerando-a-chave-ssh)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Configurando a chave SSH no Github](#configurando-a-chave-ssh-no-**Github**)  
&nbsp;&nbsp;&nbsp;&nbsp;▪ [Testando a conexão do Git bash](#testando-a-conexão-do-git-bash)  

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
3. Criar o ambiente virtual (.venv): ```python -m venv .venv*```;
4. Ativar o ambiente virtual (.venv): ```.\.venv\Scripts\activate```;
5. Instale as bibliotecas que estão no arquivo de requerimento o requirements.txt rodando o comando: ```pip install -r requirements.txt```;
6. Caso apresente erro na instalação dos pacotes, verifique o retorno do erro e instale a parte as pendências;
  * a) Exemplo: ERROR: Cannot install -r requirements.txt (line 25);
  * b) Execute no terminal: ```pip install "pacote da linha 25 no aquivo requirements.txt"```;
7. Após isso verificar o arquivo .env pois ele direciona o acesso ao banco que quais URLs podem ser buscar os dados via API:
  * a) Exemplo de arquivo .env:
       ``` AMBIENTE=PROD

       # Caminho no sistema de arquivos para o cache do Django.
       FS_CACHE_LOCATION="D:\inetpub\wwwroot\IntranetBackend\cache\"

       # Para usuário da intranet/aplicação.
       DB_INTRANET_USERNAME=user
       DB_INTRANET_PASSWORD="pass"

       # Para usuário de banco, usado para obter models.
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
8. Configurar o web.config, seguindo os passos do HttpHandler: https://learn.microsoft.com/pt-br/visualstudio/python/configure-web-apps-for-iis-windows?view=vs-2022.
   * a) Exemplo de web.config:
   ```
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
        <system.webServer>
            <httpPlatform processPath="D:\inetpub\wwwroot\IntranetBackend\venv\Scripts\python.exe" arguments="D:\inetpub\wwwroot\IntranetBackend\manage.py runserver %HTTP_PLATFORM_PORT%" stdoutLogEnabled="true"           stdoutLogFile="D:\inetpub\wwwroot\IntranetBackend\logs\logs">
                <environmentVariables>
                    <environmentVariable name="%HTTP_PLATAFORM_PORT%" value="SERVER_PORT" />
                </environmentVariables>
            </httpPlatform>
            <handlers>
                <add name="Python" path="*.py" verb="*" modules="CgiModule" scriptProcessor="C:\Python\python.exe %s %s" resourceType="File" />
                <add name="handler-python" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" requireAccess="Script" />
            </handlers>
        </system.webServer>
        <appSettings>
            <add key="PYTHONPATH" value="D:\inetpub\wwwroot\IntranetBackend\smy" />
            <add key="WSGI_HANDLER" value="django.core.wsgi.get_wsgi_application()" />
            <add key="DJANGO_SETTINGS_MODULE" value="smy.settings" />
        </appSettings>
    </configuration>
   ```
9. Para testar o projeto Django (Python): ```python manage.py runserver```;
   * a) Caso gere um erro, por exemplo: ModuleNotFoundError: No module named 'decouple', repetir os passos 6-b para instalar as pendências.

## Redis
Link de referência: https://redis.io/blog/redis-on-windows-10.

Para a instalação do Redis no Windows Server 2022, seguir os passos abaixo:

### Ativar o Wsl no servidor e instalar o Ubuntu

1. Abra o **PowerShell** como administrador;
2. Execute o comando: ```Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux``` para instalar o recurso de sub-sistema linux no windows;
3. Reiniciei o servidor para que tenha efeito;
4. Abra o **PowerShell** como administrador;
5. Execute o comando: ```wslconfig``` o Windows irá reconhecer o comando;
6. No **PowerShell** digite o comando: ```wsl --install -d ubuntu``` para baixar a versão do Ubuntu;
7. Após baixar e instalar, execute o comando ```wsl.exe -d Ubuntu```;
8. Crie um usuário;
9. Crie uma senha e confirme.

### Instalando e testando o Redis
Para a instalação do **Redis** siga os passos abaixo:

1. No terminal do Ubuntu execute o comando: ```sudo apt-get update```;
2. Informe a senha;
3. No terminal do Ubuntu execute o comando: ```sudo apt-get upgrade```;
4. Para instalar o redis execute o comando: ```sudo apt-get install redis-server```;
5. Após a instalação verfique a versão: ```redis-cli -v```;
6. Após execute o comando para reiniciar o servidor redis: ```sudo service redis-server restart```;
7. Teste o redis com o comando: ```redis-cli```;
8. Após abrir o server redis, digite: ping, retornará pong.

### Testando o redis no servidor
Para testar a conexão como Redis, siga os passos abaixo:

1. Abrir a pasta c:\Meu_Teste_Redis no VsCode;
2. Cria um ambiente virtual: ```python -m venv .venv```;
3. Ative o ambiente virtual: ```.\.venv\Script\activate```;
4. Instalar o pacote redis: ```pip install redis```;
5. Crie um arquivo teste_redis.py, com o seguinte código:
 ```
import redis


def main():
    try:
        # conecta no redis (ajuste host/port se necessário)
        r = redis.Redis(host="localhost", port=6379, db=0)

        # escreve um valor
        r.set("teste_chave", "Olá Redis!")

        # lê o valor
        valor = r.get("teste_chave")

        print("Valor armazenado no Redis:", valor.decode("utf-8"))

    except Exception as e:
        print("Erro ao conectar no Redis:", e)


if __name__ == "__main__":
    main()

```
7. Com o Ubuntu e o redis rodando, execute o compando: ```python .\teste_redis.py```;
8. Estando tudo certo, irá retornar Olá redis.

### Executando o Redis automaticamente
Para que o **Redis** execute automaticamete, siga os passos abaixo:

1. Criar um serviço para o WSL iniciar junto ao windows:
   * a) Abrir o **PowerShell**, vá até a pasta C:\Nssm\Win64;
   * b) Crie um serviço: ```.\Nssm install WSL-Ubuntu```;
   * c) Preencha da seguinte forma:
        * Application   
        * Path: ```C:\Program Files\WSL\wsl.exe````;
        * Startup directory: ```C:\Program Files\WSL```;
        * Arguments: ```wsl.exe --exec bash```;
        * Log on
        * This account: usuário que instalou o Wls
        * Password:
        * Confirm:
          
2. Habilitar o serviço Redis no WSL:
   * a) Execute o comando no WSL: ```sudo systemctl enable redis-server```;
   * b) Inicie o serviço: ```sudo systemctl start redis-server```;

## Nssm
Para o funcioanmento do Celery, faz se necessário a instalação do serviço no Windows com **Nssm**, pois o mesmo não inicia-se sozinho.

### Instalando Nssm
Para instalar o **Nssm** siga os passos abaixo:

1. Efetuar o download do Nssm no seguinte endereço: https://nssm.cc/download;
2. Descompactar o conteúdo e de preferência no caminho C:\Nssm;
3. Na pasta C:\Nssm\Win64, execute o Nssm.exe, ele irá informar os comandos.

### Gerenciando o Nssm

1. Execute o **PowerShell** com admin e vá até a pasta onde esta o Nssm.exe;
2. Execute o comando listado na aplicação iniciando com ```.\```, por exemplo: ```.\nssm edit <servicename>```.

## Celery
Link da documentação referência: https://docs.celeryq.dev/en/v5.5.3/getting-started/introduction.html
Para a utlização do Celery no projeto Django (Python), siga os passo abaixo:

### Instalando o pacote Celery

1. Na pasta do projeto, abra o **PowerShell** como adim;
2. Ative a .venv do projeto: ```.\.venv\Scripts\activate````;
3. Para instalar o pacote digite: ```pip install celery```;

### Configurando o Celery

1. Crie um arquivo task.py;
2. No arquivo importe o Celery e crie uma função, por exemplo:
   ```
    from celery import Celery  
    app = Celery(
        "task",
        broker="redis://localhost:6379/0",
        backend="redis://localhost:6379/0"
    )    
    @app.task
    def add(x, y):
        return x + y    
    if __name__ == "__main__":
        # dispara a task
        result = add.delay(4, 6)
        print("Task enviada, esperando resultado...")    
        print("Resultado:", result.get(timeout=10))
   ```
3. Para realizar o teste do arquivo, abra o **PowerShell** na pasta do arquivo e digite o comando: ```python .\task.py```;
4. Estando tudo certo, irá retornar 10. Obs: o **CeleryWork** deve estar executando no servidor.

### Executando o CeleryWork automaticamente
Para que o **CeleryWork** consuma a fila do **Redis**, siga os passos abaixo:

1. Criar um serviço para o CeleryWork iniciar junto ao windows:
   * a) Abrir o **PowerShell**, vá até a pasta C:\Nssm\Win64;
   * b) Crie um serviço: ```.\Nssm install CeleryWork```;
   * c) Preencha da seguinte forma:
        * Application   
        * Path: ```D:\inetpub\wwwroot\App\venv\Scripts\python.exe````;
        * Startup directory: ```D:\inetpub\wwwroot\App```;
        * Arguments: ```-m celery -A task worker --loglevel=info --pool=solo```;        

## Github
Para instalar e configurar o Git bash, siga os passos abaixo:

### Instalando o Git bash:
   * a) Efetuar o download do Git bash: https://git-scm.com/downloads;
   * b) Instalar o Git bash no servidor de forma padrão;

### Configurando o Git bash:
  * a) Atere a porta ssh: ```nano ~/.ssh/config (acessa o config)```;
  * b) Edite o arquivo:
  ```
  Host github.com
  Hostname ssh.github.com
  Port 443
  User git
  ```
  Salve a alteração com crtl+S e feche com crtl+X;

### Gerando a chave SSH:
  * a) Digite o comando no Gitbash: ```ssh-keygen.exe```;
  * b) A senha deixe em branco;
  * c) Copie o valor da chave gerada, com o comando cat e o caminho da chave publica gerada.

### Configurando a chave SSH no **Github**:
  * a) Em uma conta **Github**, vá em **Setting** e depois em **SSH and GPG keys**;
  * b) Crie uma nova chave SSH, informe o nome da chave e cole a chave gerada.

### Testando a conexão do Git bash:
  * a) Digite o comando: ```ssh -T git@github.com ```, estando tudo certo irá retornar ```Hi (nome no git)!```.


