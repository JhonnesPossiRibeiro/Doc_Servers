# Doc_Servers
Documentação para configuração de servidores

## Configurando IIS para Django (Python)
Para criar um site no IIS para backend em Django (Python) siga os passos abaixo:

### Criar um site:
1. Botão direito do mouse sobre o **Sites**, escolha a opção **Add WebSites**;
2. Informe um nome para o site **Site name**;
3. A **Application pool** será criada com o mesmo nome do site;
4. Em **Physical path** selecione a pasta em que ficará o código fonte do projeto;
5. Em **Binding** em **Type** escolha o protocolo, em **Port** informe uma porta para o site;
6. Caso escolher o protocolo **https** informe o **Host name**. Obs: em conjunto com o time de infra, gerar um certificado, o **Host name** será o mesmo informado para o certificado;
7. Em **SSL certificate** informe o certificado intalado no servidor para o protocolo https;
8. Confirme a criação em "OK".


