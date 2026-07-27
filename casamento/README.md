# Painel de Casamento

App de planejamento de casamento (checklist, orçamento, convidados, fornecedores, cortejo, roteiro e dia da noiva), pronto para ser acessado por qualquer pessoa pelo celular.

## Como acessar

Depois que este projeto estiver publicado no GitHub Pages, o link será algo como:

```
https://<usuario>.github.io/<repositorio>/casamento/
```

Abra esse link no celular e, se quiser, use "Adicionar à tela inicial" (Android/Chrome) ou "Adicionar à Tela de Início" (iPhone/Safari) para que ele funcione como um app de verdade, com ícone próprio.

## Armazenamento dos dados

Por padrão, o app salva os dados **no navegador de cada aparelho** (localStorage). Ou seja, se a noiva abrir no celular dela e o noivo abrir no dele, cada um vê e edita sua própria cópia — os dados não se misturam automaticamente.

Um banner no topo do app avisa qual modo está ativo.

### Ativar sincronização entre celulares (opcional)

Para que **todo mundo que abrir o link veja e edite os mesmos dados em tempo real**, é preciso ativar a sincronização com o Firebase Realtime Database (gratuito, sem cartão de crédito). Passo a passo:

1. Acesse https://console.firebase.google.com e crie um projeto novo (qualquer nome).
2. No menu lateral, vá em **Build > Realtime Database** e clique em **Criar banco de dados**. Escolha qualquer região e comece em **modo de teste**.
3. Depois de criado, vá na aba **Regras** e substitua pelo conteúdo abaixo (isso libera leitura/escrita para qualquer pessoa com o link, que é a ideia do painel compartilhado):
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
4. Volte para a visão geral do projeto (ícone de engrenagem > Configurações do projeto) e, na seção **Seus apps**, clique no ícone `</>` para registrar um app da Web. Copie o objeto `firebaseConfig` gerado.
5. Abra o arquivo `casamento/index.html` deste repositório e localize o bloco:
   ```js
   const firebaseConfig = {
     apiKey: "",
     authDomain: "",
     databaseURL: "",
     projectId: ""
   };
   ```
   Cole os valores correspondentes do seu projeto (apiKey, authDomain, databaseURL, projectId).
6. Salve, faça commit e publique novamente. O banner do app vai passar a mostrar "Sincronização ativa".

**Atenção:** como as regras acima liberam leitura/escrita para qualquer pessoa com o link (sem login), não compartilhe o link publicamente além de quem deve poder editar o painel — assim como já era a proposta original do painel ("qualquer pessoa com o link pode ver e editar").

## Estrutura

- `index.html` — o app completo (HTML + CSS + JS em um único arquivo)
- `manifest.json` — manifesto PWA (permite instalar na tela inicial)
- `icon-192.png`, `icon-512.png` — ícones do app
