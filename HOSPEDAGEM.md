# Guia de Hospedagem Gratuita do StashKeeper Pro

Este guia explica como hospedar o StashKeeper Pro gratuitamente enquanto mantém a integração com o Supabase.

## Pré-requisitos

- Conta no GitHub (para hospedar o código)
- Conta no Vercel, Netlify ou similar (para hospedagem gratuita)
- Projeto Supabase já configurado (conforme o SETUP.md)

## Passo 1: Preparar o Projeto para Implantação

1. Certifique-se de que seu projeto está funcionando localmente com o Supabase
2. Verifique se o arquivo `.env` contém as variáveis necessárias:
   ```
   VITE_SUPABASE_URL=sua_url_do_supabase
   VITE_SUPABASE_ANON_KEY=sua_chave_anon_do_supabase
   ```
3. Crie um arquivo `.env.example` com o mesmo formato, mas sem os valores reais:
   ```
   VITE_SUPABASE_URL=
   VITE_SUPABASE_ANON_KEY=
   ```
4. Certifique-se de que o arquivo `.gitignore` inclui o arquivo `.env` para não expor suas chaves

## Passo 2: Hospedar no Vercel (Opção Recomendada)

1. Crie uma conta no [Vercel](https://vercel.com) se ainda não tiver uma
2. Faça login e clique em "New Project"
3. Importe seu repositório do GitHub (você precisará fazer o push do projeto para o GitHub primeiro)
4. Na configuração do projeto:
   - Framework Preset: Selecione "Vite"
   - Build Command: `npm run build` (já configurado no package.json)
   - Output Directory: `dist` (padrão do Vite)
5. Expanda a seção "Environment Variables" e adicione:
   - `VITE_SUPABASE_URL`: Cole sua URL do Supabase
   - `VITE_SUPABASE_ANON_KEY`: Cole sua chave anônima do Supabase
6. Clique em "Deploy"

## Passo 3: Hospedar no Netlify (Alternativa)

1. Crie uma conta no [Netlify](https://netlify.com) se ainda não tiver uma
2. Faça login e clique em "New site from Git"
3. Escolha GitHub como provedor e selecione seu repositório
4. Na configuração do projeto:
   - Build Command: `npm run build`
   - Publish Directory: `dist`
5. Clique em "Show advanced" e adicione as variáveis de ambiente:
   - `VITE_SUPABASE_URL`: Cole sua URL do Supabase
   - `VITE_SUPABASE_ANON_KEY`: Cole sua chave anônima do Supabase
6. Clique em "Deploy site"

## Passo 4: Configurar Domínio Personalizado (Opcional)

### No Vercel:
1. Vá para o painel do seu projeto
2. Clique na aba "Domains"
3. Adicione seu domínio personalizado e siga as instruções para configurar os registros DNS

### No Netlify:
1. Vá para o painel do seu site
2. Clique na aba "Domain settings"
3. Clique em "Add custom domain" e siga as instruções

## Passo 5: Verificar a Implantação

1. Acesse a URL fornecida pelo Vercel ou Netlify
2. Verifique se o login com o Supabase está funcionando corretamente
3. Teste todas as funcionalidades que dependem do Supabase

## Solução de Problemas

### Erro de CORS

Se encontrar erros de CORS:

1. No painel do Supabase, vá para "Authentication" > "URL Configuration"
2. Adicione a URL do seu site implantado (ex: `https://seu-app.vercel.app`) à lista de URLs permitidas

### Erro de Conexão com o Supabase

1. Verifique se as variáveis de ambiente foram configuradas corretamente
2. Confirme se as chaves do Supabase estão corretas e não expiraram
3. Verifique se o projeto do Supabase está ativo

### Problemas com Funções Edge do Supabase

Se estiver usando funções Edge do Supabase:

1. Certifique-se de que as funções foram implantadas corretamente
2. Verifique se as variáveis de ambiente das funções estão configuradas

## Considerações de Segurança

- Nunca exponha sua chave de serviço (service_role) do Supabase no frontend
- Use apenas a chave anônima (anon) para operações do cliente
- Implemente regras de segurança adequadas no Supabase (RLS - Row Level Security)

## Limites do Plano Gratuito

### Vercel/Netlify (Plano Hobby/Free)
- Implantações ilimitadas
- Largura de banda limitada (geralmente suficiente para projetos pequenos)
- Sem domínios personalizados no Vercel Free (disponível no Netlify Free)

### Supabase (Plano Free)
- Até 500MB de armazenamento de banco de dados
- Até 2GB de transferência de dados por mês
- Até 50MB de armazenamento de arquivos
- Até 1GB de transferência de arquivos por mês

Monitore o uso para evitar surpresas com cobranças caso ultrapasse os limites gratuitos.