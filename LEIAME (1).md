# Painel de Cancelamentos — Grupo Aspekto

## 1. Conectar sua planilha real

1. Abra a planilha do Google Sheets ligada ao seu Forms.
2. Vá em **Arquivo → Compartilhar → Publicar na Web**.
3. Em "Link", escolha a aba com as respostas (ex: "Respostas ao formulário 1") e o formato **CSV**.
4. Clique em **Publicar** e copie o link gerado.
5. Abra o arquivo `index.html`, encontre a linha:
   ```
   const SHEET_CSV_URL = "COLE_AQUI_O_LINK_CSV_PUBLICADO";
   ```
   e cole o link entre as aspas.
6. Salve o arquivo.

Sem esse link configurado, o painel funciona normalmente com dados de exemplo (aparece um aviso amarelo no topo avisando disso).

## 2. Testar localmente

Basta abrir o arquivo `index.html` duas vezes clicando nele — funciona em qualquer navegador, sem precisar instalar nada.

## 3. Publicar no Netlify (mais simples)

1. Acesse [app.netlify.com](https://app.netlify.com) e crie uma conta gratuita.
2. Na tela inicial, arraste a pasta inteira deste projeto para a área "Deploy manually".
3. Pronto — o Netlify gera um link público (algo como `nome-aleatorio.netlify.app`).
4. Toda vez que você quiser atualizar o site (por exemplo, se eu enviar uma nova versão do arquivo), é só arrastar a pasta de novo.

## 4. Publicar no GitHub Pages (alternativa)

1. Crie um repositório novo no GitHub e envie os arquivos desta pasta para ele.
2. Vá em **Settings → Pages**.
3. Em "Source", selecione a branch `main` e a pasta raiz (`/`).
4. Salve — o GitHub gera um link público em alguns minutos (formato `seuusuario.github.io/nome-do-repositorio`).

## Como o painel funciona no dia a dia

- Ele busca os dados da planilha automaticamente sempre que a página é aberta ou recarregada (F5).
- Não é "tempo real" — é "sempre que alguém abrir a página, os dados estarão atualizados".
- O campo **"Fechamentos do mês"** não vem da planilha (isso não é registrado no Forms). Você digita esse número manualmente no próprio painel — ele fica salvo no navegador de quem preencheu.
- Como o link do CSV publicado é público, qualquer pessoa com o link consegue ver os dados brutos da planilha. Se isso for sensível, evite compartilhar o link do CSV, apenas o link do painel publicado.

## Cálculos que o painel assume

- **Valor reembolsado** = Valor contratado − Valor da multa, somado apenas para solicitações com Status = "Finalizado".
- **Multa retida** = soma da coluna "Valor da multa", também apenas para Status = "Finalizado" (solicitações em outros status ainda não geraram um valor financeiro definitivo).
- **Tempo médio de resolução** = média de dias entre "Data da solicitação" e "Data do fechamento".

Se algum desses critérios não fizer sentido pro seu processo, é só avisar que eu ajusto a lógica.
