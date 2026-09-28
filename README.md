# SUAP Lite

> Um SUAP Lite totalmente vibe-coded 💀

Um protótipo experimental de consulta ao boletim do IFPR: tela enxuta, tema escuro e foco no que importa — disciplinas, notas e frequência. **Totalmente criado por inteligência artifical.**

**Feito para aprender e testar, não para produção.** O projeto foi desenvolvido com apoio do **Manus** e do **Claude Code**, em um fluxo de prototipação rápida (*vibe coding*).

> Este projeto não é oficial, não é mantido pelo IFPR e não substitui o SUAP.

## O que tem

- Login usando a autenticação do SUAP.

- Resumo do aluno com nome, matrícula, curso, período de referência e quantidade de períodos.

- Seleção do período letivo e consulta de disciplinas.

- Detalhes de avaliações, notas, faltas e frequência por disciplina.

- Interface responsiva, minimalista e em tema escuro, com Geist e fontes de sistema como fallback.

- Cache local de boletins já consultados para ajudar quando a conexão falhar.

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

- `GET /api/ensino/disciplinas/{ano}.{período}/` — disciplinas do período.

- `GET /api/ensino/disciplinas/{id}/etapas/` — avaliações de uma disciplina.

Os endpoints, formatos de resposta, autenticação ou regras de CORS podem mudar sem aviso; por isso, o funcionamento pode variar.

## Privacidade e limitações

- Use apenas em um dispositivo confiável. A sessão é mantida no navegador por cookies e armazenamento local para facilitar o uso.

- Ao sair, o protótipo remove os tokens e o cache local gerenciado por ele.

- Não compartilhe capturas de tela ou arquivos de cache que possam conter informações acadêmicas.

- Não inclua credenciais, tokens ou dados pessoais em issues, commits públicos ou mensagens.

- A senha é enviada ao endpoint de autenticação do SUAP; não há um servidor próprio intermediando as chamadas.

## Stack

- HTML, CSS e JavaScript sem framework.

- API do SUAP/IFPR.

## Status

Protótipo de teste em evolução. Use por sua conta e risco; para operações oficiais, consulte diretamente o SUAP.
