# 🎵 Musicaberta Dev

Este repositório contém o ambiente de desenvolvimento unificado para os projetos **frontend** e **backend** do Musicaberta, usando Docker Compose.

## 📦 Estrutura esperada

```bash
musicaberta-dev/
├── docker-compose.yml
├── .gitignore
├── README.md
├── musicaberta-frontend/   # Clonado manualmente (ignorado no Git)
└── musicaberta-backend/    # Clonado manualmente (ignorado no Git)
```

## 🚀 Pré-requisitos

- [Git](https://git-scm.com/)
- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

## 📥 Setup

1. Clone este repositório:
   ```bash
   git clone https://github.com/ProjetoEngenhariaII/musicaberta-dev.git
   cd musicaberta-dev
   ```

2. Clone os repositórios do frontend e backend **dentro da pasta `musicaberta-dev/`**:
   ```bash
   git clone https://github.com/ProjetoEngenhariaII/musicaberta-frontend.git
   git clone https://github.com/ProjetoEngenhariaII/musicaberta-backend.git
   ```

3. Verifique se a estrutura de pastas está assim:
   ```
   musicaberta-dev/
   ├── docker-compose.yml
   ├── .gitignore
   ├── musicaberta-frontend/
   └── musicaberta-backend/
   ```

> ❗ Esses diretórios estão listados no `.gitignore`, então não serão versionados.

## ⚙️ Variáveis de ambiente

Crie os arquivos `.env` nos projetos `musicaberta-frontend/` e `musicaberta-backend/`.

Exemplo para `musicaberta-backend/.env`:

```env
DATABASE_URL=postgresql://postgres:prisma@postgres_db:5432/postgres
STORAGE_URL=http://minio:9000
MINIO_ROOT_USER=minio
MINIO_ROOT_PASSWORD=minio123
```

Exemplo para `musicaberta-frontend/.env`:

```env
NEXT_PUBLIC_API_URL_BROWSER=http://localhost:3333
NEXT_PUBLIC_API_URL_INTERNAL=http://backend:3333
```

## 🐳 Subindo o ambiente

Execute:

```bash
docker-compose up --build
```

Este comando irá:

- Criar um banco de dados PostgreSQL
- Subir o backend (`localhost:3333`)
- Subir o frontend (`localhost:3000`)
- Iniciar o Prisma Studio (`localhost:5555`)
- Subir o MinIO (`localhost:9000` | Console: `localhost:9001`)

## 🗂️ Buckets públicos no MinIO

Para o correto funcionamento do sistema, é necessário que os buckets `avatars` e `sheets` existam no MinIO e estejam configurados como públicos.

### Como criar

1. Acesse o console MinIO: [http://localhost:9001](http://localhost:9001)  
   Login:  
   - **Usuário:** `minio`  
   - **Senha:** `minio123`

2. Crie dois buckets com os nomes `avatars` e `sheets`.

3. Para cada bucket, defina a seguinte política de acesso (Access Policy) para: `Public`

## ❗ Dicas para desenvolvimento

- Alterações nos arquivos locais são refletidas automaticamente nos containers (hot reload).
- Use o Prisma Studio para explorar o banco.
- Certifique-se de que as portas 3000, 3333, 5432 e 5555 estão livres.

