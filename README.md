# Estudando versionamento com git

## Navegando no histórico

- Ver como o repositório se encontra em algum commit:
```git
git checkout <commit> <file'opcional'>
```

Nesse momento o repositório fica em modo detached head e não é possível adicionar novos commits.

- Voltar para o último commit:
```git
git checkout master
```

## Desfazendo com checkout

- Desfazer todas as alterações que não estejam em stage:
```git
git checkout -- <path_or_file>
```

Se quiser desfazer tudo:
```git
git checkout -- .
```

- Desfazer todas as alterações desde o último commit, incluindo o stage:
```git
git checkout HEAD -- <path_or_file>
```

## Desfazendo com Revert e Reset

### Revert
- Vai criar um novo commit desfazendo tudo o que foi feito no commit especificado.
- Útil para desfazer um commit antigo

```git
git revert <commit>
```

### Reset
Normalmente queremos desfazer as alterações no último commit, para isso é mais viável utilizar o reset.
- Resetar o repositório para um determinado commit:
```git
git reset <commit>
```

- Resetar e remover todas as alterações:
```git
git reset --hard <commit>
```
Cuidado ao usar o --hard, se já foi publicado no repositório remoto não se deve usá-lo.

## Conflitos
- Acontecem ao unirmos alterações;
- Quando versões diferentes possuem as mesmas linhas nos mesmos arquivos editadas diferentes;
- O git identifica os conflitos e fica aguardando a solução;
- Ao resolver os conflitos deve ser feito um commit;

- Para resolver o conflito é preciso dar um `git pull` , resolver os conflitos apontados pelo git e commitar as alterações.

## Branching
- É uma lista de commits
- Representa ramificações no repositório
- Listar as branchs do repositório:
```
git branch
```
- Criar uma nova branch:
```
git branch <nova_branch>
```

- Exclui uma branch:
```
git branch -d <branch>
```

- Acessar a branch:
```
git checkout <branch>
```
Seu repositório passar a ter os commits da branch e novos commits serão adicionados a ela.

## Merge
- Aplica os commits de uma branch na branch atual;
- Encontra um commit comum entre as branchs e aplica todos os commits que a atual não possui;
- Caso existam commits na atual que não estão na outra, será criado um commit de merge.
- Comando:
```
git merge <branch>
```

## Rebase
- Semelhante ao merge, porém difere na ordem de aplicar os commits;
- No rebase os commits na frente da base são removidos temporariamente, os commits da branch são adicionados e por fim os da branch atual são adicionados um a um.
- Podem acontecer conflitos que serão removidos para cada commit.
- Comando:
```
git rebase <branch>
```

## Fetch
- Baixa as atualizações do remote porém não aplica no repositório;
- Permite fazer o rebase de uma branch em vez de fazer o merge;
- `pull = fetch + merge` 
- fetch e rebase é melhor para manter histórico de desenvolvimento.
- Comando:
```
git fetch
```

## Tags
- Útil para definir versões estáveis do projeto;
- Semelhante a branch porém não recebe mais commits;
- Guarda um estado do repositório;
- Comando:
```
git tag [nome da tag]
```

```
git push <remote> <tag>
```

## Commit amend
- Altera a mensagem do último commit;
- Adiciona arquivos ao último commit
- Comando:
```
git commit --amend
```

## Git stash
- Guarda as alterações do working directory:
```
git stash
```
- Permite fazer rebase, merge, trocar de branch sem a necessidade de fazer um commit:
```
git stash list
```

- Aplica o último stash armazenado:
```
git stash pop
```  