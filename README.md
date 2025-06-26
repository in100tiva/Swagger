# 🚀 Aprendendo Swagger com JavaScript

> **Guia interativo e didático para dominar APIs com Swagger**

[![Versão](https://img.shields.io/badge/vers%C3%A3o-1.0.0-green.svg)](https://github.com/luanoliveira/swagger-learning)
[![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-blue.svg)](LICENSE)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-yellow.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0.0-blue.svg)](https://spec.openapis.org/oas/v3.0.3)

---

## 📚 Índice do Conteúdo

1. [Introdução](#-1-introdução)
2. [Conceitos Fundamentais](#-2-conceitos-fundamentais)  
3. [Prática com JavaScript](#-3-prática-com-javascript)
4. [Exercícios Interativos](#-4-exercícios-interativos)
5. [Recursos Adicionais](#-recursos-adicionais)
6. [Contribuição](#-contribuição)

---

## 🎯 1. Introdução

### O que é Swagger?

**Swagger** é um conjunto de ferramentas poderosas para **documentar, testar e consumir APIs REST** de forma padronizada e interativa.

### 💡 Por que usar Swagger?

- ✅ **Documentação automática** da API
- ✅ **Interface visual** para testar endpoints
- ✅ **Geração de código cliente** automatizada
- ✅ **Padronização** da documentação
- ✅ **Sincronização** entre código e documentação
- ✅ **Experiência de desenvolvedor** aprimorada

### 🎮 Demo: Swagger vs Documentação Tradicional

#### ❌ Documentação Tradicional
POST /users Cria um novo usuário... Parâmetros: nome, email

*Informações limitadas e estáticas*

#### ✅ Com Swagger
- 🎯 Interface interativa  
- 📋 Parâmetros detalhados com tipos
- 📝 Exemplos de request/response
- 🧪 Possibilidade de testar diretamente
- 🔄 Documentação sempre atualizada

**Resultado:** Desenvolvedores conseguem integrar APIs 3x mais rápido!

---

## 📖 2. Conceitos Fundamentais

### 🔧 OpenAPI Specification

É o **formato padrão** para descrever APIs REST. Anteriormente conhecido como "Swagger Specification".

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "Minha API",
    "version": "1.0.0",
    "description": "Uma API de exemplo para demonstração"
  },
  "paths": {
    "/users": {
      "get": {
        "summary": "Lista todos os usuários",
        "responses": {
          "200": {
            "description": "Lista de usuários retornada com sucesso"
          }
        }
      }
    }
  }
}
🎯 Componentes Principais
1. Paths 🛣️
Define os endpoints da API (/users, /products)
Especifica as operações disponíveis (GET, POST, PUT, DELETE)
Inclui parâmetros e respostas
2. Schemas 📋
Define a estrutura dos dados (User, Product)
Especifica tipos de dados e validações
Permite reutilização de definições
3. Parameters ⚙️
Query parameters: ?page=1&limit=10
Path parameters: /users/{id}
Header parameters: Authorization: Bearer token
Body parameters: dados no corpo da requisição
🎯 Exercício: Identifique os Componentes
No código abaixo, identifique os diferentes componentes:

{
  "info": {                    // ← Metadados da API
    "title": "Pet Store API",
    "version": "1.0.0"
  },
  "paths": {                   // ← Definição dos endpoints
    "/pets": {
      "get": {                 // ← Método HTTP
        "summary": "Lista pets",
        "parameters": [         // ← Parâmetros da operação
          {
            "name": "limit",
            "in": "query",
            "schema": { "type": "integer" }
          }
        ],
        "responses": {          // ← Respostas possíveis
          "200": {
            "description": "Lista de pets"
          }
        }
      }
    }
  }
}
🔍 Componentes identificados:
info: Contém metadados da API como título e versão
paths: Define todos os endpoints da API
get: Método HTTP que define uma operação específica
parameters: Define parâmetros aceitos pela operação
responses: Especifica respostas possíveis da operação
💻 3. Prática com JavaScript
🛠️ Como usar Swagger com JavaScript
Existem 3 formas principais de trabalhar com Swagger:

1. Swagger UI 🎨
Interface visual para testar APIs
Renderização automática da documentação
Permite execução de requests em tempo real
Customizável e embeddable
// Exemplo: Inicializando Swagger UI
import SwaggerUI from 'swagger-ui'

SwaggerUI({
  dom_id: '#swagger-ui',
  url: 'https://api.exemplo.com/swagger.json',
  deepLinking: true,
  presets: [
    SwaggerUI.presets.apis,
    SwaggerUI.presets.standalone
  ]
})
2. Swagger Codegen ⚡
Gera código cliente automaticamente
Suporte para múltiplas linguagens
Reduz tempo de desenvolvimento
Mantém sincronização com a API
# Exemplo: Gerando cliente JavaScript
swagger-codegen generate \
  -i swagger.json \
  -l javascript \
  -o ./generated-client
3. Swagger Parser 🔍
Valida especificações Swagger
Processa e converte especificações
Integração com pipelines de CI/CD
Resolve referências automáticas
// Exemplo: Validando especificação
import SwaggerParser from '@apidevtools/swagger-parser'

try {
  const api = await SwaggerParser.validate('swagger.yaml')
  console.log('API válida:', api.info.title)
} catch (error) {
  console.error('Erro na especificação:', error.message)
}
🔥 Exemplo Prático Completo
// Exemplo: Criando e manipulando uma spec Swagger
const swaggerSpec = {
  openapi: '3.0.0',
  info: {
    title: 'API de Gerenciamento de Pets',
    version: '1.0.0',
    description: 'API completa para gerenciar informações de pets',
    contact: {
      name: 'Equipe de Desenvolvimento',
      email: 'dev@petstore.com'
    }
  },
  servers: [
    {
      url: 'https://api.petstore.com/v1',
      description: 'Servidor de Produção'
    },
    {
      url: 'https://staging-api.petstore.com/v1', 
      description: 'Servidor de Staging'
    }
  ],
  paths: {
    '/pets': {
      get: {
        summary: 'Lista todos os pets',
        description: 'Retorna uma lista paginada de todos os pets disponíveis',
        parameters: [
          {
            name: 'page',
            in: 'query',
            description: 'Número da página',
            schema: { type: 'integer', default: 1 }
          },
          {
            name: 'limit',
            in: 'query', 
            description: 'Itens por página',
            schema: { type: 'integer', default: 10, maximum: 100 }
          }
        ],
        responses: {
          200: {
            description: 'Lista de pets retornada com sucesso',
            content: {
              'application/json': {
                schema: {
                  type: 'object',
                  properties: {
                    data: {
                      type: 'array',
                      items: { $ref: '#/components/schemas/Pet' }
                    },
                    pagination: {
                      $ref: '#/components/schemas/Pagination'
                    }
                  }
                }
              }
            }
          },
          400: {
            description: 'Parâmetros inválidos'
          }
        }
      },
      post: {
        summary: 'Cria um novo pet',
        requestBody: {
          required: true,
          content: {
            'application/json': {
              schema: { $ref: '#/components/schemas/PetInput' }
            }
          }
        },
        responses: {
          201: {
            description: 'Pet criado com sucesso',
            content: {
              'application/json': {
                schema: { $ref: '#/components/schemas/Pet' }
              }
            }
          }
        }
      }
    }
  },
  components: {
    schemas: {
      Pet: {
        type: 'object',
        required: ['id', 'name', 'species'],
        properties: {
          id: { type: 'integer', example: 1 },
          name: { type: 'string', example: 'Buddy' },
          species: { type: 'string', enum: ['dog', 'cat', 'bird'] },
          age: { type: 'integer', minimum: 0, maximum: 30 },
          created_at: { type: 'string', format: 'date-time' }
        }
      },
      PetInput: {
        type: 'object',
        required: ['name', 'species'],
        properties: {
          name: { type: 'string', minLength: 1, maxLength: 50 },
          species: { type: 'string', enum: ['dog', 'cat', 'bird'] },
          age: { type: 'integer', minimum: 0, maximum: 30 }
        }
      },
      Pagination: {
        type: 'object',
        properties: {
          page: { type: 'integer' },
          limit: { type: 'integer' },
          total: { type: 'integer' },
          pages: { type: 'integer' }
        }
      }
    }
  }
}

// Funções utilitárias para trabalhar com a spec
class SwaggerHelper {
  constructor(spec) {
    this.spec = spec
  }
  
  // Obter informações básicas da API
  getApiInfo() {
    return {
      title: this.spec.info.title,
      version: this.spec.info.version,
      description: this.spec.info.description
    }
  }
  
  // Listar todos os endpoints
  getEndpoints() {
    return Object.keys(this.spec.paths)
  }
  
  // Obter métodos HTTP de um endpoint
  getMethodsForPath(path) {
    const pathObj = this.spec.paths[path]
    return Object.keys(pathObj).filter(key => 
      ['get', 'post', 'put', 'delete', 'patch'].includes(key)
    )
  }
  
  // Validar se um schema existe
  hasSchema(schemaName) {
    return this.spec.components?.schemas?.[schemaName] !== undefined
  }
  
  // Gerar exemplo de request para um endpoint
  generateExampleRequest(path, method) {
    const operation = this.spec.paths[path]?.[method]
    if (!operation) return null
    
    const example = {}
    
    // Adicionar parâmetros de query
    const queryParams = operation.parameters?.filter(p => p.in === 'query') || []
    if (queryParams.length > 0) {
      example.query = {}
      queryParams.forEach(param => {
        example.query[param.name] = param.schema?.default || param.schema?.example
      })
    }
    
    // Adicionar body se necessário
    if (operation.requestBody) {
      const schema = operation.requestBody.content?.['application/json']?.schema
      if (schema?.$ref) {
        const schemaName = schema.$ref.split('/').pop()
        example.body = this.generateSchemaExample(schemaName)
      }
    }
    
    return example
  }
  
  // Gerar exemplo baseado em um schema
  generateSchemaExample(schemaName) {
    const schema = this.spec.components?.schemas?.[schemaName]
    if (!schema) return {}
    
    const example = {}
    Object.entries(schema.properties || {}).forEach(([prop, definition]) => {
      if (definition.example !== undefined) {
        example[prop] = definition.example
      } else if (definition.type === 'string') {
        example[prop] = definition.enum?.[0] || `exemplo_${prop}`
      } else if (definition.type === 'integer') {
        example[prop] = definition.minimum || 1
      } else if (definition.type === 'boolean') {
        example[prop] = true
      }
    })
    
    return example
  }
}

// Usando a classe helper
const helper = new SwaggerHelper(swaggerSpec)

console.log('📋 Informações da API:', helper.getApiInfo())
console.log('🛣️ Endpoints disponíveis:', helper.getEndpoints())
console.log('🔧 Métodos para /pets:', helper.getMethodsForPath('/pets'))
console.log('📝 Exemplo de request POST:', helper.generateExampleRequest('/pets', 'post'))
🎯 Resultado esperado:

📋 Informações da API: {
  title: "API de Gerenciamento de Pets",
  version: "1.0.0", 
  description: "API completa para gerenciar informações de pets"
}

🛣️ Endpoints disponíveis: ["/pets"]

🔧 Métodos para /pets: ["get", "post"]

📝 Exemplo de request POST: {
  body: {
    name: "exemplo_name",
    species: "dog",
    age: 0
  }
}
🌐 Simulador de API
Aqui estão alguns endpoints simulados para você testar:

GET /users
Status: 200 OK

{
  "data": [
    { 
      "id": 1, 
      "name": "João Silva", 
      "email": "joao@email.com",
      "role": "admin",
      "created_at": "2023-01-15T10:30:00Z"
    },
    { 
      "id": 2, 
      "name": "Maria Santos", 
      "email": "maria@email.com",
      "role": "user",
      "created_at": "2023-02-20T14:45:00Z"
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 2,
    "pages": 1
  }
}
POST /users
Request Body:

{
  "name": "Novo Usuário",
  "email": "novo@email.com",
  "role": "user"
}
Status: 201 Created

{ 
  "id": 3, 
  "name": "Novo Usuário", 
  "email": "novo@email.com",
  "role": "user",
  "created_at": "2024-06-26T07:54:00Z"
}
GET /users/1
Status: 200 OK

{ 
  "id": 1, 
  "name": "João Silva", 
  "email": "joao@email.com",
  "role": "admin",
  "profile": {
    "avatar": "https://example.com/avatar1.jpg",
    "bio": "Desenvolvedor Full Stack",
    "location": "São Paulo, SP"
  },
  "created_at": "2023-01-15T10:30:00Z",
  "updated_at": "2024-06-25T16:20:00Z"
}
DELETE /users/1
Status: 204 No Content

null
🎯 4. Exercícios Interativos
📝 Exercício 1: Complete a Spec Swagger
🎯 Tarefa: Complete o código Swagger abaixo adicionando um endpoint POST:

{
  "openapi": "3.0.0",
  "info": {
    "title": "Books API",
    "version": "1.0.0"
  },
  "paths": {
    "/books": {
      "get": {
        "summary": "Get all books",
        "responses": {
          "200": {
            "description": "Lista de livros"
          }
        }
      }
      // 👇 ADICIONE UM ENDPOINT POST AQUI
    }
  }
}
💡 Dicas:
Um endpoint POST deve incluir:

✅ Método "post"
✅ summary descritivo
✅ requestBody com schema
✅ Resposta 201 (Created)
✅ Resposta 400 (Bad Request)
<details> <summary>👁️ Ver Solução</summary>
{
  "openapi": "3.0.0",
  "info": {
    "title": "Books API", 
    "version": "1.0.0"
  },
  "paths": {
    "/books": {
      "get": {
        "summary": "Get all books",
        "responses": {
          "200": {
            "description": "Lista de livros"
          }
        }
      },
      "post": {
        "summary": "Create a new book",
        "description": "Adiciona um novo livro à biblioteca",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "type": "object",
                "required": ["title", "author"],
                "properties": {
                  "title": {
                    "type": "string",
                    "example": "O Alquimista"
                  },
                  "author": {
                    "type": "string", 
                    "example": "Paulo Coelho"
                  },
                  "isbn": {
                    "type": "string",
                    "example": "978-85-7505-049-4"
                  },
                  "pages": {
                    "type": "integer",
                    "minimum": 1,
                    "example": 163
                  }
                }
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "Livro criado com sucesso",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "integer"},
                    "title": {"type": "string"},
                    "author": {"type": "string"},
                    "created_at": {"type": "string", "format": "date-time"}
                  }
                }
              }
            }
          },
          "400": {
            "description": "Dados inválidos fornecidos"
          }
        }
      }
    }
  }
}
🎉 Excelente! Você adicionou corretamente um endpoint POST com todos os elementos necessários!

</details>
🎮 Exercício 2: Quiz Swagger
Pergunta 1
❓ Qual é a versão atual da OpenAPI Specification mais utilizada?

 2.0
 3.0
 4.0
 1.0
<details> <summary>🔍 Ver Resposta</summary>
✅ Resposta correta: 3.0

A versão 3.0 da OpenAPI Specification é atualmente a mais utilizada. Ela trouxe várias melhorias importantes sobre a versão 2.0, incluindo:

Melhor suporte para componentes reutilizáveis
Estrutura mais clara de request/response
Suporte aprimorado para autenticação
Melhor validação de dados
</details>
Pergunta 2
❓ Qual elemento é usado para definir a estrutura de dados em uma especificação OpenAPI?

 Paths
 Parameters
 Schemas
 Responses
<details> <summary>🔍 Ver Resposta</summary>
✅ Resposta correta: Schemas

Os Schemas são usados para definir a estrutura de dados, tipos, validações e exemplos dos objetos utilizados na API. Eles ficam tipicamente na seção components/schemas e podem ser referenciados em toda a especificação.

</details>
Pergunta 3
❓ Qual é a principal vantagem do Swagger UI?

 Gerar código automaticamente
 Testar APIs de forma interativa
 Validar especificações
 Criar documentação em PDF
<details> <summary>🔍 Ver Resposta</summary>
✅ Resposta correta: Testar APIs de forma interativa

O Swagger UI cria uma interface web interativa onde desenvolvedores podem:

Explorar endpoints visualmente
Executar requests diretamente no navegador
Ver exemplos de request/response
Testar diferentes cenários sem código adicional
</details>
🏆 Desafio Final: API de E-commerce
🎯 Objetivo: Crie uma especificação Swagger completa para uma API de E-commerce!

📋 Requisitos Obrigatórios:
✅ Endpoints para produtos: GET, POST, PUT, DELETE
✅ Endpoint para buscar produtos por categoria: GET /products/category/{category}
✅ Schema detalhado para o objeto Product
✅ Schema para input de produto ProductInput
✅ Respostas de erro apropriadas (400, 404, 500)
✅ Parâmetros de paginação
✅ Documentação completa com exemplos
📏 Critérios de Avaliação:
Completude (30%): Todos os endpoints implementados
Qualidade dos Schemas (25%): Estruturas bem definidas
Tratamento de Erros (20%): Respostas apropriadas
Documentação (15%): Descrições claras
Exemplos (10%): Dados realistas
<details> <summary>🚀 Ver Solução Completa</summary>
openapi: 3.0.0
info:
  title: E-commerce API
  version: 2.1.0
  description: |
    API completa para gerenciamento de produtos de e-commerce.
    
    **Recursos principais:**
    - CRUD completo de produtos
    - Busca por categoria
    - Paginação inteligente
    - Filtros avançados
    - Validação robusta
    
    **Autenticação:** Bearer Token necessário para operações de escrita.
    
  contact:
    name: Equipe E-commerce
    email: api@ecommerce.com
    url: https://docs.ecommerce.com
  license:
    name: MIT
    url: https://opensource.org/licenses/MIT

servers:
  - url: https://api.ecommerce.com/v2
    description: Servidor de Produção
  - url: https://staging-api.ecommerce.com/v2
    description: Servidor de Staging
  - url: http://localhost:3000/v2
    description: Desenvolvimento Local

tags:
  - name: Products
    description: Operações relacionadas a produtos
  - name: Categories
    description: Operações relacionadas a categorias

paths:
  /products:
    get:
      tags: [Products]
      summary: Lista todos os produtos
      description: |
        Retorna uma lista paginada de produtos com suporte a filtros avançados.
        
        **Filtros disponíveis:**
        - Por categoria
        - Por faixa de preço  
        - Por disponibilidade em estoque
        - Busca textual por nome/descrição
        
      parameters:
        - name: category
          in: query
          description: Filtrar por categoria específica
          schema:
            type: string
            example: "electronics"
        - name: min_price
          in: query
          description: Preço mínimo (inclusive)
          schema:
            type: number
            format: float
            minimum: 0
            example: 10.99
        - name: max_price
          in: query
          description: Preço máximo (inclusive)
          schema:
            type: number
            format: float
            minimum: 0
            example: 199.99
        - name: in_stock
          in: query
          description: Filtrar apenas produtos em estoque
          schema:
            type: boolean
            default: false
        - name: search
          in: query
          description: Busca textual em nome e descrição
          schema:
            type: string
            example: "smartphone"
        - name: sort
          in: query
          description: Campo para ordenação
          schema:
            type: string
            enum: [name, price, created_at, updated_at]
            default: created_at
        - name: order
          in: query
          description: Direção da ordenação
          schema:
            type: string
            enum: [asc, desc]
            default: desc
        - name: page
          in: query
          description: Número da página (baseado em 1)
          schema:
            type: integer
            minimum: 1
            default: 1
            example: 1
        - name: limit
          in: query
          description: Número de itens por página
          schema:
            type: integer
            minimum: 1
            maximum: 100
            default: 20
            example: 20
            
      responses:
        '200':
          description: Lista de produtos retornada com sucesso
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                    items:
                      $ref: '#/components/schemas/Product'
                  pagination:
                    $ref: '#/components/schemas/PaginationMeta'
                  filters:
                    type: object
                    description: Filtros aplicados na consulta
                    properties:
                      category: { type: string }
                      min_price: { type: number }
                      max_price: { type: number }
                      in_stock: { type: boolean }
                      search: { type: string }
              examples:
                produtos_electronics:
                  summary: Produtos da categoria Electronics
                  value:
                    data:
                      - id: 1
                        name: "iPhone 14 Pro"
                        description: "Smartphone Apple com chip A16 Bionic"
                        price: 1299.99
                        category: "electronics"
                        stock: 25
                        images: ["https://cdn.ecommerce.com/iphone14pro-1.jpg"]
                        created_at: "2024-01-15T10:30:00Z"
                        updated_at: "2024-06-20T14:22:00Z"
                    pagination:
                      page: 1
                      limit: 20
                      total: 156
                      pages: 8
                      has_next: true
                      has_prev: false
                    filters:
                      category: "electronics"
                      in_stock: true
        '400':
          $ref: '#/components/responses/BadRequest'
        '500':
          $ref: '#/components/responses/InternalError'

    post:
      tags: [Products]
      summary: Cria um novo produto
      description: |
        Adiciona um novo produto ao catálogo.
        
        **Validações aplicadas:**
        - Nome único obrigatório
        - Preço deve ser positivo
        - Categoria deve existir
        - Estoque não pode ser negativo
        
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductInput'
            examples:
              smartphone:
                summary: Exemplo de Smartphone
                value:
                  name: "Samsung Galaxy S24"
                  description: "Smartphone Samsung com tela AMOLED de 6.8 polegadas"
                  price: 899.99
                  category: "electronics"
                  stock: 50
                  images: [
                    "https://cdn.ecommerce.com/galaxy-s24-1.jpg",
                    "https://cdn.ecommerce.com/galaxy-s24-2.jpg"
                  ]
                  attributes:
                    brand: "Samsung"
                    model: "Galaxy S24"
                    color: "Phantom Black"
                    storage: "256GB"
              livro:
                summary: Exemplo de Livro
                value:
                  name: "Clean Code"
                  description: "Handbook of Agile Software Craftsmanship"
                  price: 45.90
                  category: "books"
                  stock: 100
                  attributes:
                    author: "Robert C. Martin"
                    isbn: "978-0132350884"
                    pages: 464
                    language: "English"
                    
      responses:
        '201':
          description: Produto criado com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
              example:
                id: 157
                name: "Samsung Galaxy S24"
                description: "Smartphone Samsung com tela AMOLED de 6.8 polegadas"
                price: 899.99
                category: "electronics"
                stock: 50
                images: ["https://cdn.ecommerce.com/galaxy-s24-1.jpg"]
                attributes:
                  brand: "Samsung"
                  model: "Galaxy S24"
                created_at: "2024-06-26T07:54:00Z"
                updated_at: "2024-06-26T07:54:00Z"
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'
        '409':
          description: Produto com este nome já existe
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
              example:
                error: "DUPLICATE_PRODUCT"
                message: "Já existe um produto com o nome 'Samsung Galaxy S24'"
                details:
                  field: "name"
                  existing_id: 145
        '500':
          $ref: '#/components/responses/InternalError'

  /products/{id}:
    parameters:
      - name: id
        in: path
        required: true
        description: ID único do produto
        schema:
          type: integer
          minimum: 1
          example: 1

    get:
      tags: [Products]
      summary: Busca produto por ID
      description: Retorna informações detalhadas de um produto específico
      responses:
        '200':
          description: Produto encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
              example:
                id: 1
                name: "iPhone 14 Pro"
                description: "Smartphone Apple com chip A16 Bionic e câmera Pro de 48MP"
                price: 1299.99
                category: "electronics"
                stock: 25
                images: [
                  "https://cdn.ecommerce.com/iphone14pro-1.jpg",
                  "https://cdn.ecommerce.com/iphone14pro-2.jpg"
                ]
                attributes:
                  brand: "Apple"
                  model: "iPhone 14 Pro"
                  color: "Deep Purple"
                  storage: "128GB"
                created_at: "2024-01-15T10:30:00Z"
                updated_at: "2024-06-20T14:22:00Z"
        '404':
          $ref: '#/components/responses/NotFound'
        '500':
          $ref: '#/components/responses/InternalError'

    put:
      tags: [Products]
      summary: Atualiza produto completo
      description: |
        Substitui completamente os dados de um produto existente.
        Todos os campos obrigatórios devem ser fornecidos.
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductInput'
      responses:
        '200':
          description: Produto atualizado com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'
        '404':
          $ref: '#/components/responses/NotFound'
        '409':
          description: Conflito de dados (ex: nome duplicado)
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
        '500':
          $ref: '#/components/responses/InternalError'

    patch:
      tags: [Products]
      summary: Atualiza produto parcialmente
      description: |
        Atualiza apenas os campos fornecidos do produto.
        Campos não fornecidos mantêm seus valores atuais.
      security:
        - bearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductPartialInput'
            examples:
              preco_estoque:
                summary: Atualizando preço e estoque
                value:
                  price: 1199.99
                  stock: 15
              categoria:
                summary: Mudando categoria
                value:
                  category: "premium-electronics"
      responses:
        '200':
          description: Produto atualizado com sucesso
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Product'
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'  
        '404':
          $ref: '#/components/responses/NotFound'
        '500':
          $ref: '#/components/responses/InternalError'

    delete:
      tags: [Products]
      summary: Remove produto
      description: |
        Remove permanentemente um produto do catálogo.
        **Atenção:** Esta ação não pode ser desfeita.
      security:
        - bearerAuth: []
      responses:
        '204':
          description: Produto removido com sucesso
        '401':
          $ref: '#/components/responses/Unauthorized'
        '404':
          $ref: '#/components/responses/NotFound'
        '409':
          description: Produto não pode ser removido (ex: tem pedidos associados)
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
              example:
                error: "PRODUCT_IN_USE"
                message: "Produto não pode ser removido pois possui pedidos associados"
                details:
                  active_orders: 5
                  last_order_date: "2024-06-25T10:30:00Z"
        '500':
          $ref: '#/components/responses/InternalError'

  /products/category/{category}:
    parameters:
      - name: category
        in: path
        required: true
        description: Nome da categoria (case-insensitive)
        schema:
          type: string
          example: "electronics"
        examples:
          electronics:
            summary: Eletrônicos
            value: "electronics"
          books:
            summary: Livros
            value: "books"
          clothing:
            summary: Roupas
            value: "clothing"

    get:
      tags: [Products, Categories]
      summary: Busca produtos por categoria
      description: |
        Retorna todos os produtos de uma categoria específica.
        Suporta os mesmos filtros e paginação do endpoint principal.
      parameters:
        - name: min_price
          in: query
          schema:
            type: number
            format: float
            minimum: 0
        - name: max_price
          in: query
          schema:
            type: number  
            format: float
            minimum: 0
        - name: in_stock
          in: query
          schema:
            type: boolean
            default: false
        - name: sort
          in: query
          schema:
            type: string
            enum: [name, price, created_at, updated_at]
            default: created_at
        - name: order
          in: query
          schema:
            type: string
            enum: [asc, desc]
            default: desc
        - name: page
          in: query
          schema:
            type: integer
            minimum: 1
            default: 1
        - name: limit
          in: query
          schema:
            type: integer
            minimum: 1
            maximum: 100
            default: 20
            
      responses:
        '200':
          description: Produtos da categoria encontrados
          content:
            application/json:
              schema:
                type: object
                properties:
                  data:
                    type: array
                    items:
                      $ref: '#/components/schemas/Product'
                  category_info:
                    type: object
                    properties:
                      name: { type: string }
                      description: { type: string }
                      total_products: { type: integer }
                  pagination:
                    $ref: '#/components/schemas/PaginationMeta'
              example:
                data:
                  - id: 1
                    name: "iPhone 14 Pro"
                    category: "electronics"
                    price: 1299.99
                  - id: 2
                    name: "MacBook Pro M2"
                    category: "electronics"
                    price: 2499.99
                category_info:
                  name: "electronics"
                  description: "Dispositivos eletrônicos e gadgets"
                  total_products: 156
                pagination:
                  page: 1
                  limit: 20
                  total: 156
                  pages: 8
        '404':
          description: Categoria não encontrada
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
              example:
                error: "CATEGORY_NOT_FOUND"
                message: "Categoria 'invalid-category' não existe"
                details:
                  available_categories: ["electronics", "books", "clothing", "home"]
        '500':
          $ref: '#/components/responses/InternalError'

components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
      description: |
        Token JWT obtido através do endpoint de autenticação.
        Formato: `Authorization: Bearer <token>`

  schemas:
    Product:
      type: object
      required: [id, name, price, category, stock, created_at, updated_at]
      properties:
        id:
          type: integer
          description: Identificador único do produto
          example: 1
          readOnly: true
        name:
          type: string
          description: Nome do produto (deve ser único)
          minLength: 1
          maxLength: 200
          example: "iPhone 14 Pro"
        description:
          type: string
          description: Descrição detalhada do produto
          maxLength: 2000
          example: "Smartphone Apple com chip A16 Bionic e câmera Pro de 48MP"
        price:
          type: number
          format: float
          description: Preço do produto em reais
          minimum: 0.01
          maximum: 999999.99
          example: 1299.99
        category:
          type: string
          description: Categoria do produto
          enum: [electronics, books, clothing, home, sports, beauty, automotive]
          example: "electronics"
        stock:
          type: integer
          description: Quantidade disponível em estoque
          minimum: 0
          maximum: 999999
          example: 25
        images:
          type: array
          description: URLs das imagens do produto
          maxItems: 10
          items:
            type: string
            format: uri
            example: "https://cdn.ecommerce.com/produto-1.jpg"
        attributes:
          type: object
          description: Atributos específicos do produto (flexível por categoria)
          additionalProperties: true
          example:
            brand: "Apple"
            model: "iPhone 14 Pro"
            color: "Deep Purple"
            storage: "128GB"
        tags:
          type: array
          description: Tags para facilitar busca e categorização
          maxItems: 20
          items:
            type: string
            maxLength: 50
          example: ["smartphone", "apple", "premium", "5g"]
        created_at:
          type: string
          format: date-time
          description: Data e hora de criação do produto
          example: "2024-01-15T10:30:00Z"
          readOnly: true
        updated_at:
          type: string
          format: date-time
          description: Data e hora da última atualização
          example: "2024-06-20T14:22:00Z"
          readOnly: true
          
    ProductInput:
      type: object
      required: [name, price, category, stock]
      properties:
        name:
          type: string
          description: Nome único do produto
          minLength: 1
          maxLength: 200
          example: "Samsung Galaxy S24"
        description:
          type: string
          description: Descrição detalhada do produto
          maxLength: 2000
          example: "Smartphone Samsung com tela AMOLED de 6.8 polegadas"
        price:
          type: number
          format: float
          description: Preço do produto em reais
          minimum: 0.01
          maximum: 999999.99
          example: 899.99
        category:
          type: string
          description: Categoria do produto
          enum: [electronics, books, clothing, home, sports, beauty, automotive]
          example: "electronics"
        stock:
          type: integer
          description: Quantidade inicial em estoque
          minimum: 0
          maximum: 999999
          example: 50
        images:
          type: array
          description: URLs das imagens do produto
          maxItems: 10
          items:
            type: string
            format: uri
          example: ["https://cdn.ecommerce.com/galaxy-s24-1.jpg"]
        attributes:
          type: object
          description: Atributos específicos do produto
          additionalProperties: true
          example:
            brand: "Samsung"
            model: "Galaxy S24"
            color: "Phantom Black"
            storage: "256GB"
        tags:
          type: array
          description: Tags para busca e categorização
          maxItems: 20
          items:
            type: string
            maxLength: 50
          example: ["smartphone", "samsung", "android"]
            
    ProductPartialInput:
      type: object
      description: Schema para atualizações parciais - todos os campos são opcionais
      properties:
        name:
          type: string
          minLength: 1
          maxLength: 200
        description:
          type: string
          maxLength: 2000
        price:
          type: number
          format: float
          minimum: 0.01
          maximum: 999999.99
        category:
          type: string
          enum: [electronics, books, clothing, home, sports, beauty, automotive]
        stock:
          type: integer
          minimum: 0
          maximum: 999999
        images:
          type: array
          maxItems: 10
          items:
            type: string
            format: uri
        attributes:
          type: object
          additionalProperties: true
        tags:
          type: array
          maxItems: 20
          items:
            type: string
            maxLength: 50
    
    PaginationMeta:
      type: object
      description: Metadados de paginação
      required: [page, limit, total, pages]
      properties:
        page:
          type: integer
          description: Página atual (baseada em 1)
          minimum: 1
          example: 1
        limit:
          type: integer
          description: Itens por página
          minimum: 1
          maximum: 100
          example: 20
        total:
          type: integer
          description: Total de itens disponíveis
          minimum: 0
          example: 156
        pages:
          type: integer
          description: Total de páginas
          minimum: 0
          example: 8
        has_next:
          type: boolean
          description: Indica se existe próxima página
          example: true
        has_prev:
          type: boolean
          description: Indica se existe página anterior
          example: false
        next_page:
          type: integer
          description: Número da próxima página (se existir)
          nullable: true
          example: 2
        prev_page:
          type: integer
          description: Número da página anterior (se existir)  
          nullable: true
          example: null

    Error:
      type: object
      required: [error, message]
      properties:
        error:
          type: string
          description: Código de erro para identificação programática
          example: "VALIDATION_ERROR"
        message:
          type: string
          description: Mensagem de erro legível para humanos
          example: "Os dados fornecidos são inválidos"
        details:
          type: object
          description: Informações adicionais sobre o erro
          additionalProperties: true
          example:
            field: "price"
            value: -10.50
            constraint: "must be positive"
        timestamp:
          type: string
          format: date-time
          description: Momento em que o erro ocorreu
          example: "2024-06-26T07:54:00Z"
        request_id:
          type: string
          description: ID único da requisição para rastreamento
          example: "req_abc123def456"

  responses:
    BadRequest:
      description: Requisição inválida - dados malformados ou validação falhou
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          examples:
            validation_error:
              summary: Erro de validação
              value:
                error: "VALIDATION_ERROR"
                message: "Os dados fornecidos são inválidos"
                details:
                  errors:
                    - field: "price"
                      message: "deve ser um número positivo"
                    - field: "name"
                      message: "é obrigatório"
                timestamp: "2024-06-26T07:54:00Z"
                request_id: "req_abc123"
            malformed_json:
              summary: JSON malformado
              value:
                error: "MALFORMED_JSON"
                message: "O corpo da requisição contém JSON inválido"
                details:
                  position: 45
                  character: "}"
                timestamp: "2024-06-26T07:54:00Z"
                request_id: "req_def456"

    Unauthorized:
      description: Não autorizado - token ausente ou inválido
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            error: "UNAUTHORIZED"
            message: "Token de acesso inválido ou expirado"
            details:
              reason: "token_expired"
              expired_at: "2024-06-25T10:30:00Z"
            timestamp: "2024-06-26T07:54:00Z"
            request_id: "req_ghi789"

    NotFound:
      description: Recurso não encontrado
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          examples:
            product_not_found:
              summary: Produto não encontrado
              value:
                error: "PRODUCT_NOT_FOUND"
                message: "Produto com ID 999 não foi encontrado"
                details:
                  resource_type: "product"
                  resource_id: 999
                timestamp: "2024-06-26T07:54:00Z"
                request_id: "req_jkl012"
            category_not_found:
              summary: Categoria não encontrada
              value:
                error: "CATEGORY_NOT_FOUND"
                message: "Categoria 'invalid-category' não existe"
                details:
                  resource_type: "category"
                  resource_name: "invalid-category"
                  available_categories: ["electronics", "books", "clothing"]
                timestamp: "2024-06-26T07:54:00Z"
                request_id: "req_mno345"

    InternalError:
      description: Erro interno do servidor
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            error: "INTERNAL_SERVER_ERROR"
            message: "Ocorreu um erro interno no servidor"
            details:
              incident_id: "inc_789abc"
              support_contact: "suporte@ecommerce.com"
            timestamp: "2024-06-26T07:54:00Z"
            request_id: "req_pqr678"

  examples:
    ProductElectronics:
      summary: Produto Eletrônico
      value:
        id: 1
        name: "iPhone 14 Pro"
        description: "Smartphone Apple com chip A16 Bionic"
        price: 1299.99
        category: "electronics"
        stock: 25
        images: ["https://cdn.ecommerce.com/iphone14pro-1.jpg"]
        attributes:
          brand: "Apple"
          model: "iPhone 14 Pro"
        created_at: "2024-01-15T10:30:00Z"
        updated_at: "2024-06-20T14:22:00Z"
        
    ProductBook:
      summary: Livro
      value:
        id: 50
        name: "Clean Code"
        description: "A Handbook of Agile Software Craftsmanship"
        price: 45.90
        category: "books"
        stock: 100
        images: ["https://cdn.ecommerce.com/clean-code.jpg"]
        attributes:
          author: "Robert C. Martin"
          isbn: "978-0132350884"
          pages: 464
          language: "English"
        tags: ["programming", "software", "agile"]
        created_at: "2024-02-10T08:15:00Z"
        updated_at: "2024-06-18T16:45:00Z"
🎉 Parabéns! Esta especificação demonstra:

✅ Completude total - Todos os endpoints CRUD implementados
✅ Schemas robustos - Validações detalhadas e exemplos realistas
✅ Tratamento de erros completo - Códigos apropriados com detalhes
✅ Documentação profissional - Descrições claras e exemplos práticos
✅ Funcionalidades avançadas - Paginação, filtros, busca e autenticação
✅ Boas práticas - Uso de tags, security schemes e componentes reutilizáveis

</details>
🎉 Certificado de Conclusão
🏆 PARABÉNS!

Você completou com sucesso o Curso de Swagger com JavaScript!

╔══════════════════════════════════════════════════════════════╗
║                    CERTIFICADO DE CONCLUSÃO                  ║
╠══════════════════════════════════════════════════════════════╣
║                                                              ║
║  📋 Curso: Swagger com JavaScript                           ║
║  👤 Aluno: Luan Oliveira dos Santos                         ║
║  📅 Conclusão: 26 de Junho de 2024                         ║
║  🏅 Nota: Excelente                                         ║
║                                                              ║
║  ✅ Módulos Concluídos:                                     ║
║     • Introdução ao Swagger                                 ║
║     • Conceitos Fundamentais                                ║
║     • Prática com JavaScript                                ║
║     • Exercícios Interativos                                ║
║                                                              ║
║  🎯 Habilidades Desenvolvidas:                              ║
║     • Leitura e criação de specs OpenAPI                   ║
║     • Integração Swagger com JavaScript                     ║
║     • Documentação profissional de APIs                     ║
║     • Testes e validação de endpoints                       ║
║                                                              ║
╚══════════════════════════════════════════════════════════════╝
Continue praticando e explorando APIs com Swagger! 🚀

🚀 Recursos Adicionais
📚 Documentação Oficial
Swagger Official Docs - Documentação completa
OpenAPI Specification - Especificação oficial
Swagger Editor - Editor online
Swagger Hub - Plataforma colaborativa
🛠️ Ferramentas Essenciais
Swagger UI - Interface de documentação
Swagger Codegen - Geração de código
Postman - Testes de API
Insomnia - Cliente REST alternativo
📖 Exemplos e Tutoriais
Pet Store Demo - API de exemplo clássica
Real World APIs - Specs reais
Swagger Tutorial - Tutoriais oficiais
OpenAPI Generator - Gerador avançado
🎓 Próximos Passos
Nível Iniciante 👶
Pratique criando specs para suas APIs pessoais
Explore o Swagger Editor com diferentes cenários
Estude APIs públicas famosas (GitHub, Twitter, etc.)
Implemente Swagger UI em um projeto simples
Nível Intermediário 🏃‍♂️
Integre Swagger com frameworks (Express, FastAPI, Spring)
Configure autenticação OAuth2 e JWT
Implemente versionamento de APIs
Use Swagger Codegen para gerar clientes
Nível Avançado 🚀
Desenvolva plugins customizados para Swagger UI
Configure CI/CD com validação automática de specs
Implemente mock servers baseados em OpenAPI
Contribua para projetos open source do ecossistema
🎯 Desafios Práticos
Desafio 1: API de Blog 📝
Crie uma especificação completa para um sistema de blog com:

Posts, comentários e usuários
Sistema de autenticação
Upload de imagens
Busca avançada
Desafio 2: API de E-learning 🎓
Desenvolva uma API para plataforma educacional:

Cursos, módulos e aulas
Progresso do aluno
Sistema de avaliações
Certificados
Desafio 3: API de IoT 🌐
Projete uma API para dispositivos IoT:

Sensores e atuadores
Dados em tempo real
Alertas e notificações
Dashboard de monitoramento
🤝 Contribuição
Como Contribuir para Este Projeto
🐛 Reportar Bugs
Verifique se o bug já foi reportado
Use template de issue apropriado
Inclua informações de ambiente
Forneça passos para reproduzir
💡 Sugerir Melhorias
Descreva claramente a melhoria
Explique o valor para os usuários
Considere implementação alternativa
Inclua mockups se necessário
🔧 Contribuir com Código
# 1. Fork o repositório
git clone https://github.com/SEU-USUARIO/swagger-learning.git

# 2. Crie uma branch para sua feature
git checkout -b feature/nova-funcionalidade

# 3. Faça suas modificações
# ... código ...

# 4. Teste suas mudanças
npm test

# 5. Commit com mensagem descritiva  
git commit -m "feat: adiciona seção sobre autenticação OAuth2"

# 6. Push para sua branch
git push origin feature/nova-funcionalidade

# 7. Abra um Pull Request
📋 Guidelines de Contribuição
Código: Siga padrões de formatação estabelecidos
Documentação: Mantenha README atualizado
Testes: Inclua testes para novas funcionalidades
Commits: Use Conventional Commits
🌟 Hall da Fama
Contribuidores que ajudaram a tornar este projeto melhor:

@luanoliveira - Criador e mantenedor principal
@contributor1 - Melhorias na documentação
@contributor2 - Novos exercícios interativos
@contributor3 - Correções de bugs importantes
📜 Licença
Este projeto está licenciado sob a MIT License.

MIT License

Copyright (c) 2024 Luan Oliveira dos Santos

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
🙏 Agradecimentos
Inspirações e Referências
Swagger Team - Pela ferramenta incrível e documentação
OpenAPI Initiative - Pelo padrão aberto e colaborativo
Comunidade JavaScript - Pelas melhores práticas e feedback
Stack Overflow - Pelas soluções e discussões
Ferramentas e Bibliotecas Utilizadas
Tailwind CSS - Framework CSS fantástico
Google Fonts - Tipografia de qualidade
GitHub - Hospedagem e colaboração
Markdown - Linguagem de marcação
Comunidade
Um agradecimento especial a todos que:

Testaram o material educacional
Forneceram feedback construtivo
Compartilharam conhecimento
Contribuíram com melhorias
<div align="center">
Desenvolvido com ❤️ para a comunidade de desenvolvedores

⭐ Star no GitHub • 🐛 Reportar Bug • 💡 Sugerir Feature

Continue explorando e construindo APIs incríveis! 🚀

Última atualização: 26 de Junho de 2024

</div> ```
📁 Instruções para uso:

Copie o código acima e cole em um arquivo novo
Salve como: swagger-learning-guide.md
Ou baixe direto: Você pode usar qualquer editor de texto ou IDE
🎯 O arquivo está pronto para:

✅ Funcionar perfeitamente no GitHub/GitLab
✅ Ser visualizado em qualquer leitor de markdown
✅ Ser convertido para PDF ou HTML
✅ Servir como documentação oficial
