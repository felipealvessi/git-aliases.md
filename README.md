# Git alias - seja rápido, seja breve!

Git freak como sou, precisava compartilhar algo útil sobre ele, claro. E, já que não vejo muito por aí o pessoal usando, resolvi falar dos alias do git! É um recurso que eu uso muito, e nunca entendi porque muitas pessoas não são adeptas. :confused:

Pelo nome você já deve perceber que os alias no git são atalhos. Atalhos pro quê? São atalhos para comandos do git e até comandos shell se você quiser. E é bem fácil cadastrar um alias:

```
$ git config --global alias.st status
```

Com esse código, você cadastra um alias `st` para o subcomando `status` do git. 

A opção `--global` quer dizer que o alias será aplicado no arquivo `.gitconfig` dentro do seu diretório `home`, e por isso o alias será aplicado em todos seus repositórios. Sem esta opção, o alias será aplicado no `.gitconfig` do repositório atual, logo só será aplicado apenas a ele.

Agora voltando ao alias. Criamos o alias `st` para o subcomando `status` certo? Como uso esse alias agora? Bem fácil:

```
$ git st
On branch master
Your branch is up-to-date with 'origin/master'.

nothing to commit, working directory clean
```

Isso, como podem perceber, foi igual a executar o comando `git status`. Mas vamos a um exemplo de alias muito  mais interessante que uso no dia-a-dia aqui:

```
$ git lg
*   ebd5ff6 (HEAD, origin/master, origin/feature/org-permissions, origin/HEAD, master) Merged in feature/rolify (pull request #21)
|\
| * 486b8a7 (origin/feature/rolify, feature/rolify) Updating seeds after rolify refactor
| * 12d24a7 Fixing problems on tests after rolify
| * 4afb86d Fixing problems after pipe permissions change
| * 1e57066 Fixing problems on phases factory
| * a8b72f1 Saving user roles instead of members of pipes
| * 6a19bf8 Fixing problems on pipe roles changes
:
```

O que é isso? Uma lista gráfica dos commits, com anotações de onde está o HEAD, e em que commit cada branch está apontando. Mas percebam que usei um alias `lg`. 

Agora por que esse caso o alias é tão interessante? Olha qual o comando que eu teria que executar para conseguir esse mesmo resultado sem o alias:

```
$ git log --all --graph --decorate --oneline --abbrev-commit
*   ebd5ff6 (HEAD, origin/master, origin/feature/org-permissions, origin/HEAD, master) Merged in feature/rolify (pull request #21)
|\
| * 486b8a7 (origin/feature/rolify, feature/rolify) Updating seeds after rolify refactor
| * 12d24a7 Fixing problems on tests after rolify
| * 4afb86d Fixing problems after pipe permissions change
| * 1e57066 Fixing problems on phases factory
| * a8b72f1 Saving user roles instead of members of pipes
| * 6a19bf8 Fixing problems on pipe roles changes
:
```

Cansou até de ler não é? Pois é...

Ah, eu havia comentado que dá pra executar comando externo certo? Então, é só colocar `!` na frente do código para seu alias e pronto:

```
$ git config --global alias.visual '!gitk'
```

Isso pode ser usado em subcomandos do git também para por exemplo executar dois comandos em sequência. Eu por exemplo uso muito esse alias aqui:

```
$ git config --global alias.ac '!git add -A && git commit'
```

Esse alias basicamente vai adicionar todos os arquivos que estiverem unstaged com um `git add -A` e logo depois abrir meu editor de commit message, tudo isso só com um `git ac`.

Lembrando tudo isso é salvo no seus arquivos de configuração do git, se você abrir um (pode ser o `~/.gitconfig` por exemplo) você vai ver uma seção `[alias]`. Olha como a minha está:

```
[alias]
  co = checkout
  lg = log --all --graph --decorate --oneline --abbrev-commit
  cm = commit
  ac = !git add -A && git commit
  st = status -sb
  tags = tag -l
  branches = branch -a
  remotes = remote -v
```

Você pode editar esse arquivo à vontade, desde que você coloque opções válidas (não é difícil, é só lembrar de colocar `!` em comandos que não são subcomandos do git). E claro, se você for alguém que não gosta de ter que ficar configurando essas coisas uma a uma a cada máquina que usa, guarde esse arquivo em algum lugar e pronto. 
