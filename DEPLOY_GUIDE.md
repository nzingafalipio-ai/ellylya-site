# Guia Completo: Como Enviar o Site ao Cliente

## Resumo das Opções

Existem 3 formas principais de enviar e publicar o site. Escolha a que melhor se adapta ao seu caso:

| Opção | Facilidade | Custo | Melhor para |
|-------|-----------|-------|-----------|
| **Netlify** (Recomendado) | Fácil | Grátis (com upgrade opcional) | Sites estáticos, Netlify CMS, domínios personalizados |
| **GitHub Pages** | Fácil | Grátis | Projetos públicos, sem Netlify CMS |
| **Servidor FTP/Hosting tradicional** | Média | 5-50€/mês | Agências com servidores já contratados |

---

## **OPÇÃO 1: Deploy via Netlify (RECOMENDADO)**

### O que é Netlify?
Netlify é uma plataforma que hospeda sites estáticos gratuitamente. Oferece:
- Deploy automático a partir do GitHub
- Netlify CMS integrado (admin panel)
- SSL/HTTPS grátis
- Domínio personalizado
- Redirects, headers, functions

### Passo 1: Preparar o Repositório Git

Abra PowerShell na pasta do seu projeto (`c:\Users\figue\Desktop\index.html\`) e execute:

```powershell
cd 'c:\Users\figue\Desktop\index.html'

# Verificar se git está iniciado
git status

# Se não estiver, inicializar (se já estiver, pule este passo)
git init

# Adicionar todos os ficheiros
git add .

# Fazer commit
git commit -m "Site + Netlify CMS + configuração"

# Renomear branch para main (se necessário)
git branch -M main

# Adicionar repositório remoto (substituir SEU_USUARIO/SEU_REPO)
git remote add origin https://github.com/SEU_USUARIO/SEU_REPO.git

# Enviar para GitHub
git push -u origin main
```

**Se o repositório já existe e tem alterações:**
```powershell
git add .
git commit -m "Atualizações do site"
git push
```

### Passo 2: Criar Conta no Netlify

1. Abra https://app.netlify.com
2. Clique em **"Sign up"** (ou faça login se já tiver conta)
3. Escolha **"GitHub"** como método (ou Google, GitLab, etc.)
4. Autorize Netlify a aceder ao GitHub
5. Confirme o e-mail

### Passo 3: Adicionar o Site ao Netlify

1. Em https://app.netlify.com, clique em **"Add new site"** → **"Import from Git"**
2. Escolha **"GitHub"** como provedor
3. Selecione o repositório que criou (ex: `SEU_USUARIO/SEU_REPO`)
4. Preencha os campos:
   - **Build command**: deixe vazio (é um site estático)
   - **Publish directory**: `/` (a raiz do projeto)
5. Clique em **"Deploy site"**
6. Aguarde o deploy (2-3 minutos)

### Passo 4: Verificar o Domínio Temporário

Após deploy:
- Netlify atribui automaticamente um URL: `https://NOME-ALEATORIO.netlify.app`
- Este URL será enviado ao seu cliente temporariamente

### Passo 5: Adicionar Domínio Personalizado (Opcional)

Se o cliente tem um domínio (ex: `seudominio.com`):

1. No painel do site em Netlify → **"Domain settings"** → **"Add custom domain"**
2. Introduza o domínio (`seudominio.com`)
3. Escolha um método DNS:

**Opção A: Usar Netlify DNS (mais fácil)**
- Clique em "Set up Netlify DNS"
- Netlify fornecerá 4 servidores de nomes (NS)
- No provedor de domínios (GoDaddy, Nomedrive, etc.), mude os NS para os que o Netlify indicou
- Propagação: 24-48 horas

**Opção B: Usar CNAME (se o provedor não permite mudar NS)**
- Netlify indicará um CNAME (ex: `seudominio.com-12345.netlify.app`)
- No provedor de domínios, crie um registo CNAME apontando para o CNAME do Netlify
- Propagação: 2-24 horas

### Passo 6: Ativar Netlify CMS (para cliente editar conteúdo)

1. No painel do site → **"Site settings"** → **"Identity"** → **"Enable Identity"**
2. Em **"Registration"** escolha:
   - `Invite only` (mais seguro) — convida clientes por e-mail
   - `Open` (qualquer um pode registar-se)
3. Vá a **"Services"** e ative **"Git Gateway"**
4. Autorize Netlify a usar GitHub (pode ser solicitado)

### Passo 7: Criar Utilizador para o Cliente

1. No painel do site → **"Identity"** → **"Invite users"**
2. Introduza o e-mail do cliente
3. Clique em **"Send invite"**
4. Cliente recebe e-mail com link de convite
5. Cliente clica no link e cria senha
6. Cliente acede a `https://seudominio.com/admin/` e faz login

### Passo 8: Enviar Instruções ao Cliente

Envie este template ao cliente:

```
Olá [Nome Cliente],

O seu site está pronto em: https://seudominio.com

Para editar o conteúdo (produtos, posts, imagens):
1. Aceda a: https://seudominio.com/admin/
2. Clique em "Sign in"
3. Use o e-mail e senha que recebeu por e-mail

Secções disponíveis:
- Posts: Criar/editar posts (blogue, notícias)
- Imagens: Upload de fotos para galeria

Qualquer dúvida, contacte: SEU_EMAIL

Abraços,
[Seu Nome]
```

---

## **OPÇÃO 2: GitHub Pages (Grátis, mas sem Netlify CMS)**

### Passo 1: Criar Repositório Público

1. Vá a https://github.com/new
2. Nome: `seudominio` (ou nome do projeto)
3. Deixe **Public** selecionado
4. Clique em **"Create repository"**

### Passo 2: Subir o Projeto

```powershell
cd 'c:\Users\figue\Desktop\index.html'
git init
git add .
git commit -m "Site inicial"
git branch -M main
git remote add origin https://github.com/SEU_USUARIO/seudominio.git
git push -u origin main
```

### Passo 3: Ativar GitHub Pages

1. No repositório GitHub → **Settings** → **Pages**
2. Em **"Branch"** escolha `main`
3. Em **"Folder"** escolha `/` (root)
4. Clique em **"Save"**
5. GitHub publicará em: `https://SEU_USUARIO.github.io/seudominio`

### Passo 4: Adicionar Domínio Personalizado

1. Em **Settings** → **Pages** → **"Custom domain"**
2. Introduza `seudominio.com`
3. No provedor de domínios, crie CNAME apontando para `SEU_USUARIO.github.io`
4. Marque a opção "Enforce HTTPS"

---

## **OPÇÃO 3: Servidor FTP/Hosting Tradicional**

Se já tem um servidor/hosting contratado:

### Passo 1: Obter Credenciais FTP

Contacte o seu provedor de hosting e peça:
- Servidor FTP (ex: `ftp.seuserver.com`)
- Utilizador FTP
- Palavra-passe
- Diretório de publicação (ex: `/public_html`)

### Passo 2: Transferir Ficheiros

**Opção A: Usar FileZilla (Grátis)**

1. Descarregue FileZilla em https://filezilla-project.org/
2. Abra FileZilla
3. Em **File** → **Site Manager** → **New site**
4. Preencha:
   - **Host**: `ftp.seuserver.com`
   - **Protocol**: FTP
   - **User**: (seu utilizador FTP)
   - **Password**: (sua palavra-passe)
5. Clique em **Connect**
6. À esquerda (local) navegue para `c:\Users\figue\Desktop\index.html`
7. À direita (servidor) navegue para `/public_html`
8. Selecione todos os ficheiros à esquerda e clique em **Upload**

**Opção B: Usar PowerShell (se o servidor suporta SFTP)**

```powershell
# Instalar módulo de SFTP (se não tiver)
Install-Module Posh-SSH -Force

# Conectar e enviar
$cred = New-Object System.Management.Automation.PSCredential ("usuario", (ConvertTo-SecureString "password" -AsPlainText -Force))
New-SFTPSession -ComputerName "sftp.seuserver.com" -Credential $cred
Set-SFTPLocation -SessionId 0 -Path "/public_html"
Send-SFTPItem -SessionId 0 -LocalFile "c:\Users\figue\Desktop\index.html\*" -Remote "."
```

### Passo 3: Verificar o Acesso

- Abra `https://seudominio.com` no navegador
- O site deve aparecer

---

## **Checklist Final Antes de Enviar ao Cliente**

- [ ] Site funciona em desktop e mobile (testar em `https://...`)
- [ ] Links navegam corretamente
- [ ] Botão WhatsApp abre com mensagem
- [ ] Imagens carregam corretamente
- [ ] Formulário de encomenda funciona
- [ ] Favicon aparece na aba
- [ ] Certificado SSL está ativo (HTTPS, cadeado verde)
- [ ] Cookies banner aparece (if applicable)
- [ ] Admin (`/admin/`) carrega (se usar Netlify CMS)
- [ ] Teste um post no CMS (criar, editar, eliminar)

---

## **Depois do Deploy: Manutenção**

### Atualizar o Site

Se precisar de atualizar algo:

1. Edite os ficheiros locais
2. Faça commit e push para GitHub:
   ```powershell
   git add .
   git commit -m "Descrição da atualização"
   git push
   ```
3. Netlify/GitHub Pages redeploy automaticamente (1-2 minutos)

### Cliente Editar Conteúdo

1. Acede a `https://seudominio.com/admin/`
2. Clica em "Sign in"
3. Edita Posts, Imagens, etc.
4. Clica "Publish" — a alteração fica direto no site

---

## **Suporte e Resolução de Problemas**

### "O site não carrega"
- Aguarde 5 minutos (propagação DNS)
- Limpe cache do navegador (Ctrl+Shift+Del)
- Confirme que o URL está correto

### "Admin (`/admin/`) não funciona"
- Certifique-se que `admin/config.yml` existe
- Verifique que Git Gateway está ativado (Netlify)
- Recarregue a página

### "Imagens não aparecem"
- Verifique os caminhos das imagens no HTML (devem ser relativos ou absolutos)
- Confirme que as imagens estão na pasta certa

### "Domínio personalizado não funciona"
- Aguarde propagação DNS (pode levar 48 horas)
- Verifique os registos DNS no provedor de domínios
- Contacte o suporte do Netlify/GitHub

---

## **Dúvidas? Contactos de Suporte**

- **Netlify**: https://support.netlify.com
- **GitHub Pages**: https://docs.github.com/en/pages
- **FileZilla**: https://wiki.filezilla-project.org/

---

**Criado em 4 de Dezembro de 2025**
