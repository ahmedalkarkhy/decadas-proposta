# Décadas · Como subir a landing e ligar ao domínio

## O que é este ficheiro

`decadas-landing.html` é a página completa numa só peça. Fontes, imagens, vídeo, estilos
e scripts estão todos embutidos, por isso funciona sozinha em qualquer sítio, sem
dependências externas.

Peso: cerca de 7 MB (o vídeo da obra, embutido, ocupa cerca de 6 MB). Ver a secção
"Otimização" no fim, importante antes de a pôr como homepage real.

## Onde a página está agora (só para mostrar)

Já está publicada para demonstração aqui:

    https://ahmedalkarkhy.github.io/decadas-proposta/

Isto serve apenas para mostrar aos sócios. Os passos abaixo são para a pôr no vosso
repositório e no vosso domínio.

---

## Opção A · Publicar num caminho, sem mexer no site atual (recomendado para já)

Risco zero. A página fica em `decadasrh.com/proposta`, o site atual não muda.

1. Copiar `decadas-landing.html` para a pasta `public/` do projeto, com o nome
   `proposta.html`:

       public/proposta.html

2. Commit e deploy (git push).
3. Fica disponível em:

       https://decadasrh.com/proposta.html

Nada da página atual é alterado. Bom para validar com a equipa antes de trocar a original.

---

## Opção B · Substituir a página principal (a original)

Quando quiserem que esta seja a homepage do domínio.

Contexto: o site é Next.js (App Router). A rota `/` é servida por `app/page.tsx`
(ou `app/(grupo)/page.tsx`). Um ficheiro em `public/` não substitui `/` sozinho, por isso
são dois passos.

1. Colocar o ficheiro em `public/proposta.html` (igual à Opção A).

2. Desligar a homepage atual: renomear o ficheiro da rota `/`
   (ex.: `app/page.tsx` para `app/page.tsx.bak`) ou apagar.
   Guardem o original para poderem voltar atrás.

3. Reencaminhar `/` para o ficheiro, no `next.config.js`:

       module.exports = {
         async rewrites() {
           return [{ source: '/', destination: '/proposta.html' }]
         },
       }

   Se já tiverem um bloco `rewrites`, acrescentem só a linha à lista existente.

4. Commit e deploy. `decadasrh.com` passa a mostrar a nova página.

Voltar atrás: repor o `app/page.tsx` original e remover o rewrite.

---

## Domínio

O domínio `decadasrh.com` já está ligado ao vosso deploy (o site já corre lá). Não é
preciso mexer em DNS. Basta o deploy do repositório. Se o host for Vercel ou Netlify,
o `git push` faz o deploy automático.

---

## Formulário "Marcar reunião"

Neste ficheiro, ao submeter, o formulário abre o email do visitante já preenchido para
`adm@decadasrh.com` e mostra a mensagem de confirmação. Não tem back-end. Quando quiserem
que os pedidos entrem direto no vosso sistema (base de dados ou CRM), digam-me e ligo o
formulário a um endpoint vosso.

---

## Otimização (importante para produção)

O vídeo embutido torna a página pesada (cerca de 6 MB só de vídeo). Para a homepage real,
o melhor é NÃO embutir o vídeo:

- Opção 1: usar o player Wistia que já têm (o vídeo "video obras", id `783ilv9itv`).
  No vosso próprio domínio não existe a restrição que obrigou a embutir no artifact.
- Opção 2: pôr o mp4 como ficheiro em `public/` e referenciar por URL.

Qualquer uma baixa a página para menos de 1 MB. Se quiserem, eu entrego já a versão de
produção assim (HTML leve + o mp4 à parte, ou com o embed Wistia).

---

## Resumo rápido

- Mostrar já aos sócios: `https://ahmedalkarkhy.github.io/decadas-proposta/`
- Pôr no domínio sem risco: Opção A, em `/proposta.html`.
- Trocar a página principal: Opção B, rewrite mais desligar a homepage atual.
- Antes de ser a homepage definitiva: pedir a versão leve (sem vídeo embutido).
