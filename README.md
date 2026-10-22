# 🌳 Cadastro de Alunos por Campus

Sistema em Java que cadastra alunos em **7 campi**, cada um com a sua própria **Árvore Binária de Busca (ABB)**, com interface web e servidor HTTP embutido. Sem dependências externas.

![Java](https://img.shields.io/badge/Java-17%2B-ED8B00?logo=openjdk&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)
![Licença](https://img.shields.io/badge/licen%C3%A7a-MIT-blue)

*Trabalho de Estrutura de Dados — Universidade Cruzeiro do Sul · Ciência da Computação*

---

## 📖 Sobre

A árvore foi implementada com nós e ponteiros, **sem `TreeMap`, `TreeSet` ou `Collections.sort`**.

Regra principal: um aluno não pode estar matriculado em dois campi. Antes de inserir, o nome é procurado nas 7 árvores.

A comparação de nomes ignora acentos, maiúsculas e espaços repetidos: `José da Silva` = `JOSE DA SILVA`.

**Campi:** Anália Franco · Guarulhos · Liberdade · Paulista · São Miguel · Santo Amaro · Villa Lobos

## ✨ Funcionalidades

| Tela | O que faz |
|------|-----------|
| ➕ **Cadastrar** | Insere o aluno na árvore do campus, recusando nomes já existentes em qualquer campus |
| 🔍 **Localizar** | Percorre as árvores dos campi e para no primeiro resultado |
| 📋 **Listar** | Mostra os alunos em ordem alfabética (percurso em ordem) e desenha a árvore, com zoom e arraste |
| 🗑️ **Excluir** | Remove o aluno tratando os 3 casos: folha, um filho e dois filhos (sucessor em ordem), com confirmação antes |

A interface é responsiva e funciona em desktop e celular.

## ⏱️ Complexidade

| Operação | Caso médio | Pior caso |
|----------|-----------|-----------|
| Inserir / Buscar / Remover | O(log n) | O(n) |
| Percurso em ordem | O(n) | O(n) |

O pior caso acontece quando os nomes chegam em ordem alfabética e a árvore vira uma lista.

## 🚀 Como executar

Requer **JDK 17 ou superior**. Na pasta do projeto:

**PowerShell (Windows)**

```powershell
javac -encoding UTF-8 -d target/classes (Get-ChildItem -Recurse src -Filter *.java).FullName
java -cp target/classes unicsul.Principal
```

**Bash (Linux/macOS/Git Bash)**

```bash
javac -encoding UTF-8 -d target/classes $(find src -name '*.java')
java -cp target/classes unicsul.Principal
```

O navegador abre em **http://localhost:8080** (se a porta estiver ocupada, tenta 8081, 8082...).

- `--sem-navegador`: não abre o navegador automaticamente.
- Execute com a **pasta do projeto como diretório atual**: o servidor procura a pasta `webapp` a partir dele.

## 🧪 Testes

```bash
java -cp target/classes unicsul.testes.TesteArvore
```

Os testes cobrem a árvore (inserção, busca, remoção, altura) e as regras do sistema, sem JUnit.

## 🗂️ Estrutura

```text
src/main/java/unicsul/
├── Principal.java          # ponto de entrada e dados de exemplo
├── arvore/                 # ArvoreBinariaBusca e No
├── campus/                 # Campus (enum) e SistemaDeCampi (regras)
├── web/ServidorWeb.java    # servidor HTTP e API
├── testes/TesteArvore.java # testes
└── webapp/                 # index.html, css/, js/, imagens/
```

## 🔌 API

| Método | Rota | Parâmetros |
|--------|------|------------|
| `GET` | `/api/campi` | — |
| `POST` | `/api/cadastrar` | `nome`, `campus` |
| `GET` | `/api/buscar` | `nome` |
| `GET` | `/api/listar` | `campus` |
| `DELETE` | `/api/excluir` | `nome` |

## 🔐 Segurança

- Escuta apenas em `127.0.0.1` e rejeita `Host`/`Origin` de fora (proteção contra CSRF e DNS rebinding).
- Cabeçalhos: CSP restritiva, `X-Content-Type-Options`, `X-Frame-Options` e `Referrer-Policy`.
- Limite de 1000 alunos por campus, pois a árvore não é balanceada e as operações são recursivas.
- Não há login: **não exponha a porta na rede**.
- Dados só em memória, alunos de exemplo fictícios, sem secrets, banco de dados ou variáveis de ambiente.
- Para reportar uma falha, veja a [política de segurança](SECURITY.md).

## 📄 Licença

Distribuído sob a licença MIT. Veja o arquivo [LICENSE](LICENSE).
