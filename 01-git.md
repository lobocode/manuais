# Guia Básico do Git

Este guia vai te ajudar com os comandos mais básicos do Git, interagindo com o GitHub, e entenderá a razão por trás de cada comando.

## Índice

- [Diferença entre Git e GitHub](#diferença-entre-git-e-github)
- [Configuração Inicial](#configuração-inicial)
- [Trabalhando com Repositórios do GitHub](#trabalhando-com-repositórios-do-github)
- [Comandos Básicos](#comandos-básicos)
- [Branches](#branches)
- [GitFlow: Uma Estratégia de Branching](#gitflow-uma-estratégia-de-branching)
- [Dicas Finais](#dicas-finais)


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

Explore mais! Git e GitHub têm muitos recursos avançados. Assim que se sentir confortável, mergulhe na documentação oficial para aprender mais!


