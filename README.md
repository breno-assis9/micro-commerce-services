# micro-commerce-services

# E-Commerce Microservices

Este projeto é uma arquitetura de microsserviços para uma plataforma de e-commerce construída com **.NET Core 8**. A solução integra várias tecnologias e ferramentas modernas para garantir escalabilidade, resiliência, segurança e facilidade de manutenção. O projeto inclui um **API Gateway**, comunicação entre serviços utilizando **gRPC**, manipulação eficiente de dados com **Dapper** e **EF Core**, autenticação com **JWT**, e uma série de outras funcionalidades essenciais para um e-commerce robusto.

---

## 🚀 Tecnologias Utilizadas

- **.NET Core 8**: Framework para construção de APIs modernas e escaláveis.
- **API Gateway**: Roteamento centralizado de todas as requisições para os microsserviços.
- **gRPC (Google.Protobuf)**: Comunicação de alta performance entre microsserviços.
- **Serilog**: Framework de logging para monitoramento e rastreamento de eventos.
- **Swagger**: Interface de documentação interativa da API.
- **FluentValidation**: Validação de dados com uma API fluente.
- **MediatR**: Biblioteca para implementação de padrões CQRS (Command Query Responsibility Segregation).
- **EasyNetQ**: Biblioteca para comunicação assíncrona baseada em **RabbitMQ**.
- **Polly**: Estratégias de resiliência, como retries e circuit breakers, para chamadas HTTP.
- **EF Core (Entity Framework Core)**: ORM para mapeamento de dados entre a aplicação e o banco.
- **Pomelo**: Driver MySQL para EF Core, compatível com MySQL e MariaDB.
- **JWT (JSON Web Tokens)**: Autenticação segura baseada em tokens.
- **Bogus**: Biblioteca para geração de dados falsos para testes e desenvolvimento.
- **Dapper**: Micro ORM para consultas SQL mais rápidas e eficientes.

---

## 💡 Funcionalidades

- **Autenticação e Autorização JWT**: Controle de acesso seguro com tokens JWT.
- **API Gateway**: Roteamento centralizado das requisições para os microsserviços, simplificando a gestão de endpoints.
- **gRPC para Comunicação entre Microsserviços**: Alta performance e baixo overhead na comunicação entre os serviços.
- **Health Checks**: Monitoramento da saúde de cada serviço e do sistema como um todo.
- **Resiliência e Retry com Polly**: Garantia de que os microsserviços sejam resilientes a falhas.
- **Validação de Dados com FluentValidation**: Validação de entradas e saídas em toda a API.
- **Mensageria Assíncrona com EasyNetQ (RabbitMQ)**: Comunicação assíncrona e escalável entre microsserviços.
- **Banco de Dados com EF Core e Dapper**: Acesso eficiente a dados com mapeamento ORM (EF Core) e consultas SQL (Dapper).
- **Documentação Interativa com Swagger**: Interface para testar os endpoints da API diretamente.
- **Gerador de Dados com Bogus**: Geração de dados fictícios para testes e desenvolvimento.
- **Logs com Serilog**: Logs detalhados e estruturados para rastreamento e auditoria.
- **Versionamento de API**: Suporte a múltiplas versões da API, garantindo retrocompatibilidade.

---

## 📦 Como Começar

### Pré-requisitos

Para rodar a aplicação localmente, você precisará ter as seguintes ferramentas instaladas:

- **.NET Core SDK 8.x** ou superior
- **SQL Server / MySQL / MariaDB** (ou outros bancos de dados compatíveis)
- **RabbitMQ** (para mensageria com EasyNetQ)
- **Postman** ou outro cliente de API (opcional)

### Passos para Configuração

1. **Clone o repositório**:

   git clone https://github.com/seu-usuario/ecommerce-microservices.git
   cd ecommerce-microservices

2. **Restaurar dependências:**

dotnet restore

3. **Configuração do Banco de Dados:**

Configure a string de conexão do banco de dados no arquivo appsettings.json:

4. **Para SQL Server:**

"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=EcommerceDB;Trusted_Connection=True;"
}

5. **Para MySQL com Pomelo:**

"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Database=EcommerceDB;User=root;Password=senha;"
}

6. **Executar Migrations (caso necessário):**

Se for a primeira vez que você está rodando a aplicação, será necessário aplicar as migrações do banco de dados:

dotnet ef database update
Rodar a aplicação:

7. **Execute o seguinte comando para iniciar os microsserviços:**

dotnet run
A aplicação estará disponível no endereço: http://localhost:5000.

## 🛠️ Endpoints da API

Acesse a documentação interativa da API através do Swagger. Para visualizar a documentação, acesse o seguinte endereço:

URL do Swagger: http://localhost:5000/swagger

Exemplos de Endpoints:

**Autenticação:**

POST /api/auth/login
Retorna um token JWT para autenticação.

**Cadastro de Produto:**

POST /api/v1/products
Adiciona um novo produto ao catálogo.

**Carrinho de Compras:**

POST /api/v1/cart
Cria ou atualiza o carrinho de compras do usuário.

**Pedido de Compra:**

POST /api/v1/orders
Cria um novo pedido de compra.

**Mensageria (RabbitMQ):**

POST /api/v1/notifications/send
Envia notificações assíncronas para outros microsserviços.

## ✅ Validação de Dados com FluentValidation
A API utiliza o FluentValidation para garantir que as entradas sejam válidas e consistentes. Exemplo de uma regra de validação de produto:

public class ProductValidator : AbstractValidator<ProductDto>
{
    public ProductValidator()
    {
        RuleFor(x => x.Name).NotEmpty().WithMessage("O nome do produto é obrigatório.");
        RuleFor(x => x.Price).GreaterThan(0).WithMessage("O preço do produto deve ser maior que zero.");
    }
}

## 🔧 Monitoramento de Erros com Serilog
Serilog é configurado para gerar logs estruturados. Isso facilita o rastreamento de erros e eventos na aplicação.

Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .WriteTo.File("logs/ecommerce-log.txt", rollingInterval: RollingInterval.Day)
    .CreateLogger();

## 🔐 Autenticação JWT

A API utiliza JWT Bearer Tokens para autenticação. Para obter um token de acesso, envie as credenciais do usuário para o endpoint de login:

**Endpoint de Login:**

POST /api/auth/login
Exemplo de Resposta:

{
  "token": "seu-token-jwt-aqui"
}

Inclua o token nas requisições subsequentes utilizando o cabeçalho Authorization:

Authorization: Bearer seu-token-jwt-aqui

## 📝 Contribuindo

Contribuições são bem-vindas! Se você encontrou um bug ou tem sugestões de melhorias, siga os passos abaixo:

Fork este repositório.
Crie uma branch para sua feature ou correção:
git checkout -b feature/MinhaFeature
Faça as alterações necessárias e comite-as:
git commit -am 'Adiciona nova funcionalidade'
Envie para o seu fork:
git push origin feature/MinhaFeature
Abra um Pull Request explicando suas alterações.

## 🛡️ Licença
Distribuído sob a licença MIT. Veja o arquivo LICENSE para mais informações.

## 🙏 Agradecimentos
Agradecemos a todos os mantenedores e à comunidade de código aberto pelas ferramentas e bibliotecas que tornam este projeto possível. Nosso objetivo é fornecer uma solução robusta e escalável para e-commerce com microsserviços.

Este README.md fornece uma visão clara sobre a estrutura do projeto, como configurá-lo e utilizá-lo, além de detalhar as funcionalidades e ferramentas usadas para garantir uma arquitetura de microsserviços eficiente e segura.

### Características deste README:
- **Estrutura clara e organizada**, dividida em seções fáceis de entender.
- **Tecnologias e ferramentas** detalhadas, explicando o papel de cada uma.
- **Passos de configuração e execução** para que qualquer desenvolvedor possa rodar o projeto localmente.
- **Documentação Swagger** para facilitar a integração e o uso dos endpoints da API.
- **Exemplos de código** para ilustrar



