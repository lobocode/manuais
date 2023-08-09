# Guia Básico do Git

Este guia vai te ajudar com os comandos mais básicos do Git, interagindo com o GitHub, e entenderá a razão por trás de cada comando.

## Índice

- [Origem e História do Git](#origem-e-história-do-git)
- [Diferença entre Git e GitHub](#diferença-entre-git-e-github)
- [Configuração Inicial](#configuração-inicial)
- [Trabalhando com Repositórios do GitHub](#trabalhando-com-repositórios-do-github)
- [Comandos Básicos](#comandos-básicos)
- [Branches](#branches)
- [GitFlow: Uma Estratégia de Branching](#gitflow-uma-estratégia-de-branching)
- [Resolvendo Conflitos no Git](#resolvendo-conflitos-no-git)
- [Dicas Finais](#dicas-finais)


## Origem e História do Git

### Quem criou o Git e por quê?

Git foi criado por **Linus Torvalds**, o visionário por trás do Linux. Antes do Git, o desenvolvimento do kernel Linux usava um sistema de controle de versão chamado BitKeeper. No entanto, as questões de licenciamento com o BitKeeper levaram a comunidade Linux a uma encruzilhada. Linus, vendo a necessidade de uma ferramenta que fosse robusta, eficiente e que se adequasse perfeitamente às demandas de desenvolvimento do Linux, decidiu criar sua própria ferramenta. Ele imaginou algo que fosse mais rápido e tivesse um design mais flexível do que os sistemas de controle de versão disponíveis na época. Assim, em **2005**, o Git foi introduzido ao mundo.

### Características principais do Git:

- **Distribuído**: Cada desenvolvedor tem uma cópia local completa do histórico de desenvolvimento, e as mudanças são copiadas de um repositório para outro.
  
- **Integridade**: Com o Git, tudo é verificado por checksum antes de ser armazenado, o que garante a integridade e confiabilidade dos dados.
  
- **Flexibilidade**: Seu design flexível permite que os desenvolvedores escolham seu fluxo de trabalho - seja trabalhando linearmente, criando múltiplas ramificações ou até mesmo trabalhando desconectado.

## Diferença entre Git e GitHub

- **Git**: É uma ferramenta de controle de versão distribuído, que permite a programadores rastrear e trabalhar com versões diferentes de um projeto. O Git gerencia e rastreia as mudanças no código, permitindo que várias pessoas colaborem em um único projeto.

- **GitHub**: É uma plataforma de hospedagem para repositórios Git. Ela fornece uma interface gráfica para gerenciar projetos Git e colaborar com outros desenvolvedores.


## Configuração Inicial

### Configurando sua identidade

O Git usa um sistema de identificação para relacionar commits a uma pessoa. Isso ajuda em projetos colaborativos para identificar quem fez quais alterações. Quando você configura o Git pela primeira vez usando `git config`, um arquivo chamado `.gitconfig` é criado em seu diretório home. Este arquivo armazena as configurações do usuário para o Git.

- **Windows**: Localizado em `C:\Users\<seu nome de usuário>`.
- **Mac e Linux**: Localizado em `~/`.

O arquivo `.gitconfig` armazena informações como nome de usuário, email, e outras configurações do Git que você pode definir. Ele permite que você configure o comportamento padrão do Git, como a ferramenta de mesclagem a ser usada ou cores para a saída do comando.

1. **Configurando seu nome**
   ```bash
   git config --global user.name "Seu Nome"
   ```
   O `--global` significa que esta configuração é aplicada globalmente para todos os repositórios no seu sistema. Se você omitir `--global`, a configuração será aplicada apenas para o repositório atual.

2. **Configurando seu email**
   ```bash
   git config --global user.email seuemail@example.com
   ```

### Inicializando um Repositório Git

O comando `init` é usado para iniciar um novo repositório Git no seu projeto. Ele basicamente começa a rastrear um diretório existente e começa a observar mudanças.

```bash
git init
```

## Trabalhando com Repositórios do GitHub

### Clonando um Repositório

Para copiar um repositório já existente do GitHub para sua máquina local, usamos o comando `clone`.

```bash
git clone URL_DO_REPOSITÓRIO
```

### Conectando um Repositório Local a um Remoto

Se você tem um repositório local e deseja começar a sincronizá-lo com um repositório remoto no GitHub, você conecta os dois com o comando abaixo.

```bash
git remote add origin URL_DO_REPOSITÓRIO
```
Aqui, `origin` é um nome padrão dado ao URL remoto, mas pode ser qualquer nome.

## Comandos Básicos

1. **Adicionando arquivos à área de staging**
   A "área de staging" é como uma área de preparação. Os arquivos aqui estão prontos para serem incluídos no próximo commit.
   ```bash
   git add NOME_DO_ARQUIVO # Adiciona um arquivo específico
   git add .               # Adiciona todos os arquivos modificados
   ```

2. **Commitando suas mudanças**
   Um "commit" é como uma fotografia do seu código em um determinado momento. Ele registra as mudanças que você fez.
   ```bash
   git commit -m "Mensagem descritiva do que foi feito"
   ```

Um "commit" em Git é uma "fotografia" ou registro do estado atual do código. Imagine que você está escrevendo um livro. Cada vez que você termina um capítulo ou uma seção significativa, você tira uma "foto" dessa parte, para que possa voltar a ela, se necessário.

### Exemplos de commits:

- **Boa prática**: "Adicionada função de autenticação de usuário"
- **Má prática**: "Alterações" ou "Atualizações" ou até simplesmente commitar qualquer coisa só por commitar.

### O que é uma boa prática de commit?

1. **Descritivo, mas conciso**: Descreva o que o commit faz, não como ele faz.
2. **Uso do tempo presente**: Por exemplo, "Adiciona" em vez de "Adicionado".
3. **Evite commits muito amplos**: Se um commit faz muitas coisas diferentes (corrige um bug, adiciona uma nova funcionalidade, muda estilos), é melhor dividir em vários commits separados.

3. **Enviando mudanças para o GitHub**
   O comando `push` envia seus commits locais para o repositório remoto.
   ```bash
   git push origin NOME_DA_BRANCH
   ```

### Antes de enviar um `push`

Antes de enviar suas mudanças para um repositório remoto, considere:

1. **Verificar o status com `git status`**: Garanta que todos os arquivos desejados estejam na área de staging.
2. **Revisar seus commits**: Use `git log` para ver seu histórico de commits e garantir que não haja erros.
3. **Testar suas mudanças localmente**: Sempre teste o código em sua máquina local antes de enviá-lo.
4. **Atualize e integre mudanças**: Antes de enviar suas mudanças, faça `git pull` para integrar quaisquer atualizações do repositório remoto.

4. **Baixando mudanças do GitHub**
   O comando `pull` pega as mudanças de um repositório remoto e as aplica ao seu repositório local.
   ```bash
   git pull origin NOME_DA_BRANCH
   ```
   
## Branches

### O que é uma Branch?

Uma "branch" (ramificação ou ramo) no Git é basicamente uma linha de desenvolvimento independente. Pense nisso como uma forma de ter sua própria área de trabalho onde você pode fazer alterações sem afetar a linha principal (muitas vezes chamada de "master" ou "main") ou outras branches.

### Por que usar branches?

- **Isolar Desenvolvimento**: Branches permitem que você trabalhe em novos recursos ou bugs sem perturbar a base de código principal.
- **Facilitar a Colaboração**: Vários desenvolvedores podem trabalhar em diferentes recursos ou correções ao mesmo tempo, cada um em sua própria branch.
- **Prevenir erros**: Ao testar mudanças em uma branch separada, você pode garantir a estabilidade da branch principal.

### Como as Branches Funcionam?

Quando você cria uma branch, você está essencialmente criando um ponteiro para um commit específico. À medida que você faz novos commits em sua branch, esse ponteiro se move para frente, junto com a linha principal de desenvolvimento.

### Comandos Básicos para Branches

- **Criar uma nova branch**: 
  ```bash
  git checkout -b nome_da_branch
  ```
  
- **Mudar para uma branch existente**: 
  ```bash
  git checkout nome_da_branch
  ```
  
- **Listar todas as branches**: 
  ```bash
  git branch
  ```

- **Deletar uma branch**: 
  ```bash
  git branch -d nome_da_branch
  ```

## GitFlow: Uma Estratégia de Branching

GitFlow é uma estratégia de organização de branches que define tipos específicos de branches e como elas interagem.

### Componentes principais:

1. **Master (Main)**: A branch principal onde o código em produção reside. Deve estar sempre pronta para deploy.

2. **Develop**: Uma branch para desenvolvimento geral. Novos recursos e correções são mesclados aqui antes de se moverem para a Master.

3. **Feature branches**: Para desenvolvimento de novos recursos. Eles são criados a partir do `develop` e são mesclados de volta ao `develop` quando o recurso estiver pronto.

4. **Release branches**: Prepara para uma nova release de produção. Ela permite fazer pequenas correções ou preparativos para a release. Uma vez pronta, é mesclada na `master` e `develop`.

5. **Hotfix branches**: Para correções críticas que precisam ser introduzidas imediatamente na produção.

### Vantagens do GitFlow:

- **Organização clara**: Ao seguir o GitFlow, você terá uma estrutura clara de onde e como o código deve ser mesclado.
- **Desenvolvimento Paralelo**: Permite desenvolvimento simultâneo de vários recursos e correções.
- **Versões Estáveis**: Ao separar claramente as releases e hotfixes, você garante que a master esteja sempre pronta para deploy.

Conclusão: Branches são uma ferramenta poderosa no Git, e o GitFlow é apenas uma das muitas estratégias que você pode usar para gerenciar como essas branches interagem. Encontre a estratégia que melhor se adapta à sua equipe e projeto.

 **Criando uma nova branch**
  m Git, a "branch" (ramo) é uma versão paralela do código. Isso permite trabalhar em recursos ou experimentos separadamente.
   ```bash
   git checkout -b NOME_DA_NOVA_BRANCH
   ```

6. **Mudando para uma branch existente**
   ```bash
   git checkout NOME_DA_BRANCH
   ```

7. **Mergeando branches**
   Se você quiser integrar as mudanças de uma branch em outra, use o comando `merge`.
   ```bash
   git merge NOME_DA_BRANCH
   ```

## Resolvendo Conflitos no Git

Os conflitos são inevitáveis quando trabalhamos em um ambiente colaborativo. Eles ocorrem quando duas ou mais pessoas fazem alterações no mesmo trecho de código em um arquivo e, depois, tentam combinar (ou "merge") essas mudanças. Como o Git não sabe qual alteração deve prevalecer, ele marca o arquivo e pede intervenção humana para resolver o conflito.

1. **Identifique o Conflito**:
   Ao tentar combinar branches com `git merge` ou reordenar commits com `git rebase`, o Git informará se houver conflitos. Você pode verificar quais arquivos estão em conflito com:
2. **Visualize as Discrepâncias**:
Abra o arquivo em um editor de texto. O Git demarcará a área problemática com `<<<<<<<`, `=======`, e `>>>>>>>`. 
3. **Resolva Manualmente o Conflito**:
Agora, cabe a você resolver o dilema:
- Decida qual alteração manter, qual descartar ou se deseja combinar ambas.
- Remova as marcas de conflito (`<<<<<<<`, `=======`, e `>>>>>>>`).
- Salve o arquivo.

4. **Confirme a Resolução**:
Depois de limpar todas as discrepâncias, informe ao Git que o conflito foi resolvido:

```bash
git add [nome_do_arquivo]
```

Continue com sua ação inicial, seja ela um `merge` ou `rebase`.

5. **Ferramentas Adicionais**:
Existem ferramentas gráficas e ambientes de desenvolvimento integrados (IDEs) que oferecem suporte visual na resolução de conflitos. Eles podem simplificar a tarefa ao destacar visualmente os conflitos e permitir correções com cliques de botão. Em resumo, o Git revolucionou o controle de versão com sua eficiência e flexibilidade. Conflitos, embora possam parecer intimidantes no início, são apenas parte do processo colaborativo e, com prática e compreensão, tornam-se facilmente gerenciáveis.


## Dicas Finais

- **Verificando o status**
  Para ver o status dos seus arquivos (modificados, não rastreados, etc.), use:
  ```bash
  git status
  ```

- **Histórico de Commits**
  Para rever os commits anteriores e suas mensagens:
  ```bash
  git log
  ```

### Git aliases

Quando você trabalha com o Git no terminal, muitas vezes precisa digitar comandos longos e repetitivos. Os aliases permitem que você crie abreviações para esses comandos, facilitando a execução de tarefas comuns. Em vez de digitar algo como:

```bash
git commit -m "Minha mensagem de commit"
```

Você pode criar um alias, como gcm, para que você possa simplesmente digitar:

```bash
gcm "Minha mensagem de commit"
```

Para criar aliases como os quais estão abaixo, basta abrir o ``.bashrc`` que está em seu diretório home no Windows ou Linux/Mac. No windows geralmente se encontra em `c:\Users\User\.bashrc` e no Linux/Mac em `~/.bashrc`, e colar as dicas abaixo:


### Básicos
```bash
alias gs='git status'
alias ga='git add'
alias gc='git commit -m'
alias gcm='git commit -m'
alias gp='git push'
alias gpl='git pull'
alias gl='git log'
alias gd='git diff'
alias gb='git branch'
alias gco='git checkout'
alias gr='git remote -v'
alias gbr='git branch -a'
```

### Agilizando o Commit

```bash
alias gca='git commit -a -m'
alias gcaa='git commit -a --amend'
alias gcp='git commit -m "WIP: "'
alias gcam='git commit -a -m'
alias gcamend='git commit --amend --no-edit'
alias gfixup='git commit --fixup'
alias gautosquash='git rebase -i --autosquash'
```

### Visualizando alterações
```bash
alias gds='git diff --staged'
alias gdc='git diff --cached'
alias gdt='git difftool'
alias gk='gitk --all'
```

### Branches

```bash
alias gcb='git checkout -b'
alias gbd='git branch -d'
alias gbD='git branch -D'
alias gba='git branch -a'
alias gbu='git branch --set-upstream-to'
alias gbrn='git branch --rename'
alias gm='git merge'
alias gmg='git merge --no-ff'
```


### Stash

```bash
alias gsl='git stash list'
alias gsp='git stash pop'
alias gss='git stash save'
alias gsa='git stash apply'
alias gsd='git stash drop'
alias gsc='git stash clear'
```

### Miscelânea

```bash
alias grb='git rebase'
alias grbc='git rebase --continue'
alias grbi='git rebase -i'
alias grba='git rebase --abort'
alias gf='git fetch'
alias gcl='git clone'
alias glog='git log --oneline --decorate --graph'
```

### Configuração

```bash
alias gcfg='git config --global'
alias gcfgl='git config --list'
alias gcfge='git config --global --edit'
```

### Limpeza

```bash
alias gclean='git clean -fd'
alias gprune='git remote prune origin'
```

### Remoto

```bash
alias gtrack='git branch -u'
alias gcpo='git checkout -b'
alias gpom='git pull origin'
alias gpro='git pull --rebase origin'
alias gpusho='git push origin'
alias gpsh='git push'
alias gpt='git push --tags'
```

Explore mais! Git e GitHub têm muitos recursos avançados. Assim que se sentir confortável, mergulhe na documentação oficial para aprender mais!


