# Aprenda Git

> Um guia fácil para começar no Git.

## Sumário

-   [Conceitos básicos de Git]()
-   [Configuração inicial]()
-   [Comandos úteis]()
-   [Situações e problemas comuns]()
-   [Um dia de trabalho qualquer com Git]()

## Conceitos básicos de Git

Em breve.

## Configuração inicial

Antes de utilizar o Git é interessantes fazer algumas configurações. Você pode dizer a ele seu nome e seu e-mail, por exemplo, para que eles fiquem registrados nos commits que você fizer. Para isso abra o terminal e digite:

```sh
git config --global user.name "Seu Nome"
git config --global user.email seuemail@exemplo.com
```

Para mudar o editor de texto padrão, utilize:

```sh
git config --global core.editor "nano"
```

Você pode escolher o editor que preferir no lugar do `nano`, mas é o recomendado para iniciantes por ser mais fácil de usar do que o `vi`, por exemplo.

A flag `--global` sinaliza que essa configuração será o padrão para todos os projetos. Para configurar uma variável apenas para um projeto específico, navegue até ele pelo terminal e utilize `git config` sem a flag `--global`.

## Comandos úteis

### `git log`

> zsh: `gl`

Mostra o histórico de todos os commits

### `git add`

### `git commit`

### `git reset`

### `git checkout`

### `git pull`

### `git push`

### `git rebase`

### `git cherry-pick`

## Um dia de trabalho qualquer com Git

Em breve.

## Situações e problemas comuns

### Elencar/rastrear arquivos

1.  Use `git add <nome-do-arquivo>` para elencar um arquivo específico ou `git add .` para elencar todos os arquivos detectáveis pelo Git.

### Descartar alterações no Working Directory

1.  Use `git checkout -- <nome-do-arquivo>` para descartar alterações no arquivo. Serve apenas para arquivos ainda não elencados, mas modificados ou não-rastreados.

### Deselencar arquivos

1.  Use `git reset HEAD <nome-do-arquivo>` para remover ele dos arquivos elencados. As alterações serão preservadas, mas ele voltará à working tree.

### Atualizar seu código local com a última versão do repositório remoto

1.  Use `git pull --rebase`. É semelhante ao `git pull`, mas commits de merge não são criados, o que reduz a poluição do histórico do projeto.
2.  Em caso de conflito, resolva os conflito, salve os arquivo, faça o staging com `git add .` ou `git add <nome-arquivo>` e em seguida `git rebase --continue`.

### Trazer commits de um branch para outro

1.  Faça checkout no branch onde você deseja aplicar os commits com `git checkout <branch-destino>`.
2.  Faça o merge dos commits do branch de onde você deseja trazer os commits com `git merge <branch-origem>`.

Alternativamente você pode utilizar `git merge <branch-destino> <branch-origem>`.

### Aplicar commits de um branch local em cima de outro branch

1.  Atualize o branch sobre o qual você deseja aplicar seus commits locais com `git pull` ou `git pull --rebase`.
2.  Faça checkout em seu branch local com `git checkout <branch-local>`
3.  Use `git rebase <branch-destino>` para aplicar todos os commits do `<branch-local>` seu branch local em cima do `<branch-destino>`.

Alternativamente você pode utilizar `git rebase <branch-destino> <branch-local>`.

Ex:

```sh
# Isso moverá os commits da branch feature/style para cima da branch develop
git rebase develop feature/style
```

> Não faça isso a partir de um branch que esteja publicado em seu repositório remoto. O rebase reescreve o histórico do branch.

### Navegar em um commit anterior

> Requer `HEAD` limpo!

1.  Use `git log` para ver o hash dos commits.
2.  Digite `git checkout <commit_hash>`, onde `<commit_hash>` é o hash do commit que você deseja visualizar.
3.  Se quiser fazer alterações e preservá-las, crie um novo branch com `git checkout -b <branch-name>` e edite à vontade.

### Desfazer o último commit (local)

1.  Use `git reset --soft HEAD^` para desfazer o último commit, mantendo os arquivos anteriormente commitados ainda no staging.
2.  Use `git reset --mixed HEAD^` para desfazer o último commit, mantendo os arquivos anteriormente commitados na working tree.
3.  Use `git reset --hard HEAD^` para desfazer o último commit e descartar todos os arquivos e alterações introduzidos pelo commit desfeito.

### Desfazer commits locais até um commit específico (local)

1.  Utilize os comandos anteriores de forma semelhante, mas em vez do `HEAD^`, utilize a hash último commit que deseja preservar. Todos os commits entre o `HEAD` e o commit do hash digitado (não incluso) serão desfeitos. O comportamento de preservar as mudanças ou não dependem das flags `--soft`, `--mixed`, `--hard`.

### Inserir as mudanças de um commit no `HEAD` atual

> Requer `HEAD` limpo!

1.  Use `git log --all` para verificar o hash do commit que você quer inserir no seu branch.
2.  Já no `HEAD` do branch que deseja aplicar o commit, utilize `git cherry-pick <commit_hash>` para aplicar as mudanças introduzidas pelo commit ou `git cherry-pick <branch-name>` para aplicar as mudanças introduzidas pelo commit no `HEAD` daquele branch.

### Limpar o cache do Git sem remover arquivos do disco

[Fonte](http://www.randallkent.com/2010/04/30/gitignore-not-working/)

Isso acontece quando um arquivo é inicialmente rastreado pelo Git mas em algum momento no futuro esse arquivo é adicionado ao .gitignore. Se esse arquivo for removido do projeto logo após essa adição, sua remoção precisará ser commitada. Se ele for adicionado novamente no mesmo diretório onde estava antes por algum motivo,ele provavelmente será rastreado também.

Para resolver o problema de arquivo persistente, limpe o cache do Git das seguinte formas:

#### Opção 1 - Mais fácil de entender

Remove todos os arquivos do cache do Git (ou seja, para de rastrear todos os arquivos, mas os matém no disco) e faz o commit de tudo, menos dos arquivos persistentes após adição no .gitignore. Isso vai basicamente adicionar todos os arquivos novamente.

```sh
git rm -r --cached .    # Remove todos os arquivos do Git, sem remover do disco
git add .               # Adiciona novamente todos os arquivos ao Git
git commit              # Commita arquivos, sem os arquivos em cache
```

#### Opção 2 - Mais eficiente

Remove do cache apenas os arquivos que estão listados no `.gitignore`:

```
for file in `cat .gitignore` ; do git rm -r --cached $file ; done
```

## Para se aprofundar mais

-   [Git e Github para iniciantes (Curso gratuito)](https://www.udemy.com/git-e-github-para-iniciantes/)
-   [Pro Git (Livro gratuito)](https://git-scm.com/book/pt-br/v2)
