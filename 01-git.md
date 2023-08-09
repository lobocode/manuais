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
- [Comandos avançados do git](#comandos-avançados-do-git)
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

### Gerando uma Chave SSH para o Git

1. Abra o terminal.
2. Verifique se você já tem chaves SSH existentes:

```bash
ls -al ~/.ssh
```

Se você já tiver chaves, elas serão exibidas com extensões .pub (chaves públicas) e possivelmente outros arquivos. Para gerar uma nova chave SSH, use o seguinte comando, substituindo pelo seu endereço de e-mail:

```bash
ssh-keygen -t ed25519 -C "seu-email@example.com"
```

Escolha um local para salvar a chave (pressione Enter para aceitar o local padrão) e defina uma senha (ou deixe em branco). Isso criará duas chaves, uma pública (com extensão .pub) e uma privada (sem extensão).

### Configurando a Chave SSH no GitHub

1. Abra o arquivo da sua chave pública em um editor de texto:

```bash
cat ~/.ssh/id_ed25519.pub
```

2. Copie todo o conteúdo da chave pública.
3. Acesse sua conta no GitHub.
4. Clique na sua foto de perfil no canto superior direito e escolha "Settings".
5. No menu lateral esquerdo, clique em "SSH and GPG keys".
6. Clique em "New SSH key" ou "Add SSH key".
7. Dê um título à chave (para identificação).
8. Cole a chave pública que você copiou no campo "Key".
9. Clique em "Add SSH key" para salvar.
10. Você pode ser solicitado a confirmar a ação inserindo sua senha do GitHub.

Agora sua chave SSH está configurada no GitHub. Lembre-se de manter a chave privada segura, pois ela dá acesso às suas contas e repositórios. Agora você pode copiar todo o conteúdo acima e colá-lo em um arquivo Markdown para referência futura. Certifique-se de seguir as etapas cuidadosamente ao gerar e configurar sua chave SSH no Git e no GitHub.

### Inicializando um Repositório Git

O comando `init` é usado para iniciar um novo repositório Git no seu projeto. Ele basicamente começa a rastrear um diretório existente e começa a observar mudanças.

```bash
git init
```

## Trabalhando com Repositórios do GitHub

### Conectando um Repositório Local a um Remoto

Se você tem um repositório local e deseja começar a sincronizá-lo com um repositório remoto no GitHub, você conecta os dois com o comando abaixo.

```bash
git remote add origin URL_DO_REPOSITÓRIO
```

Aqui, `origin` é um nome padrão dado ao URL remoto, mas pode ser qualquer nome. Outra opção é vc criar o repositório direto no Github bastando apenas clonar ele na máquina. Para copiar um repositório já existente do GitHub para sua máquina local, usamos o comando `clone`.

```bash
git clone URL_DO_REPOSITÓRIO
```

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
5. **Baixando mudanças do GitHub**
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
git branch -a
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

Embora o GitFlow seja um modelo de fluxo de trabalho popular para o desenvolvimento de software, existem situações em que pode não ser a melhor escolha. Aqui estão alguns cenários em que o GitFlow pode ser uma má ideia:

1. **Projetos pequenos ou individuais**: O GitFlow foi projetado para projetos maiores e equipes de desenvolvimento. Em projetos pequenos ou quando você é o único desenvolvedor, o GitFlow pode adicionar complexidade desnecessária e tornar o processo de desenvolvimento mais burocrático.
2. **Iterações rápidas e entrega contínua**: Se você estiver trabalhando em um ambiente que exige entregas frequentes e rápidas, o GitFlow pode se tornar um gargalo, pois ele introduz várias etapas (branches de features, branches de release, etc.) que podem retardar o processo de entrega.
3. **Manutenção de versões antigas**: O GitFlow é útil para gerenciar versões de software com suporte a longo prazo. No entanto, se você não precisa manter várias versões antigas do software, a complexidade adicional introduzida pelo GitFlow pode ser excessiva.
4. **Curva de aprendizado**: Se sua equipe não estiver familiarizada com o GitFlow ou não tiver experiência em lidar com fluxos de trabalho mais complexos, a implementação do GitFlow pode levar a erros e confusões.
5. **Foco excessivo na estrutura**: O GitFlow enfatiza uma estrutura rígida de branches (feature, develop, release, hotfix, etc.). Em alguns casos, isso pode levar a uma mentalidade focada mais na estrutura do que na entrega de valor ao cliente.
6. **Colaboração externa limitada**: Se você estiver trabalhando com colaboradores externos ou equipes distribuídas, o GitFlow pode ser mais complicado de gerenciar, especialmente se todos não estiverem alinhados com o mesmo fluxo de trabalho.
7. **Integração contínua complexa**: Se o seu processo de integração contínua (CI) não estiver configurado para lidar bem com as diferentes branches do GitFlow, você pode encontrar problemas ao automatizar a construção, teste e implantação.
8. **Projeto experimental ou de pesquisa**: Em situações em que você está fazendo experimentações rápidas, prototipagem ou pesquisas, a rigidez do GitFlow pode ser excessiva. Nesses casos, fluxos de trabalho mais flexíveis, como o GitHub Flow, podem ser mais adequados.

Lembre-se de que não existe um único modelo de fluxo de trabalho que funcione para todos os projetos. A escolha do modelo depende das necessidades específicas da equipe, do projeto e do ciclo de vida do software. Pode ser útil adaptar ou mesclar diferentes abordagens para criar um fluxo de trabalho personalizado que atenda às necessidades do seu projeto.

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

## Comandos avançados do git

O `git rebase` é uma operação que altera o histórico de commits, reorganizando-os linearmente. Ele "reaplica" os commits de uma branch em relação à referência de outra branch, geralmente a branch alvo é a que você deseja que o histórico reorganizado seja baseado. Isso é útil para manter o histórico de commits mais limpo, linear e fácil de entender. O `git rebase`` é mais adequado para casos em que você deseja:

1. **Manter um histórico linear**: Reorganizar commits para ter um histórico mais linear e fácil de seguir, em vez de ter muitos merges.
2. **Integrar mudanças da branch pai**: Quando você trabalhou em uma branch secundária e deseja integrar as mudanças mais recentes da branch pai (normalmente a main ou master) sem criar um commit de merge.
3. **Corrigir conflitos de maneira gradual**: Resolver conflitos de merge enquanto você aplica seus commits, em vez de resolver tudo no final.

Aqui está um guia passo a passo sobre como usar o `git rebase``:

1. **Atualize sua branch**: Antes de rebase, certifique-se de que sua branch está atualizada com a branch pai (ou a branch na qual você deseja aplicar as mudanças).

```bash
git checkout sua-branch
git pull origin branch-pai
```

2. **Inicie o rebase**: Use o comando git rebase seguido da branch que você deseja como base (normalmente a branch pai).

```bash
git rebase branch-pai
```

3. **Resolva conflitos**: Se houver conflitos, o rebase será interrompido para permitir que você resolva cada conflito manualmente. Use `git add` para marcar os arquivos como resolvidos e, em seguida, continue o rebase com `git rebase --continue``.
4. **Conclua o rebase**: Após resolver todos os conflitos, o rebase continuará até que todos os seus commits sejam aplicados na ordem em que foram originalmente feitos.

### Exemplo de uso do git rebase

Suponha que você tenha uma branch `feature` onde trabalhou em uma funcionalidade específica. Enquanto isso, houve mudanças na branch `main`. Para atualizar sua funcionalidade e integrar as mudanças recentes da `main`, você faria o seguinte:

```bash
# Atualize a branch feature
git checkout feature
git pull origin main

# Inicie o rebase
git rebase main

# Resolva conflitos, se houver
# Use git add para marcar arquivos como resolvidos

# Continue o rebase após resolver conflitos
git rebase --continue

# Repita até que todos os commits sejam aplicados

# Finalize o rebase
git push origin feature
```

Lembre-se de que, ao reescrever o histórico, você está criando novos commits. Portanto, evite usar o `git rebase` em commits que já foram compartilhados com outras pessoas, pois isso pode causar problemas de sincronização para os outros colaboradores do repositório.

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


