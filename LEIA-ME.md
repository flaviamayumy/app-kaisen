# KAISEN · Área do aluno (versão 1: login)

Por enquanto o app tem só o login por **e-mail e senha**, para você e para os seus alunos. Depois de entrar, aparece uma tela vazia com o mesmo fundo do site flaviamayumi.com.br.

- **Não existe "Criar conta" no app.** Só entra quem tem conta criada por você.
- **Custo: R$ 0 por mês.** O login fica no Supabase (plano Free) e a hospedagem no GitHub Pages.

---

## 1. Criar o projeto no Supabase (uma vez só)

1. Entre em **supabase.com** e crie uma conta grátis. Pode entrar com o GitHub.
2. Clique em **New project**:
   - Em **Region**, escolha **South America (São Paulo)**.
   - Crie uma senha forte para o banco e guarde-a.
3. Quando o projeto ficar pronto, vá em **Authentication → Sign In / Providers**:
   - Desligue **Allow new users to sign up**. Assim ninguém cria conta sozinho.
   - Em **Email**, deixe o provedor **ligado**.
4. Vá em **Authentication → URL Configuration**:
   - Em **Site URL**, coloque `https://app.flaviamayumi.com.br`.
   - Em **Redirect URLs**, adicione o mesmo endereço. É ele que faz o link de "Esqueci minha senha" funcionar.
5. Vá em **Project Settings → API** (ou **Data API**) e copie dois valores:
   - **Project URL**
   - **anon public key** (em alguns painéis aparece como "publishable key")

## 2. Colocar as chaves no app

Abra o `config.js` e preencha:

```js
supabaseUrl: "https://xxxxxxxx.supabase.co",
supabaseAnonKey: "eyJhbGciOi...",
```

A chave "anon" é feita para ficar no app. **Nunca** use a chave `service_role` no app.

## 3. Publicar no GitHub Pages

1. No GitHub, crie um repositório novo, por exemplo `app-kaisen`.
2. Envie todos os arquivos desta pasta pelo botão **Add file → Upload files**.
3. Vá em **Settings → Pages**:
   - Em **Source**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`, e salve.
   - Em **Custom domain**, digite `app.flaviamayumi.com.br` e salve. Marque **Enforce HTTPS** quando a opção aparecer.
4. No **Registro.br**, abra a zona DNS do flaviamayumi.com.br e crie um registro:
   - Tipo: **CNAME**
   - Nome: **app**
   - Valor: **flaviamayumy.github.io**

O endereço pode levar de alguns minutos até algumas horas para funcionar.

## 4. Criar as contas (a sua e a de cada aluno)

No Supabase, vá em **Authentication → Users → Add user → Create new user**:

1. Digite o **e-mail** e uma **senha** (mínimo de 6 caracteres).
2. Deixe marcado **Auto Confirm User**.
3. Clique em **Create user**.

Faça isso primeiro para você e depois para cada aluno. Mande para o aluno o endereço do app, o e-mail e a senha. Ele pode trocar a senha depois em "Esqueci minha senha".

Para **tirar o acesso** de alguém, abra **Authentication → Users**, clique nos três pontinhos do usuário e escolha **Delete user**.

## 5. Instalar no celular

- **Android (Chrome):** abra o app e toque no menu (⋮) → **Instalar app** (ou **Adicionar à tela inicial**).
- **iPhone (Safari):** abra o app e toque em **Compartilhar** → **Adicionar à Tela de Início**.

---

## Bom saber

- **"Esqueci minha senha"** usa o e-mail grátis do Supabase, que manda poucos e-mails por hora. Para poucos alunos, é suficiente. Se um aluno não receber o e-mail, você pode trocar a senha dele em **Authentication → Users**.
- **Pausa por inatividade:** o Supabase grátis pausa o projeto depois de 7 dias sem nenhum acesso. Se acontecer, entre no painel e clique em **Restore**. Nada se perde.
- **Teste sem configurar nada:** com o `config.js` vazio, o app abre em modo demonstração. Entre com `aluno@demo.com` ou `treinadora@demo.com`, senha `demo123`.

## Arquivos

```
index.html            página do app
config.js             ← chaves do Supabase e textos da marca
css/app.css           visual e fundo (iguais aos do site)
js/app.js             login, recuperação de senha e tela inicial
sw.js                 deixa o app instalável
manifest.webmanifest  nome e ícone do app instalado
img/                  imagens do fundo do site
icons/                ícone do torii
```
