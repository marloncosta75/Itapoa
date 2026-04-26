# 🌸 Itapoã — Guia Completo de Deploy + Google Drive

> App do casal Camila & Marlon. Senha: `161124`

---

## PARTE 1 — Subir no GitHub Pages (hosting gratuito)

### Passo 1 — Criar o repositório no GitHub

1. Acesse [github.com](https://github.com) e faça login
2. Clique em **New repository** (botão verde no canto superior direito)
3. Configure assim:
   - **Repository name:** `itapoa` (ou qualquer nome)
   - **Visibility:** Private ← importante para manter o app privado
   - **Add a README file:** deixe desmarcado
4. Clique em **Create repository**

### Passo 2 — Fazer upload do arquivo

1. Na página do repositório recém criado, clique em **Add file → Upload files**
2. Arraste o arquivo `itapoa.html` para a área de upload
3. Na caixa "Commit changes" escreva: `primeiro deploy`
4. Clique em **Commit changes**

### Passo 3 — Ativar o GitHub Pages

1. No repositório, clique em **Settings** (aba no topo)
2. No menu lateral esquerdo, clique em **Pages**
3. Em "Source", selecione **Deploy from a branch**
4. Em "Branch", selecione **main** e pasta **/ (root)**
5. Clique em **Save**
6. Aguarde ~2 minutos e recarregue a página
7. Aparecerá o link: `https://SEU_USUARIO.github.io/itapoa/`

> ⚠️ Repositórios privados com GitHub Pages gratuito precisam do plano Pro.
> Alternativa gratuita: tornar o repositório **público** (o app ainda é protegido por senha).

---

## PARTE 2 — Configurar Google Drive API

### Passo 1 — Criar projeto no Google Cloud

1. Acesse [console.cloud.google.com](https://console.cloud.google.com)
2. No topo, clique em **Select a project → New Project**
3. Nome: `Itapoã App`
4. Clique em **Create**
5. Aguarde criar e certifique-se que o projeto está selecionado no topo

### Passo 2 — Ativar as APIs necessárias

1. No menu lateral, vá em **APIs & Services → Library**
2. Pesquise por **Google Drive API** → clique → **Enable**
3. Volte à Library, pesquise **Google Identity** → já vem ativa, só confirme

### Passo 3 — Criar credencial OAuth 2.0

1. Vá em **APIs & Services → Credentials**
2. Clique em **+ Create Credentials → OAuth client ID**
3. Se aparecer "Configure consent screen", clique nele primeiro:
   - **User Type:** External → Create
   - **App name:** Itapoã
   - **User support email:** seu email
   - **Developer contact:** seu email
   - Clique em **Save and Continue** em todas as telas
   - Em "Test users", adicione seu email do Google
   - Clique em **Back to Dashboard**
4. Volte em **Credentials → + Create Credentials → OAuth client ID**
5. Configure:
   - **Application type:** Web application
   - **Name:** Itapoã Web
   - **Authorized JavaScript origins:** adicione sua URL do GitHub Pages
     ```
     https://SEU_USUARIO.github.io
     ```
   - Se quiser testar local também, adicione:
     ```
     http://localhost:8080
     ```
6. Clique em **Create**
7. Aparecerá uma janela com o **Client ID** — copie-o (parece com: `123456789-abc...apps.googleusercontent.com`)

### Passo 4 — Colar o Client ID no app

1. Abra o arquivo `itapoa.html` em qualquer editor de texto (Bloco de Notas, VS Code, etc.)
2. Localize a linha:
   ```javascript
   const GOOGLE_CLIENT_ID = 'SEU_CLIENT_ID_AQUI';
   ```
3. Substitua `SEU_CLIENT_ID_AQUI` pelo Client ID que você copiou:
   ```javascript
   const GOOGLE_CLIENT_ID = '123456789-abc.apps.googleusercontent.com';
   ```
4. Salve o arquivo

### Passo 5 — Publicar a atualização

1. No GitHub, vá ao repositório `itapoa`
2. Clique no arquivo `itapoa.html`
3. Clique no ícone de lápis ✏️ (Edit this file)
4. Selecione todo o conteúdo (Ctrl+A) e cole o novo conteúdo do arquivo atualizado
5. Clique em **Commit changes**
6. Aguarde ~1 minuto para o deploy atualizar

---

## PARTE 3 — Usar o Google Drive no app

1. Abra o app na sua URL do GitHub Pages
2. Entre com a senha `161124`
3. Vá na aba **❀ Biblioteca**
4. Clique no botão **Google Drive**
5. Aparecerá a tela de login do Google — entre com sua conta
6. Autorize o acesso às fotos
7. O app mostrará as últimas 50 imagens do seu Drive
8. Selecione as fotos que quiser importar
9. Clique em **Importar selecionadas ✦**
10. As fotos aparecem na biblioteca automaticamente!

---

## Resumo dos arquivos

```
itapoa.html   ← arquivo único do app (tudo incluído)
README.md     ← este guia
```

---

## Dúvidas frequentes

**O botão Drive aparece mas não faz nada**
→ O Client ID ainda está como `SEU_CLIENT_ID_AQUI`. Siga o Passo 4 da Parte 2.

**Erro "redirect_uri_mismatch"**
→ A URL do GitHub Pages não está cadastrada no Google Cloud. Verifique o Passo 3 (Authorized JavaScript origins).

**"This app isn't verified"**
→ Normal em modo de teste. Clique em "Advanced" → "Go to Itapoã (unsafe)". Para remover esse aviso precisaria verificar o app no Google — não é necessário para uso pessoal.

**As fotos não aparecem no picker**
→ O Google Drive só mostra arquivos de imagem (`image/*`). Certifique-se que as fotos estão no Drive e não em pasta compartilhada de terceiros.

**Quero que o Drive também faça upload automático das fotos que adiciono no app**
→ Isso requer escopo de escrita (`drive.file`) e um backend. Fala comigo que a gente implementa!

---

*Com amor, para Camila & Marlon ✦*
