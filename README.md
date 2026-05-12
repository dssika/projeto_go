# Nome do Projeto

Descrição breve do projeto.

## Pré-requisitos

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Como rodar o projeto

### 1. Clone o repositório

```bash
git clone <https://github.com/dssika/projeto_go.git>
cd <projeto_go>
```

### 2. Baixe as dependências

```bash
docker run --rm --network host -v $(pwd):/app -w /app golang:1.22 go mod vendor
```

> **Obs:** o `--network host` garante que o container consiga acessar a internet mesmo em ambientes com proxy.
> Se não funcionar, verifique se há proxy corporativo e passe as variáveis de ambiente:
> ```bash
> docker run --rm --network host \
>   -e HTTP_PROXY=$HTTP_PROXY \
>   -e HTTPS_PROXY=$HTTPS_PROXY \
>   -v $(pwd):/app -w /app \
>   golang:1.22 go mod vendor
> ```

### 3. Suba os containers

```bash
docker compose up
```

A aplicação estará disponível em [http://localhost:8080](http://localhost:8080).

## Serviços

| Serviço    | Descrição              | Porta |
|------------|------------------------|-------|
| `app`      | Aplicação Go (Gin)     | 8080  |
| `postgres` | Banco de dados         | 5432  |

## Variáveis de ambiente

As variáveis do banco já estão configuradas no `docker-compose.yml`:

| Variável            | Valor padrão |
|---------------------|--------------|
| `POSTGRES_USER`     | root         |
| `POSTGRES_PASSWORD` | root         |
| `POSTGRES_DB`       | root         |
