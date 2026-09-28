# API de Clientes

API REST para cadastro de clientes, reconstruída a partir do material da aula. Feita com Node.js, Express e MySQL.

## Iniciar no Windows

1. Instale Node.js 20 ou superior e Docker Desktop.
2. Abra um terminal nesta pasta e crie a configuração local:

   ```powershell
   Copy-Item .env.example .env
   ```

3. Inicie o banco de dados:

   ```powershell
   docker compose up -d
   ```

4. Instale as dependências e rode a API:

   ```powershell
   npm install
   npm run dev
   ```

A API ficará em `http://localhost:3000`. O MySQL cria a tabela `clientes` e dois registros de exemplo na primeira inicialização.

## Rotas

| Método | Caminho | Ação |
|---|---|---|
| GET | `/` | Confirma que a API está ativa |
| GET | `/health` | Verifica a disponibilidade HTTP |
| GET | `/clientes` | Lista clientes |
| GET | `/clientes/:id` | Busca um cliente |
| POST | `/clientes` | Cria um cliente |
| PUT | `/clientes/:id` | Substitui todos os dados editáveis |
| PATCH | `/clientes/:id` | Atualiza somente os campos enviados |
| DELETE | `/clientes/:id` | Exclui um cliente |

Exemplo de corpo para POST e PUT (PATCH aceita qualquer subconjunto não vazio):

```json
{
  "nome": "Carla",
  "sobrenome": "Oliveira",
  "idade": 25,
  "cidade": "São Paulo",
  "uf": "SP"
}
```

Envie `Content-Type: application/json`. Respostas de validação usam HTTP 400, registros ausentes usam 404 e uma exclusão bem-sucedida retorna 204. As credenciais de desenvolvimento ficam no `.env.example`; altere-as antes de qualquer uso público.

## Banco

Para parar o banco: `docker compose down`. Para apagar também os dados locais: `docker compose down -v`.
A estrutura da tabela está em `database/init.sql`. O script de inicialização do MySQL só roda quando o volume é criado pela primeira vez.
