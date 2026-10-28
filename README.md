# Projeto GCS — ONGConecta

## Estrutura do Projeto

```text
Projeto_GCS_ONGconecta/
├── docs/                     # Documentação de GCS (Plano de Configuração e evidências)
│   ├── Plano_Gerenciamento_Configuracao.pdf
│   └── evidencias/
└── ongconecta-main/          # Código da aplicação
    ├── api/                  # Backend REST (Node.js + Express)
    ├── web/                  # Frontend Web (React + Vite)
    ├── mobile/               # App mobile (React Native + Expo)
    ├── scripts/              # Scripts de versionamento SemVer e smoke tests
    └── .github/workflows/    # Pipelines de CI/CD (GitHub Actions)
```

## Visão Geral do Código

- **`api/` (Backend)**: API REST simples feita com Express. Possui rota de verificação (`/health`) e rotas para listar e cadastrar doações (`/api/doacoes`). Os dados ficam salvos em memória e as regras de validação (e-mail, valores e tipos de pagamento) ficam isoladas em `src/validacao.js`.

- **`web/` (Frontend)**: Interface em React criada com Vite. Permite enviar novas doações e acompanhar as doações recebidas. Se a API não estiver conectada, o frontend roda automaticamente em modo demonstração local.

- **`mobile/` (Aplicativo)**: App em React Native (Expo) que lista campanhas sociais, exibe barra de progresso da meta e organiza por prazo de encerramento.

- **`scripts/` e CI/CD**: Scripts utilitários como `proxima-versao.mjs` (calcula a versão SemVer a partir dos Conventional Commits) e workflows do GitHub Actions para validar testes/lint nos PRs (`ci.yml`) e publicar em staging e produção no GitHub Pages (`cd.yml`).

## Dependências e Como Rodar

### 1. Instalação das dependências

O projeto é dividido em módulos. Instale as dependências entrando na pasta de cada um:

```bash
# API
cd ongconecta-main/api
npm install

# Web
cd ../web
npm install

# Mobile
cd ../mobile
npm install
```

### 2. Executando localmente

- **API:**
  ```bash
  cd ongconecta-main/api
  npm run dev
  ```
  Acessível em: `http://localhost:3000`

- **Web:**
  ```bash
  cd ongconecta-main/web
  npm run dev
  ```
  Acessível em: `http://localhost:5173`

- **Mobile:**
  ```bash
  cd ongconecta-main/mobile
  npm start
  ```
  
### 3. Rodando os testes

Para rodar os testes unitários de cada módulo:

```bash
# Testes da API
cd ongconecta-main/api && npm test

# Testes da Web
cd ongconecta-main/web && npm test

# Testes do Mobile
cd ongconecta-main/mobile && npm test

# Testes do script de versionamento
node --test ongconecta-main/scripts/proxima-versao.test.mjs
```

Para rodar os testes gerando relatório de cobertura (mínimo de 60% exigido no CI):
```bash
npm run test:coverage
```
