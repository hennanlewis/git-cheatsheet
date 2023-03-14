# git-cheatsheet
O objetivo deste repositório é compilar uma lista de comandos do Git que vão além dos essenciais.

## Commit vazio

O primeiro `commit` que em alguns casos pode ser necessário, como em momentos para rebuild de um projeto com CI/CD, é a criação de um `commit` vazio:

```
git commit --allow-empty -m "mensagem do `commit` vazio"
```

Após isso, é necessário apenas um `push` para atualizar o projeto.

## Hard/soft reset
O `hard reset` deve ser usado com autela. Esse comando irá desfazer o último `commit` e descarta todas as alterações contidas nele.
É sempre recomendado fazer um backup do repositório antes de executar um hard reset, usar essa operação apenas em casos extremos, ou usar apenas em casos de commits locais que não foram feitos `push` ainda.

```
git reset --hard HEAD~
```

Perceba que após o `HEAD` há um `~` como parâmetro. Ele indica que o comando desfaz apenas um `commit` e caso queira desfazer mais de um, basta o suvstituir pelo número desejado. Ex.:


```
git reset --hard HEAD2 # Desfaz 2 commits de uma vez
```

O `soft reset` funciona de forma parecida, mas com a diferença de desfazer o último commit, porém mantendo as alterações do código que foram realizadas, e deixando essas alterações prontas para serem recommitadas novamente. Ex.:

```
git reset --soft HEAD~
```

Um número específico de commits também é possível igual ao hard reset, basta substituir o `~` pelo número de commits desejados
