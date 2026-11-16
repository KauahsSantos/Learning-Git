****

# O que é o Git

 Em geral, git é um SVC, um Sistema de Controle de Versão. Ele nos ajuda com as versão do nosso sistema, ou projeto. Resumindo é como se o git fosse capaz de salvar vários arquivos do nosso projeto sem que esses arquivos fiquem guardados em uma pasta chamada  -  ``Versões do meus sistema.zip`` 
# As três áreas locais do Git

O Git trabalha principalmente com três áreas:

1. **Working Directory (diretório de trabalho):** onde você cria,  
    modifica e exclui arquivos.
2. **Staging Area (área de preparação):** onde você seleciona as  
    alterações que deseja incluir no próximo commit.
3. **Local Repository (repositório local):** onde os commits ficam  
    registrados no histórico do Git.

O repositório remoto, como o GitHub, é o local para o qual você pode  
enviar e de onde pode receber commits.

Fluxo simplificado:

```
Working Directory
       |
       | git add
       v
Staging Area
       |
       | git commit
       v
Local Repository
       |
       | git push / git pull
       v
Remote Repository
```

# 2. GitHub

**GitHub** é uma plataforma de hospedagem de repositórios Git e  
colaboração no desenvolvimento de software.

A diferença fundamental:

---

Git GitHub

---

Sistema de controle de versão Plataforma de hospedagem e  
colaboração

Funciona localmente Funciona principalmente online

Gerencia commits e branches Hospeda repositórios e facilita PRs

Controla o histórico Facilita o trabalho em equipe

## Não depende do GitHub Utiliza Git para versionamento

### Principais recursos do GitHub

- **Repository:** local onde o projeto fica hospedado.
- **Branch:** ramificação independente do projeto.
- **Commit:** registro de alterações.
- **Issue:** registro de tarefas, problemas e melhorias.
- **Pull Request (PR):** solicitação para integrar alterações de uma  
    branch em outra.
- **Merge:** integração das alterações de uma branch em outra.
- **Actions:** automação de processos, como testes e deploy.
- **README:** documentação inicial do projeto.

### Exemplo prático

Imagine que exista a Issue `#15 — Implementar tela de cadastro`.

Você pode criar uma branch chamada `feature/cadastro-usuario`,  
desenvolver a funcionalidade, realizar commits e enviar uma Pull Request  
para a branch principal.

Esse é um fluxo bastante utilizado em equipes de desenvolvimento.

## 3. Comandos básicos do Git

### 3.1. `git add`

O comando `git add` adiciona alterações à **Staging Area**. Ele  
seleciona quais modificações serão incluídas no próximo commit.

#### `git add .`

```
git add .
```

Adiciona as alterações do diretório atual e de seus subdiretórios à  
Staging Area.

Por exemplo, se você estiver na raiz do projeto, o comando adicionará as  
alterações encontradas em diretórios como `lib/`, `assets/` e nos  
arquivos da raiz.

#### `git add ./`

```
git add ./
```

É outra maneira de indicar o diretório atual. Nesse contexto, tem  
essencialmente o mesmo efeito de `git add .`.

#### `git add` por caminho (_path_)

Você também pode adicionar arquivos ou diretórios específicos:

```
# Adiciona somente um arquivo
git add ./lib/main.dart

# Adiciona as alterações dentro de um diretório
git add ./lib/

# Adiciona somente uma imagem
git add ./assets/logo.png
```

**Recomendação:** use `git add` por caminho quando quiser controlar  
precisamente o que entrará em cada commit. Use `git add .` quando tiver  
revisado todas as alterações e quiser adicionar tudo do diretório atual  
para baixo.

### 3.2. `git commit`

O comando `git commit` registra no histórico as alterações que estão na  
Staging Area.

```
git commit -m "mensagem do commit"
```

Exemplo:

```
git commit -m "feat: implementa tela de login"
```

O parâmetro `-m` significa _message_ (mensagem).

Uma mensagem de commit deve explicar resumidamente o que foi realizado.

#### Conventional Commits

**Conventional Commits** é uma convenção para padronizar mensagens de  
commits.

Prefixo Significado

---

`feat` Nova funcionalidade  
`fix` Correção de erro  
`docs` Documentação  
`style` Formatação sem alteração de lógica  
`refactor` Refatoração  
`test` Testes  
`chore` Tarefas de manutenção  
`perf` Melhoria de desempenho

Estrutura:

```
tipo(escopo): descrição
```

Exemplos:

```
git commit -m "feat(auth): adiciona autenticação"
git commit -m "fix(login): corrige validação de email"
git commit -m "docs: atualiza README"
git commit -m "refactor: reorganiza camada de serviços"
```

### 3.3. `git push`

O comando `git push` envia commits locais para um repositório remoto.

```
git push
```

Esse comando envia os commits da branch atual para a branch remota  
configurada.

#### `git push -u origin {nome-da-branch}`

```
git push -u origin feature/login
```

Elemento Significado

---

`git push` Envia os commits  
`-u` Configura o _upstream_  
`origin` Nome do repositório remoto  
`feature/login` Nome da branch

O parâmetro `-u` é uma abreviação de `--set-upstream`. Ele configura  
qual branch remota corresponde à branch local.

Depois dessa configuração inicial, normalmente basta executar:

```
git push
```

#### O que é upstream?

É a referência que associa uma branch local à sua branch remota  
correspondente. Essa configuração permite que comandos como `git push` e  
`git pull` saibam de qual branch remota enviar ou receber alterações.

### 3.4. `git pull`

O comando `git pull` busca atualizações do repositório remoto e tenta  
integrá-las à branch local atual.

```
git pull
```

Também é possível especificar o remoto e a branch:

```
git pull origin main
```

De maneira simplificada, o comportamento padrão é:

```
git pull = git fetch + git merge
```

O comportamento pode variar conforme a configuração de pull; por  
exemplo, ele também pode utilizar _rebase_.

### 3.5. `git fetch`

O comando `git fetch` busca atualizações do repositório remoto sem  
integrá-las automaticamente à branch local atual.

```
git fetch
```

Ou, especificando o remoto:

```
git fetch origin
```

O Git atualiza as referências remotas, mas não modifica automaticamente  
os arquivos da sua branch atual.

Depois, você pode analisar as diferenças:

```
git diff main origin/main
```

#### Diferença entre `pull` e `fetch`

---

`git fetch` `git pull`

---

Busca atualizações Busca atualizações

Não integra automaticamente à Busca e tenta integrar as  
branch atual alterações

Permite analisar antes de integrar É mais direto

## Dá mais controle sobre o momento da Atualiza a branch local conforme a  
integração configuração

**Recomendação:** utilize `git fetch` antes de integrar alterações  
importantes, principalmente em projetos com várias pessoas e branches.

### 3.6. `git remote add origin`

A sintaxe correta é:

```
git remote add origin URL_DO_REPOSITORIO
```

Esse comando adiciona um repositório remoto ao projeto local.

Exemplo:

```
git remote add origin https://github.com/usuario/mony.git
```

Elemento Significado

---

`git remote` Gerencia repositórios remotos  
`add` Adiciona um novo remoto  
`origin` Nome dado ao remoto  
URL Endereço do repositório

O nome `origin` é uma convenção, não uma obrigação.

Para verificar os repositórios remotos:

```
git remote -v
```

Exemplo de resultado:

```
origin  https://github.com/usuario/mony.git (fetch)
origin  https://github.com/usuario/mony.git (push)
```

### 3.7. `git show`

O comando `git show` exibe informações sobre um objeto do Git,  
normalmente um commit.

```
git show
```

Por padrão, mostra detalhes do commit mais recente, incluindo:

- Identificador do commit.
- Autor.
- Data.
- Mensagem.
- Alterações realizadas.

Para consultar um commit específico:

```
git show HASH_DO_COMMIT
```

Exemplo:

```
git show a82f41c
```

É útil para investigar o que foi alterado em determinado momento do  
projeto.

### 3.8. `git log --oneline`

A opção correta é `--oneline`, e não `--online`.

```
git log --oneline
```

Apresenta o histórico de commits em formato resumido.

Exemplo:

```
a82f41c feat: adiciona tela de login
c91e25a fix: corrige validação de email
b21d9a3 docs: atualiza README
```

Outros formatos úteis:

```
# Histórico completo
git log

# Histórico resumido com representação gráfica de todas as branches
git log --oneline --graph --all

# Histórico com autor, data e mensagem
git log --pretty=format:"%h - %an - %ad - %s"
```

O comando `git log --oneline --graph --all` é especialmente útil para  
visualizar o histórico de diferentes branches.

### 3.9. `git diff`

O comando `git diff` compara alterações entre arquivos e versões.

```
git diff
```

Por padrão, mostra alterações ainda não adicionadas à Staging Area.

Variações importantes:

---

Comando Função

---

`git diff` Mostra alterações não staged em  
relação à Staging Area

`git diff --staged` Mostra alterações staged em relação  
ao último commit

`git diff HEAD` Compara o diretório de trabalho com  
o último commit

## `git diff main origin/main` Compara duas referências

O `git diff` permite revisar suas alterações antes de realizar um  
commit.

### 3.10. `git restore --staged`

Esse comando remove arquivos da Staging Area sem apagar suas  
modificações locais.

```
git restore --staged nome_do_arquivo
```

Exemplo:

```
git add .
git restore --staged lib/main.dart
```

O arquivo será retirado da Staging Area, mas suas alterações continuarão  
no computador.

**Atenção:** não confunda os dois comandos:

---

Comando Resultado

---

`git restore --staged arquivo` Retira o arquivo da Staging Area,  
preservando as alterações no  
diretório de trabalho

## `git restore arquivo` Descarta alterações locais não  
staged do arquivo

Tenha cuidado com `git restore arquivo`: ele pode descartar alterações  
locais que ainda não foram salvas em um commit.

## 4. Git Branch

Uma **branch** é uma ramificação que permite desenvolver funcionalidades  
sem modificar diretamente a linha principal do projeto.

Exemplo:

```
main
 |
 +-- feature/login
 |
 +-- feature/cadastro
 |
 +-- fix/validacao-email
```

Você pode desenvolver funcionalidades diferentes sem misturar  
imediatamente suas alterações.

### Por que utilizar branches?

Imagine que você esteja desenvolvendo a Mony e precise implementar uma  
tela de cadastro. Em vez de modificar diretamente a `main`, você cria  
uma branch específica para essa funcionalidade.

Depois de terminar, pode abrir uma Pull Request e solicitar a integração  
das alterações na `main`.

### 4.1. `git branch -c main {nome-da-branch}`

A opção `-c` significa `--copy`: copia uma branch existente para uma  
nova branch.

Exemplo:

```
git branch -c main feature/login
```

Isso cria uma cópia da branch `main` com o nome `feature/login`.

Para criar uma branch nova de trabalho, normalmente não é necessário  
copiar a branch. Você pode utilizar:

```
git branch feature/login
```

Esse comando cria a branch, mas não muda para ela.

Ou:

```
git switch -c feature/login
```

Esse comando cria a branch e já muda para ela.

#### Diferença entre `-c` e `-m`

Opção Função

---

`git branch -c` Copia uma branch  
`git branch -m` Renomeia uma branch

Exemplo de renomeação:

```
git branch -m feature/login feature/auth
```

### 4.2. `git branch -l`

```
git branch -l
```

Lista as branches locais do repositório.

Exemplo:

```
* main
  feature/login
  feature/cadastro
  fix/validacao
```

O asterisco (`*`) indica a branch em que você está trabalhando  
atualmente.

### 4.3. `git branch -la`

```
git branch -la
```

Lista branches locais e referências de branches remotas. É equivalente  
a:

```
git branch -a
```

Exemplo:

```
* main
  feature/login
  remotes/origin/main
  remotes/origin/feature/login
```

### 4.4. `git branch -lav`

```
git branch -lav
```

Também é possível utilizar:

```
git branch -av
```

Lista branches locais e remotas com informações adicionais, como o  
último commit associado a cada uma.

#### Resumo das opções

---

Comando Resultado

---

`git branch -l` Lista branches locais

`git branch -la` Lista branches locais e remotas

## `git branch -lav` Lista branches locais e remotas com  
informações adicionais

> Observação: `-l`, `-a` e `-v` são opções combináveis. `-a` inclui  
> referências remotas e `-v` mostra o último commit de cada branch.

## 5. Git Checkout

O `git checkout` é um comando utilizado para mudar de branch e também  
pode recuperar versões de arquivos.

Atualmente, o Git disponibiliza comandos mais específicos, como  
`git switch` e `git restore`. Mesmo assim, é importante conhecer o  
`checkout`, pois ele ainda aparece em muitos projetos e tutoriais.

### 5.1. `git checkout {nome-da-branch}`

Utilizado para mudar de uma branch para outra.

```
git checkout main
```

Outro exemplo:

```
git checkout feature/login
```

### 5.2. `git checkout -b {nome-da-branch}`

Cria uma nova branch e muda automaticamente para ela.

```
git checkout -b feature/cadastro
```

O comando equivale a:

```
git branch feature/cadastro
git checkout feature/cadastro
```

### Checkout versus Switch

Checkout Switch

---

`git checkout main` `git switch main`  
`git checkout -b feature/login` `git switch -c feature/login`

O `switch` é mais específico para operações com branches, enquanto o  
`checkout` possui outras funcionalidades.

## 6. Fluxo de trabalho profissional com Git e GitHub

Imagine que você recebeu a Issue:

`#15 — Implementar tela de cadastro de usuários`

O objetivo é resolver essa Issue utilizando branches, commits e Pull  
Requests.

### Etapa 1 --- Atualizar o projeto

```
git switch main
git pull origin main
```

Atualiza sua branch principal com as alterações remotas.

### Etapa 2 --- Criar uma branch

```
git switch -c feature/cadastro-usuario
```

Cria uma ramificação para resolver a Issue.

### Etapa 3 --- Desenvolver a funcionalidade

Modifique os arquivos necessários no projeto.

### Etapa 4 --- Verificar as alterações

```
git status
git diff
```

Confira quais arquivos foram modificados e revise as diferenças.

### Etapa 5 --- Adicionar os arquivos

```
git add .
```

Adiciona as alterações à Staging Area. Se necessário, adicione somente  
os caminhos desejados.

### Etapa 6 --- Criar o commit

```
git commit -m "feat: implementa cadastro de usuarios"
```

Registra as alterações no histórico.

### Etapa 7 --- Enviar para o GitHub

```
git push -u origin feature/cadastro-usuario
```

Publica a branch remota e configura o upstream.

### Etapa 8 --- Criar uma Pull Request

No GitHub, abra uma PR da `feature/cadastro-usuario` para `main`.

Na descrição, você pode utilizar:

```
Closes #15
```

Isso permite fechar automaticamente a Issue quando a PR for integrada à  
branch padrão do repositório.

### Etapa 9 --- Integrar as alterações

Após a revisão e aprovação, a PR poderá ser integrada à `main`.

## 7. Resumo dos comandos para consulta

Comando Função

---

`git add .` Adiciona alterações do diretório atual e subdiretórios  
`git add ./path` Adiciona alterações de um caminho específico  
`git commit -m ""` Registra um commit  
`git push` Envia commits ao remoto  
`git push -u origin branch` Envia e configura o upstream  
`git pull` Busca e integra alterações conforme a configuração  
`git fetch` Busca alterações sem integrá-las à branch atual  
`git remote add origin URL` Adiciona um remoto  
`git remote -v` Lista os remotos  
`git show` Exibe detalhes de um objeto, normalmente um commit  
`git log --oneline` Exibe histórico resumido  
`git diff` Exibe diferenças não staged  
`git restore --staged arquivo` Retira arquivo da Staging Area  
`git branch` Lista branches locais  
`git branch nome` Cria uma branch  
`git branch -c origem destino` Copia uma branch  
`git branch -l` Lista branches locais  
`git branch -a` Lista branches locais e remotas  
`git branch -av` Lista branches com informações adicionais  
`git checkout branch` Muda de branch  
`git checkout -b branch` Cria e muda de branch  
`git switch branch` Muda de branch  
`git switch -c branch` Cria e muda de branch

## 8. Exercícios práticos

Pratique os conceitos em um repositório de testes, sem utilizar  
diretamente a `main` de um projeto importante.

### Exercício 1 --- Inicialização e versionamento

- [ ] Crie uma pasta chamada `git-estudos`.
- [ ] Inicialize um repositório Git.
- [ ] Crie um arquivo `README.md`.
- [ ] Adicione o arquivo à Staging Area.
- [ ] Realize seu primeiro commit.

### Exercício 2 --- Branches

- [ ] Crie uma branch chamada `feature/teste`.
- [ ] Crie um arquivo `teste.txt`.
- [ ] Realize um commit nessa branch.
- [ ] Volte para a `main`.
- [ ] Confira se o arquivo está presente na `main`.

### Exercício 3 --- Histórico e diferenças

- [ ] Modifique o `README.md`.
- [ ] Execute `git diff`.
- [ ] Adicione as alterações com `git add`.
- [ ] Execute `git diff --staged`.
- [ ] Realize um commit e consulte `git log --oneline`.

### Exercício 4 --- Repositório remoto

- [ ] Crie um repositório público no GitHub.
- [ ] Conecte o repositório local utilizando `git remote add origin`.
- [ ] Envie sua branch principal para o GitHub.
- [ ] Crie uma branch de funcionalidade.
- [ ] Envie essa branch utilizando `git push -u origin`.

## 9. O que estudar depois?

Depois de dominar esses comandos, estude os seguintes conceitos:

1. **Merge:** como integrar branches.
2. **Merge Conflict:** como resolver conflitos.
3. **Rebase:** como reorganizar o histórico de commits.
4. **Cherry-pick:** como selecionar commits específicos de outra  
    branch.
5. **Stash:** como guardar temporariamente alterações.
6. **Reset:** como voltar para estados anteriores do repositório.
7. **Revert:** como desfazer commits sem apagar o histórico.
8. **Pull Requests:** como revisar e integrar código.
9. **Git Flow:** estratégia de organização de branches.
10. **GitHub Actions:** automação de testes e integração contínua  
    (CI/CD).

### Recomendação de estudo

Para evoluir como desenvolvedor Flutter, domine especialmente:

- `branch`
- `commit`
- `push`
- `pull`
- `fetch`
- `merge`
- `rebase`
- Resolução de conflitos

Esses conceitos são utilizados constantemente no desenvolvimento de  
aplicações e no trabalho em equipe.

**Próximo passo recomendado:** estudar Merge, Merge Conflict e Rebase,  
pois esses conceitos complementam diretamente o conteúdo deste guia.