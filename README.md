# Blog Strapi (JAMstack)

Este é um projeto de blog construído com a arquitetura **JAMstack**, utilizando:


- **Strapi CMS** como gerenciador de conteúdo (interface + API),
- **PostgreSQL** local via Docker como banco de dados,
- **Cloudinary** para upload e gerenciamento de imagens,

Todo o projeto é voltado para **estudos e prática**, rodando 100% localmente (sem servidores hospedados).

## 🔧 Tecnologias Utilizadas

- [Strapi](https://strapi.io/) (CMS headless)
- [PostgreSQL](https://www.postgresql.org/) via [Docker](https://www.docker.com/)
- [Cloudinary](https://cloudinary.com/) (armazenamento de imagens)
- [Docker Compose](https://docs.docker.com/compose/)

---

## ⚙️ Desenvolvimento Local

### 1. Clonar o projeto

```bash
git clone https://github.com/Truefenix/blog-strapi.git
cd blog-strapi
````

### 2. Subir o banco de dados com Docker

```bash
docker-compose up -d
```

> Certifique-se de ter o Docker instalado.

### 3. Criar o arquivo `.env`

Crie um arquivo `.env` na raiz do Strapi com:

```
# PostgreSQL
DATABASE_CLIENT=postgres
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_NAME=seu_banco
DATABASE_USERNAME=seu_usuario
DATABASE_PASSWORD=sua_senha

# Cloudinary
CLOUDINARY_NAME=seu_cloud_name
CLOUDINARY_KEY=sua_api_key
CLOUDINARY_SECRET=sua_api_secret

# App
APP_KEYS=chave_segura_aqui
API_TOKEN_SALT=token_salt
ADMIN_JWT_SECRET=jwt_admin
JWT_SECRET=jwt_geral
```

---

## 📦 Upload de Imagens com Cloudinary

No arquivo `config/plugins.js`, adicione:

```js
module.exports = ({ env }) => ({
  upload: {
    config: {
      provider: 'cloudinary',
      providerOptions: {
        cloud_name: env('CLOUDINARY_NAME'),
        api_key: env('CLOUDINARY_KEY'),
        api_secret: env('CLOUDINARY_SECRET'),
      },
    },
  },
});
```

---

## 🧩 Permissões de API

Para acessar os dados da API (ex: `/api/posts`):

0. Execute o projeto e acesse a interface `npm run develop` > `http://localhost:1337`
1. Vá em **Strapi Admin > Settings > Roles > Public**.
2. Marque as permissões `find` e `findOne` para o collection type `posts`.
3. Acesse:

```http
GET http://localhost:1337/api/posts
```

Para pegar autor ou imagens, use `populate`:

```http
GET http://localhost:1337/api/posts?populate=author,cover
```

Ou para todos os relacionamentos:

```http
GET http://localhost:1337/api/posts?populate=*
```

---

## 💻 Front-end com Next.js

O front-end deste projeto está disponível neste repositório: [blog-next](https://github.com/Truefenix/blog-next)

Ele foi criado utilizando Next.js com suporte a geração estática de páginas (SSG) e estilização com Styled Components.

A aplicação se conecta à API Strapi através de `http://localhost:1337/api/posts` ou da variável de ambiente `NEXT_PUBLIC_API_URL` configurada no arquivo `.env.local`.


---

## 🧪 Objetivo

Este projeto é um estudo prático da arquitetura JAMstack, CMS headless com Strapi, banco via Docker, imagens em nuvem (Cloudinary), e front-end desacoplado com Next.js.

---

## ✍️ Autor
<table align="center">
<tr>
<td align="center">
<a href="https://github.com/Truefenix">
<img src="https://avatars.githubusercontent.com/u/94227038?s=400&u=0c061da14bb3c2f5bf9de8467443f49d7068c365&v=4" width="150px;" alt="Truefenix image" />
<br />
<sub><b>Eduardo-Roque</b></sub>
</a>
</td>
</tr>
</table>

<h4 align="center">
By<a href="https://github.com/Truefenix" target="_blank"> Truefenix </a>✍️