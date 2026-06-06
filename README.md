# iPhone Barato · Sales Game 🏆

App de gamificação de vendas para a loja **iPhone Barato**. Ranking, pontos,
conquistas e campanhas — com banco de dados real compartilhado entre toda a equipe.

> **Stack:** React + Vite (front-end) · Supabase (banco) · Vercel (hospedagem).
> Tudo com planos gratuitos.

---

## 🚀 Publicar do zero (passo a passo)

Você vai fazer 3 coisas: (1) criar o banco no Supabase, (2) subir o código no
GitHub, (3) publicar na Vercel. Leva ~20 minutos.

### Pré-requisitos
- Uma conta no [GitHub](https://github.com) (grátis)
- Node.js instalado para testar localmente — opcional ([baixar aqui](https://nodejs.org))

---

### 1️⃣ Criar o banco de dados (Supabase)

1. Acesse [supabase.com](https://supabase.com) e crie uma conta.
2. Clique em **New project**. Dê um nome (ex: `iphone-barato`), defina uma senha
   de banco e escolha a região mais próxima (ex: South America / São Paulo).
3. Espere o projeto terminar de criar (~2 min).
4. No menu lateral, abra **SQL Editor** → **New query**.
5. Abra o arquivo [`supabase-setup.sql`](./supabase-setup.sql) deste projeto,
   copie **todo o conteúdo**, cole no editor e clique em **Run**.
   - Isso cria a tabela `app_state` e libera o acesso.
6. Agora pegue suas chaves: menu lateral → **Project Settings** (engrenagem) →
   **API**. Anote dois valores:
   - **Project URL** → algo como `https://xxxxx.supabase.co`
   - **anon public** key → uma chave longa começando com `eyJ...`

> ⚠️ Use **apenas** a chave `anon public`. Nunca exponha a `service_role`.

---

### 2️⃣ Subir o código no GitHub

**Opção A — sem terminal (mais simples):**
1. No GitHub, clique em **New repository**, nomeie (ex: `iphone-barato-app`),
   deixe **Private** e crie.
2. Na página do repositório vazio, clique em **uploading an existing file**.
3. Arraste **todos os arquivos desta pasta** (menos `node_modules` e `dist`,
   que não devem ir). Faça o commit.

**Opção B — com terminal:**
```bash
git init
git add .
git commit -m "iphone barato sales game"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/iphone-barato-app.git
git push -u origin main
```

---

### 3️⃣ Publicar na Vercel

1. Acesse [vercel.com](https://vercel.com) e entre com sua conta do GitHub.
2. Clique em **Add New → Project** e selecione o repositório que você acabou
   de subir.
3. A Vercel detecta o Vite automaticamente. Antes de clicar em Deploy, abra
   **Environment Variables** e adicione as duas chaves do Supabase:

   | Name                     | Value                                   |
   |--------------------------|-----------------------------------------|
   | `VITE_SUPABASE_URL`      | sua Project URL (`https://xxxxx...`)    |
   | `VITE_SUPABASE_ANON_KEY` | sua chave `anon public` (`eyJ...`)      |

4. Clique em **Deploy**. Em ~1 minuto seu app estará no ar num link tipo
   `https://iphone-barato-app.vercel.app` 🎉

> Sempre que você atualizar o código no GitHub, a Vercel republica sozinha.

---

## 🔑 Primeiro acesso

- **Gestor/Admin:** selecione "Gestor / Admin" e use a senha **`admin123`**.
- O app começa **vazio**. Como gestor, você:
  1. Cria a campanha do mês (aba **Campanhas** ou botão na tela inicial).
  2. Cadastra os vendedores (aba **Equipe**) — cada um com nome e senha.
  3. Começa a lançar pontos (botão central ⚡).
- **Vendedores:** entram selecionando o próprio nome + a senha que você definiu.

> 🔒 **Trocar a senha do admin:** abra `src/App.jsx`, procure por `admin123`
> e altere para a senha que quiser, depois faça commit (a Vercel republica).

---

## 💻 Rodar localmente (opcional)

```bash
npm install
cp .env.example .env     # preencha com suas chaves do Supabase
npm run dev              # abre em http://localhost:5173
```

---

## 📁 Estrutura

```
iphone-barato-app/
├── index.html              # ponto de entrada HTML
├── package.json            # dependências e scripts
├── vite.config.js          # config do Vite
├── vercel.json             # roteamento SPA na Vercel
├── supabase-setup.sql      # script p/ criar o banco
├── .env.example            # modelo das variáveis de ambiente
└── src/
    ├── main.jsx            # bootstrap do React
    └── App.jsx             # o app inteiro (telas, lógica, backend)
```

---

## ❓ Notas sobre segurança

Este app usa um login simples próprio (gestor/vendedor com senha), adequado para
**uso interno** de uma equipe de loja. As senhas ficam no banco junto com os
demais dados. Para um cenário com requisitos de segurança mais altos, o caminho
seria migrar para o **Supabase Auth** (login com e-mail/senha gerenciado pela
plataforma) — posso ajudar com isso depois, se precisar.
