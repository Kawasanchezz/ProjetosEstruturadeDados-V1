# Política de Segurança

## Versões suportadas

Este é um trabalho acadêmico. Somente a versão mais recente da branch `main` recebe correções.

## Como reportar uma vulnerabilidade

Não abra uma issue pública para falhas de segurança.

Use o relato privado do GitHub: na aba **Security** do repositório, clique em **Report a vulnerability**.
Descreva o problema, os passos para reproduzi-lo e o impacto que você percebe.

Você deve receber uma resposta em alguns dias. Falhas confirmadas serão corrigidas na `main` e
registradas no histórico de commits.

## Modelo de segurança do projeto

O sistema foi feito para rodar **localmente**, em uma única máquina:

- O servidor escuta apenas em `127.0.0.1` e rejeita `Host`/`Origin` de fora
  (proteção contra CSRF e DNS rebinding).
- As respostas enviam CSP restritiva, `X-Content-Type-Options`, `X-Frame-Options` e `Referrer-Policy`.
- Há limite de 1000 alunos por campus, porque a árvore não é balanceada e as operações são recursivas.
- Os dados ficam só em memória, os alunos de exemplo são fictícios e não há banco de dados,
  secrets nem variáveis de ambiente.

### Fora do escopo

- Não há autenticação nem autorização. **Não exponha a porta do servidor na rede ou na internet.**
- Ataques que exigem acesso físico ou controle da máquina onde o servidor roda.

## Boas práticas para quem contribui

- Nunca faça commit de senhas, tokens, chaves ou arquivos `.env`. O `.gitignore` já bloqueia os formatos mais comuns.
- Não coloque dados reais de alunos no código ou nos exemplos.
