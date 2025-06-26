🚀 Aprendendo Swagger com JavaScript



Guia interativo e didático para dominar APIs com Swagger

👋 Bem-vindo! Este guia vai te ensinar Swagger de forma prática e interativa.



📚 Índice do Conteúdo





Introdução



Conceitos Fundamentais



Prática com JavaScript



Exercícios Interativos



🎯 1. Introdução

O que é Swagger?

Swagger é um conjunto de ferramentas para documentar, testar e consumir APIs REST.

💡 Por que usar Swagger?





Documentação automática da API



Interface visual para testar endpoints



Geração de código cliente



Padronização da documentação

🎮 Demo: Swagger vs Documentação Tradicional

❌ Documentação Tradicional

POST /users
Cria um novo usuário...


Informações limitadas e estáticas

✅ Com Swagger





Interface interativa



Parâmetros detalhados



Exemplos de request/response



Possibilidade de testar diretamente



Documentação sempre atualizada



📖 2. Conceitos Fundamentais

🔧 OpenAPI Specification

É o formato padrão para descrever APIs REST. Antes era chamado de "Swagger Specification".

{
  "openapi": "3.0.0",
  "info": {
    "title": "Minha API",
    "version": "1.0.0"
  },
  "paths": {
    "/users": {
      "get": {
        "summary": "Lista usuários"
      }
    }
  }
}


🎯 Componentes Principais

1. Paths





Endpoints da API (/users, /products)



Define as operações disponíveis

2. Schemas





Estrutura dos dados (User, Product)



Validação de tipos de dados

3. Parameters





Query parameters



Path parameters



Header parameters

🎯 Exercício: Identifique os Componentes

No código abaixo, identifique os diferentes componentes:

{
  "info": {                    // ← Metadados da API
    "title": "Pet Store API"
  },
  "paths": {                   // ← Definição dos endpoints
    "/pets": {
      "get": {                 // ← Método HTTP
        "summary": "List pets"
      }
    }
  }
}


Componentes identificados:





info: Contém metadados da API como título e versão



paths: Define todos os endpoints da API



get: Método HTTP que define uma operação específica



💻 3. Prática com JavaScript

🛠️ Como usar Swagger com JavaScript

Existem 3 formas principais:

1. Swagger UI





Interface visual para testar APIs



Renderização automática da documentação



Permite execução de requests em tempo real

2. Swagger Codegen





Gera código cliente automaticamente



Suporte para múltiplas linguagens



Reduz tempo de desenvolvimento

3. Swagger Parser





Valida especificações Swagger



Processa e converte especificações



Integração com pipelines de CI/CD

🔥 Exemplo Prático com JavaScript

// Exemplo: Criando uma spec Swagger
const swaggerSpec = {
  openapi: '3.0.0',
  info: {
    title: 'Minha API de Pets',
    version: '1.0.0',
    description: 'API para gerenciar pets'
  },
  paths: {
    '/pets': {
      get: {
        summary: 'Lista todos os pets',
        responses: {
          200: {
            description: 'Lista de pets'
          }
        }
      }
    }
  }
};

// Acessando informações da spec
console.log('Título:', swaggerSpec.info.title);
console.log('Endpoints:', Object.keys(swaggerSpec.paths));


Resultado:

Título: Minha API de Pets
Endpoints: ['/pets']


🌐 Simulador de API

GET /users

Status: 200 OK

[
  { "id": 1, "name": "João", "email": "joao@email.com" },
  { "id": 2, "name": "Maria", "email": "maria@email.com" }
]


POST /users

Status: 201 Created

{ "id": 3, "name": "Novo Usuário", "email": "novo@email.com" }


GET /users/1

Status: 200 OK

{ 
  "id": 1, 
  "name": "João", 
  "email": "joao@email.com", 
  "created_at": "2023-01-01" 
}


DELETE /users/1

Status: 204 No Content

null




🎯 4. Exercícios Interativos

📝 Exercício 1: Complete a Spec Swagger

Tarefa: Complete o código Swagger abaixo adicionando um endpoint POST:

{
  "openapi": "3.0.0",
  "info": {
    "title": "Books API",
    "version": "1.0.0"
  },
  "paths": {
    "/books": {
      "get": {
        "summary": "Get all books"
      }
      // ADICIONE UM ENDPOINT POST AQUI
    }
  }
}


💡 Dicas:

Um endpoint POST deve incluir:





Método "post"



Summary descritivo



Resposta 201 (Created)

✅ Solução:

{
  "openapi": "3.0.0",
  "info": {
    "title": "Books API",
    "version": "1.0.0"
  },
  "paths": {
    "/books": {
      "get": {
        "summary": "Get all books"
      },
      "post": {
        "summary": "Create a new book",
        "responses": {
          "201": {
            "description": "Book created successfully"
          }
        }
      }
    }
  }
}


🎮 Exercício 2: Quiz Swagger

Pergunta: Qual é a versão atual da OpenAPI Specification mais utilizada?





2.0



3.0



4.0

Resposta: ✅ Correto! A versão 3.0 é a mais utilizada atualmente da OpenAPI Specification.

🏆 Desafio Final: API de E-commerce

Objetivo: Crie uma especificação Swagger completa para uma API de E-commerce!

Requisitos:





Endpoints para produtos: GET, POST, PUT, DELETE



Endpoint para buscar produtos por categoria



Schema para o objeto Product



Respostas de erro apropriadas

🚀 Solução Exemplo:

openapi: 3.0.0
info:
  title: E-commerce API
  version: 1.0.0
  description: API para gerenciar produtos de e-commerce

paths:
  /products:
    get:
      summary: Lista todos os produtos
      parameters:
        - name: category
          in: query
          schema:
            type: string
          description: Filtrar por categoria
        - name: limit
          in: query
          schema:
            type: integer
            default: 10
          description: Número máximo de produtos
      responses:
        '200':
          description: Lista de produtos
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Product'
        '400':
          description: Parâmetros inválidos

    post:
      summary: Cria um novo produto
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductInput'
      responses:
        '201':
          description: Produto criado com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
        '400':
          description: Dados inválidos

  /products/{id}:
    parameters:
      - name: id
        in: path
        required: true
        schema:
          type: integer
        description: ID do produto

    get:
      summary: Busca produto por ID
      responses:
        '200':
          description: Produto encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
        '404':
          description: Produto não encontrado

    put:
      summary: Atualiza produto
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductInput'
      responses:
        '200':
          description: Produto atualizado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
        '404':
          description: Produto não encontrado

    delete:
      summary: Remove produto
      responses:
        '204':
          description: Produto removido com sucesso
        '404':
          description: Produto não encontrado

  /products/category/{category}:
    parameters:
      - name: category
        in: path
        required: true
        schema:
          type: string
        description: Nome da categoria

    get:
      summary: Busca produtos por categoria
      responses:
        '200':
          description: Produtos da categoria
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Product'

components:
  schemas:
    Product:
      type: object
      properties:
        id:
          type: integer
          description: ID único do produto
        name:
          type: string
          description: Nome do produto
        description:
          type: string
          description: Descrição do produto
        price:
          type: number
          format: float
          description: Preço do produto
        category:
          type: string
          description: Categoria do produto
        stock:
          type: integer
          description: Quantidade em estoque
        created_at:
          type: string
          format: date-time
          description: Data de criação
        updated_at:
          type: string
          format: date-time
          description: Data de atualização
      required:
        - id
        - name
        - price
        - category

    ProductInput:
      type: object
      properties:
        name:
          type: string
          description: Nome do produto
        description:
          type: string
          description: Descrição do produto
        price:
          type: number
          format: float
          description: Preço do produto
        category:
          type: string
          description: Categoria do produto
        stock:
          type: integer
          description: Quantidade em estoque
      required:
        - name
        - price
        - category




🎉 Certificado de Conclusão

Parabéns! 🏆

Você completou o curso de Swagger com JavaScript!

Certificado de Conclusão
Nome: Luan Oliveira dos Santos
Curso: Swagger com JavaScript
Data de Conclusão: [Data Atual]

Continue praticando e explorando APIs com Swagger!



🚀 Próximos Passos

Recursos Úteis





Documentação Oficial do Swagger



Swagger Editor Online



Exemplo Pet Store

Continue sua jornada:





Pratique criando suas próprias especificações



Explore ferramentas avançadas como Swagger Codegen



Integre Swagger em seus projetos reais



Contribua para a comunidade open source



🎯 Resumo do Aprendizado

✅ O que você aprendeu:





Conceitos Fundamentais





O que é Swagger/OpenAPI



Componentes principais (Paths, Schemas, Parameters)



Diferenças entre versões



Aplicação Prática





Como usar Swagger com JavaScript



Criação de especificações



Validação e testes



Exercícios Hands-on





Completar especificações Swagger



Identificar componentes



Criar APIs completas



Melhores Práticas





Estruturação de documentação



Padrões de nomenclatura



Tratamento de erros

🎓 Habilidades Desenvolvidas:





✅ Leitura e interpretação de specs Swagger



✅ Criação de documentação de APIs



✅ Uso de ferramentas do ecossistema Swagger



✅ Integração com JavaScript



✅ Validação e testes de APIs



Desenvolvido com ❤️ para a comunidade de desenvolvedores

Continue explorando e construindo APIs incríveis! 🚀
