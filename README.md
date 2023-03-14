# git-cheatsheet
O objetivo deste repositório é compilar uma lista de comandos do Git que vão além dos essenciais.

## Commit vazio

O primeiro `commit` que em alguns casos pode ser necessário, como em momentos para rebuild de um projeto com CI/CD, é a criação de um `commit` vazio:

```
git commit --allow-empty -m "mensagem do commit vazio"
```

Após isso, é necessário apenas um `push` para atualizar o projeto.

## Hard/soft reset
O `hard reset` deve ser usado com autela. Esse comando irá desfazer o último `commit` e descarta todas as alterações contidas nele.
É sempre recomendado fazer um backup do repositório antes de executar um hard reset, usar essa operação apenas em casos extremos, ou usar apenas em casos de commits locais que não foram feitos `push` ainda.

```
git reset --hard HEAD~N
```

Perceba que após o `HEAD` há um `~` como parâmetro. Ele indica que o comando desfaz apenas um `commit` e caso queira desfazer mais de um, o parâmetro completo é `HEAD~N`, sendo `N` a quantidade de commits desfeitos. Ex.:


```
git reset --hard HEAD~2
```

O comando acima desfaz completamente os 2 últimos commits de uma vez

O `soft reset` funciona de forma parecida, mas com a diferença de além de desfazer o último commit, mantem as alterações do código que foram realizadas, deixando essas alterações prontas para serem salvas e commitadas novamente. Ex.:

```
git reset --soft HEAD~
```

O comando acima desfaz o último commit, mas registra todas as alterações para serem adicionadas adicionadas ao commit. Um número específico de commits também é possível igual ao hard reset, basta substituir o `N` em `HEAD~N` pelo número de commits desejados.

## Git rebase
Reescreve o histórico de commits em um branch.

Em resumo, o `git rebase` funciona da seguinte maneira:

- Ele busca os commits em comum entre o branch atual e o branch especificado (geralmente a branch master).
- Ele "move" o branch atual para o ponto de divergência entre o branch atual e o branch especificado.
- Ele aplica os commits que não estão no branch atual na ordem em que foram criados, como se tivessem sido feitos em cima do ponto de divergência.
- Ele atualiza a branch atual com as mudanças do rebase.

Como chamada de atenção, antes de escrever o texto a partir deste momento, fiz um commit vazio com a mensagem `Commit inicialmente vazio para ser editado depois` e outro com mensagem `Commit sobre rebase inicial` que possui todo o conteúdo até o texto anterior a este parágrafo. Caso ocorra tudo bem com o teste com o comando `git rebase`, todas as alterações vão para o commit vazio e o `Commit sobre rebase inicial` ficará vazio.

A partir deste momento, devemos seguir os seguinte passos:
1. Insira o comando `git rebase -i HEAD~N`, onde `N` é o número de commits que você deseja editar, ou seja, neste caso é 2;
2. Uma lista de commits será aberta em um editor de texto. Substitua a palavra "pick" pelo comando "edit". Salve e feche o editor.
3. Após fechar o editor, faça as edições necessárias, no caso, colocar o início desse título até os 4 tópicos da lista que explica dos dados sobre o `git rebase`. Caso esteja usando esse texto como material de estudo, faça as alterações desejadas no seu repositório;
4. Insira o comando `git rebase --amend` para registrar as modificações no commit atual, no caso do exemplo, é o commit com a mensagem `Commit inicialmente vazio para ser editado depois`;
5. Aparecerá uma janela com alguns dados e a linha mais acima será a mensagem do commit. Caso queira editá-la, fique a vontade;
6. Caso tenha mudado de pick para edit mais de um commit no passo 2, o comando `git rebase --continue` pulará para o próximo commit marcado como edit. Faça as edições em cada um dos commits, lembrando que para pular ao próximo, basta inserir o comando `git rebase --continue` novamente;
7. Após chegar no último commit a ser editado, insira mais uma vez o comando `git rebase --continue` para indicar que o repositório está pronto para fazer o push dos commits;
8. Caso tenha necessidade de corrigir alguma inconsistência por conta das mudanças, faça o merge adequadamente. Caso apenas queira forçar o push do jeito que está use `git push --force`.

Apos acabar de fazer esses passos, os commits modificados desse repositório ficarão com o mesmo nome de antes da modificação para que utilizar este tutorial como exemplo, então o commit com mensagem `Commit inicialmente vazio para ser editado depois` tera todas as modificações do `Commit sobre rebase inicial` e o `Commit sobre rebase inicial` ficará vazio.