# Aprenda Git

> Um guia básico para começar no Git.

## Conceitos básicos de Git

## Comandos úteis

### `git log`

> zsh: `gl`

Mostra o histórico de todos os commits

## Situações comuns

### Elencar/rastrear arquivos

1.  Use `git add <nome-do-arquivo>` para elencar um arquivo específico ou `git add .` para elencar todos os arquivos detectáveis pelo Git.

### Descartar alterações no working directory

1.  Use `git checkout -- <nome-do-arquivo>` para descartar alterações no arquivo. Serve apenas para arquivos ainda não elencados, mas modificados ou não-rastreados.

### Deselencar arquivos

1.  Use `git reset HEAD <nome-do-arquivo>` para remover ele dos arquivos elencados. As alterações serão preservadas, mas ele voltará à working tree.

### Atualizar seu código local com a última versão do repositório remoto

1.  Use `git pull --rebase`. É semelhante ao `git pull`, mas commits de merge não são criados, o que reduz a poluição do histórico do projeto.
2.  Em caso de conflito, resolva os conflito, salve os arquivo, faça o staging com `git add .` ou `git add <nome_arquivo>` e em seguida `git rebase --continue`.

### Navegar em um commit anterior

> Requer `HEAD` limpo!

1.  Use `git log` para ver o hash dos commits.
2.  Digite `git checkout <commit_hash>`, onde `<commit_hash>` é o hash do commit que você deseja visualizar.
3.  Se quiser fazer alterações e preservá-las, crie uma nova branch com `git checkout -b <branch-name>` e edite à vontade.

### Desfazer o último commit (local)

1.  Use `git reset --soft HEAD^` para desfazer o último commit, mantendo os arquivos anteriormente commitados ainda no staging.
2.  Use `git reset --mixed HEAD^` para desfazer o último commit, mantendo os arquivos anteriormente commitados na working tree.
3.  Use `git reset --hard HEAD^` para desfazer o último commit e descartar todos os arquivos e alterações introduzidos pelo commit desfeito.

### Desfazer commits locais até um commit específico (local)

1.  Utilize os comandos anteriores de forma semelhante, mas em vez do `HEAD^`, utilize a hash último commit que deseja preservar. Todos os commits entre o `HEAD` e o commit do hash digitado (não incluso) serão desfeitos. O comportamento de preservar as mudanças ou não dependem das flags `--soft`, `--mixed`, `--hard`.

### Inserir as mudanças de um commit no `HEAD` atual

> Requer `HEAD` limpo!

1.  Use `git log --all` para verificar o hash do commit que você quer inserir na sua branch.
2.  Já no `HEAD` da branch que deseja aplicar o commit, utilize `git cherry-pick <commit_hash>` para aplicar as mudanças introduzidas pelo commit ou `git cherry-pick <branch-name>` para aplicar as mudanças introduzidas pelo commit no `HEAD` daquela branch.
