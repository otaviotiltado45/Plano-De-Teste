### Plano de Testes para a API 

Este plano de testes visa garantir que a API do grupo funcione conforme esperado para as rotas de cadastro e login de jogadores. O plano inclui os seguintes componentes:

1. **Visão Geral**
2. **Ambiente de Teste**
3. **Casos de Teste**
4. **Procedimentos de Teste**
5. **Critérios de Aceitação**

### 1. Visão Geral
A API permite o cadastro e login de jogadores. As funcionalidades principais são:
- Cadastro de jogador (signup)
- Login de jogador

### 2. Ambiente de Teste
- **URL Base**: `http://localhost:3003`
- **Ferramentas de Teste**: Postman, curl, ferramentas de logging, e um banco de dados de teste
- **Dados de Teste**: Emails, senhas, e nomes fictícios para realizar os testes

### 3. Casos de Teste

#### 3.1 Cadastro de Jogador (POST /jogador/singup)
**Objetivo**: Verificar se um jogador pode ser cadastrado com sucesso.

**Cenários de Teste**:
- **Teste de Sucesso**: Cadastro com todos os campos corretos.
- **Teste com Email Existente**: Tentativa de cadastro com um email que já está em uso.
- **Teste com Campos Faltando**: Cadastro com campos obrigatórios ausentes.
- **Teste com Dados Inválidos**: Cadastro com dados inválidos, como email no formato incorreto ou telefone com caracteres não numéricos.

**Exemplo de Requisição**:
```bash
curl --location 'http://localhost:3003/jogador/singup' \
--data-raw '{
    "email": "testPlayer@test.com", 
    "senha": "test", 
    "nome": "joaoTeste", 
    "telefone": "32999999999"
}'
```

**Exemplo de Resposta de Sucesso**:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjAxOGY2YjMwLTZiMzgtNzZkYi1iNzJkLTA4ODM2NTFhMmM5NyIsImlhdCI6MTcxNTQ5MDI4NiwiZXhwIjoxNzE1NDkzODI2fQ.L7TUNrq8obs0F_KqYn9a09KVgRSzyJsVHvHyuOk1hvM"
}
```

#### 3.2 Login de Jogador (POST /jogador/login)
**Objetivo**: Verificar se um jogador pode realizar login com sucesso.

**Cenários de Teste**:
- **Teste de Sucesso**: Login com email e senha corretos.
- **Teste com Email Incorreto**: Tentativa de login com um email que não existe.
- **Teste com Senha Incorreta**: Tentativa de login com senha incorreta.
- **Teste com Campos Faltando**: Login com campos obrigatórios ausentes.

**Exemplo de Requisição**:
```bash
curl --location 'http://localhost:3003/jogador/login' \
--data-raw '{
    "email": "testPlayer@test.com", 
    "senha": "test"
}'
```

**Exemplo de Resposta de Sucesso**:
```json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjAxOGY2YjMwLTZiMzgtNzZkYi1iNzJkLTA4ODM2NTFhMmM5NyIsImlhdCI6MTcxNTQ5MzYyNiwiZXhwIjoxNzE1NDk3MTY2fQ.51cacZdjiM2n2gfE7qBuLaKD7nHhUQgiV14B1zB6eAE"
}
```

### 4. Procedimentos de Teste

1. **Preparação**:
   - Configurar o ambiente de teste, incluindo o servidor e o banco de dados.
   - Garantir que o banco de dados esteja em um estado limpo antes de cada teste.

2. **Execução dos Testes**:
   - Utilizar as ferramentas de teste (Postman, curl) para enviar requisições às rotas da API.
   - Verificar as respostas da API, comparando com os resultados esperados.
   - Registrar qualquer comportamento inesperado ou erro.

3. **Validação**:
   - Confirmar que as respostas e o comportamento da API estão de acordo com os requisitos especificados.
   - Validar que os tokens de autenticação recebidos são válidos e permitem acesso a rotas protegidas (se aplicável).

### 5. Critérios de Aceitação

- **Cadastro de Jogador**:
  - O jogador deve ser cadastrado com sucesso e receber um token de autenticação quando todos os dados são fornecidos corretamente.
  - A API deve retornar um erro apropriado para casos de email já existente, dados ausentes ou inválidos.

- **Login de Jogador**:
  - O jogador deve conseguir realizar login com sucesso e receber um token de autenticação quando as credenciais são corretas.
  - A API deve retornar um erro apropriado para email ou senha incorretos e para campos ausentes.

### Considerações Finais
Este plano de testes tem como objetivo garantir que as funcionalidades de cadastro e login da API do grupo funcionem corretamente e lidem de forma adequada com diferentes cenários. Recomenda-se que o grupo responsável pela implementação execute esses testes e registre os resultados para análise posterior.
