# SUAP Lite

> Um SUAP Lite totalmente vibe-coded 💀

Um protótipo experimental para consultar o boletim do IFPR: tela enxuta, tema escuro e foco no que importa — disciplinas, notas, frequência e aulas de hoje. **Totalmente criado por inteligência artificial.**

**Feito para aprender e testar, não para produção.** O projeto foi desenvolvido com apoio do **Manus** e do **Claude Code**, em um fluxo de prototipação rápida (*vibe coding*).

> Este projeto não é oficial, não é mantido pelo IFPR e não substitui o SUAP.

## O que tem

- Login usando a autenticação do SUAP.

- Resumo do aluno com nome, matrícula, curso, período de referência e quantidade de períodos.

- Seleção do período letivo e consulta de disciplinas.

- Detalhes de avaliações, notas, faltas e frequência por disciplina.

- Horários das aulas do dia atual.

- Aviso estimado sobre faltar hoje: considera quantos períodos estão marcados para cada disciplina, as aulas já cumpridas, a carga horária total, as faltas e a frequência disponível no boletim.

- Interface responsiva, minimalista e em tema escuro, com Geist e fontes de sistema como fallback.

- Cache local de boletins e horários já consultados para ajudar quando a conexão falhar.

## Como funciona o aviso de faltas

O protótipo projeta o efeito de faltar a **cada período listado para hoje**. Por exemplo, dois períodos da mesma disciplina contam como duas faltas na estimativa. Quando os dados estão disponíveis, a projeção combina as aulas já cumpridas e a frequência atual para estimar como a presença pode ficar após as aulas de hoje.

O limite de faltas é estimado como 25% da carga horária total, equivalente à referência de 75% de frequência mínima usada no aviso. A mensagem diferencia situações como estar abaixo de 75% agora, cair abaixo desse patamar se faltar hoje, ou permanecer dentro do limite estimado.

> A estimativa é apenas um auxílio: pode variar conforme a atualização e as regras aplicadas pelo SUAP/IFPR. Estar abaixo de 75% durante o período não significa, por si só, reprovação final automática — a frequência pode se recuperar com as aulas seguintes. Confira sempre seus registros e sua situação diretamente no SUAP e com a instituição. Se a API não fornecer dados suficientes, o protótipo informa que não consegue calcular com segurança.

## Como testar

O protótipo é uma página HTML sem etapa de build nem dependências JavaScript adicionais. Para testar localmente, coloque o HTML e este README na mesma pasta e sirva os arquivos com um servidor local:

```bash
python3 -m http.server 8000
```

Depois, abra [http://localhost:8000](http://localhost:8000) e entre com sua conta SUAP.

> O acesso direto via `file://` pode ser bloqueado pelo navegador. Mesmo usando servidor local, a consulta depende de conexão com o SUAP e das permissões de CORS da API.

## API utilizada

O cliente aponta para a API do SUAP do IFPR e consulta, entre outros, estes endpoints:

- `POST /api/token/pair` — autenticação.

- `POST /api/token/refresh` — renovação da sessão.

- `GET /api/rh/meus-dados/` — nome e matrícula.

- `GET /api/ensino/meus-dados-aluno/` — curso e dados acadêmicos.

- `GET /api/ensino/meus-periodos-letivos/` — períodos letivos disponíveis.

- `GET /api/ensino/disciplinas/{ano}.{período}/` — disciplinas e dados do boletim no período.

- `GET /api/ensino/disciplinas/{id}/etapas/` — avaliações de uma disciplina.

- `GET /api/ensino/diarios/{ano}.{período}/?page=1` — diários e horários das aulas; o protótipo percorre páginas adicionais quando a API informa que existem.

Os endpoints, formatos de resposta, autenticação ou regras de CORS podem mudar sem aviso; por isso, o funcionamento pode variar.

## Privacidade e limitações

- Use apenas em um dispositivo confiável. A sessão é mantida no navegador por cookies e armazenamento local para facilitar o uso.

- Ao sair, o protótipo remove os tokens e o cache local gerenciado por ele.

- Não compartilhe capturas de tela ou arquivos de cache que possam conter informações acadêmicas.

- Não inclua credenciais, tokens ou dados pessoais em issues, commits públicos ou mensagens.

- A senha é enviada ao endpoint de autenticação do SUAP; não há um servidor próprio intermediando as chamadas.

- O aviso de faltas depende dos dados retornados pelo SUAP e é uma estimativa; não altera registros de frequência nem determina oficialmente aprovação ou reprovação.

## Stack

- HTML, CSS e JavaScript sem framework.

- API do SUAP/IFPR.

## Status

Protótipo de teste em evolução. Use por sua conta e risco; para operações oficiais, consulte diretamente o SUAP.
