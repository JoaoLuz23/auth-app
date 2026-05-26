# Auth-App

**Visão geral**
- **Projeto**: aplicação simples em Laravel para autenticação e gerenciamento de conteúdo (categorias e posts).
- **Estrutura**: padrão MVC com modelos Eloquent, migrations, controllers, requests e views Blade.

**Recursos principais**
- **Autenticação**: cadastro, login e perfil de usuário.
- **Categorias**: criação e gerenciamento de categorias (`Categoria`).
- **Posts**: criação, edição, remoção e upload de imagem para posts (`Post`).

**Arquivos/Locais importantes**
- **Modelos**: [app/Models/Categoria.php](app/Models/Categoria.php), [app/Models/Post.php](app/Models/Post.php), [app/Models/Posts.php](app/Models/Posts.php), [app/Models/User.php](app/Models/User.php)
- **Migrations**: [database/migrations/2026_05_19_114050_categoria.php](database/migrations/2026_05_19_114050_categoria.php), [database/migrations/2026_05_19_114734_post.php](database/migrations/2026_05_19_114734_post.php), [database/migrations/2026_05_26_144213_add_image_to_posts_table.php](database/migrations/2026_05_26_144213_add_image_to_posts_table.php)
- **Views**: [resources/views/categorias](resources/views/categorias), [resources/views/posts](resources/views/posts), [resources/views/auth](resources/views/auth), [resources/views/profile](resources/views/profile), [resources/views/layouts](resources/views/layouts)
- **Rotas**: [routes/web.php](routes/web.php), [routes/auth.php](routes/auth.php)
- **Seeders / Factories**: [database/seeders/DatabaseSeeder.php](database/seeders/DatabaseSeeder.php), [database/factories/UserFactory.php](database/factories/UserFactory.php)

**Modelos e campos principais**
- `Categoria` ([app/Models/Categoria.php](app/Models/Categoria.php)):
	- Atributos preenchíveis: `name` (nome da categoria).
	- Migration cria a tabela `categorias` com `id`, `name`, `created_at`, `updated_at`.
- `Post` ([app/Models/Post.php](app/Models/Post.php)):
	- Atributos preenchíveis: `title`, `text`, `image`, `categorias_id`.
	- Relations: `categorias_id` é `foreignId` com constraint para `categorias` (deleta em cascade).
	- Accessor: `getImageUrlAttribute()` retorna a URL completa da imagem (`storage/`).
- `Posts` ([app/Models/Posts.php](app/Models/Posts.php)):
	- Arquivo presente, sem implementação (placeholder).
- `User` ([app/Models/User.php](app/Models/User.php)):
	- Atributos preenchíveis: `name`, `email`, `password`.
	- Casts: `email_verified_at` => `datetime`, `password` => `hashed`.

**Migrations (detalhes)**
- `2026_05_19_114050_categoria.php`: cria `categorias` com `id`, `name` e timestamps.
- `2026_05_19_114734_post.php`: cria `posts` com `id`, `title`, `text`, `categorias_id` (foreign key) e timestamps. `onDelete('cascade')` para a FK.
- `2026_05_26_144213_add_image_to_posts_table.php`: adiciona coluna `image` (string, nullable) à tabela `posts`.

**Controllers e validação**
- Os controllers estão em [app/Http/Controllers](app/Http/Controllers) e lidam com CRUD de categorias e posts, além das rotas de autenticação.
- Validações customizadas estão em [app/Http/Requests](app/Http/Requests).

**Como rodar o projeto (local)**
1. Instale dependências PHP/Composer e configure um servidor local (XAMPP, Laragon ou similar).
2. No diretório do projeto, instale dependências:

```bash
composer install
npm install
npm run build
```

3. Configure o `.env` (copie `.env.example` para `.env`) — configure `DB_` e `APP_URL`.
4. Gere a chave da aplicação:

```bash
php artisan key:generate
```

5. Rode migrations e seeders:

```bash
php artisan migrate --seed
```

6. Caso precise linkar storage (para imagens):

```bash
php artisan storage:link
```

7. Inicie o servidor local:

```bash
php artisan serve
```

Abra `http://localhost:8000` (ou o `APP_URL` configurado) e acesse as rotas de autenticação e os CRUDs de categorias/posts.

**Observações e próximos passos sugeridos**
- Revisar e implementar `app/Models/Posts.php` se necessário.
- Adicionar testes para fluxo de criação de `Categoria` e `Post` (tests/Feature).
- Melhorar upload e redimensionamento de imagens (usando `Intervention/Image` ou similar).

Se quiser, eu posso:
- Gerar um README mais enxuto ou em formato passo-a-passo para deploy.
- Adicionar exemplos de rotas e payloads JSON.
- Criar testes básicos para `Categoria` e `Post`.

---
Gerado automaticamente: resumo do projeto e instruções básicas em Português.
