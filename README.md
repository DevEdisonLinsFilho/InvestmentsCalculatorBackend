# POC de Autenticação com .NET 8 e Identity Server 4

## Introdução

Este projeto demonstra a implementação de um sistema de autenticação completo utilizando o Identity Server em conjunto com o .NET 8. O Identity Server é um framework open-source para autenticação e autorização em ASP.NET Core, oferecendo recursos robustos e flexíveis para proteger seus aplicativos Web.

## Funcionalidades

- **Autenticação baseada em token:** Gere e gerencie tokens JWT para autenticação segura de usuários.
- **Autorização baseada em escopo:** Controle o acesso a recursos específicos com base em escopos definidos nos tokens.
- **Registro e gerenciamento de usuários:** Implemente endpoints para registro, login, logout, recuperação de senha e atualização de informações de usuário.
- **Suporte a OpenID Connect:** Integre com clientes OpenID Connect para autenticação e autorização simplificadas.
- **Autenticação de dois fatores (2FA):** Implemente a autenticação de dois fatores para maior segurança, utilizando autenticação por email ou Google Authenticator.
- **Autenticação por cookies:** Permita a autenticação por cookies para maior comodidade do usuário.

## Pré-requisitos

- .NET 8 SDK instalado
- Banco de dados SQL Server (local ou remoto)
- Servidor de email configurado (opcional para 2FA por email)

## Passos para execução

1. **Clone o repositório:**

    ```bash
    git clone https://<url-do-repositorio>
    ```

2. **Restaure as dependências:**

    ```bash
    cd \.net8-identity-auth-demo
    dotnet restore
    ```

3. **Configure o banco de dados:**

    Edite o arquivo `appsettings.json` para definir as credenciais de conexão com o banco de dados SQL Server.

4. **Execute as migrações do banco de dados:**

    No diretório do projeto, execute o seguinte comando para aplicar as migrações:

    ```bash
    cd \Auth.Infrastructure
    dotnet restore  
    dotnet ef database update
    ```

5. **Configure o email (opcional para 2FA por email):**

    Se desejar usar 2FA por email, edite o arquivo `appsettings.json` para definir as configurações do servidor de email.

6. **Execute a aplicação:**

    No diretório do projeto, execute o seguinte comando:

    ```bash
    dotnet run
    ```

## Testando os endpoints

Os endpoints da API podem ser testados utilizando ferramentas como Postman ou curl. A seguir, alguns exemplos de requisições:

- **Cadastro de usuário:**

    ```bash
    POST http://localhost:5001/api/register \
    Content-Type: application/json \
    -d '{ "email": "usuario@exemplo.com", "password": "senha123" }'
    ```

- **Login:**

    ```bash
    POST http://localhost:5001/api/login \
    Content-Type: application/json \
    -d '{ "email": "usuario@exemplo.com", "password": "senha123" }'
    ```

- **Acesso a recurso protegido:**

    ```bash
    GET http://localhost:5000/api/recurso-protegido \
    Authorization: Bearer <token_obtido_no_login>
    ```

- **Ativando 2FA por email:**

    - Acesse o endpoint `/api/profile/enable2fa` e forneça o seu endereço de email.
    - Verifique sua caixa de entrada e siga as instruções para concluir a ativação.

- **Ativando 2FA com Google Authenticator:**

    - Baixe e instale o aplicativo Google Authenticator em seu dispositivo móvel.
    - Acesse o endpoint `/api/profile/enable2fa` e escaneie o código QR exibido.
    - Digite o código gerado pelo Google Authenticator para concluir a ativação.

- **Autenticação por cookies:**

    Após o login bem-sucedido, o usuário será autenticado por cookie. As requisições subsequentes para recursos protegidos serão automaticamente autenticadas com base no cookie.

## Observações

- Este projeto é um PoC e pode ser adaptado para atender às necessidades específicas de sua aplicação.
- Para mais informações sobre o Identity Server, consulte a [documentação oficial](https://identityserver4.readthedocs.io/).

