Ce que UNISIS doit retenir de UseR 2019!
================

-   [Il est possible d’améliorer son utilisation de RStudio à l’aide d’addins](#il-est-possible-daméliorer-son-utilisation-de-rstudio-à-laide-daddins)
    -   [Utiliser rstudioapi comme base](#utiliser-rstudioapi-comme-base)
    -   [Faire un addin](#faire-un-addin)
-   [Il est possible de traiter des objets sur R avec Python et viceversa.](#il-est-possible-de-traiter-des-objets-sur-r-avec-python-et-viceversa.)

<!-- README.md is generated from README.Rmd. Please edit that file -->
![](images/Toulouse.jpg)

Il est possible d’améliorer son utilisation de RStudio à l’aide d’addins
------------------------------------------------------------------------

![](images/remedy_example.gif)

<font size="2">*Exemple avec le package remedy développé pour rapprocher R markdown de Word.*</font>

### Utiliser rstudioapi comme base

Pour créer des addins de ce type sur Rstudio on peut utiliser le package `rstudioapi`

Ce package permets d'utiliser l'api de Rstudio pour :

1 - Manipuler des documents.

-   `documentNew()`
-   `documentSave()`
-   `document_range()`, `modify_range()` & `insertText(range, text, id)` : un range est la position du texte dans un document R Studio.

![](images/position.png)

Exemple : créer une fonction qui rajoute un préfixe et suffixe a n'importe quel texte qui soit sélectionné sur RStudio. Ensuite, créer une fonction à partir de la précédente pour que mettre du texte en italique sur R Markdown.

``` r
enclose <- function(prefix, postfix = prefix) {
  # Get the context of the Editor
  a <- rstudioapi::getSourceEditorContext()
  # a$selection is a list refering to the selected text
  for (s in a$selection) {
    rstudioapi::insertText(
      location = s$range,
      text = 
        sprintf(
          "%s%s%s",
          prefix,
          s$text,
          postfix
        )
    )
  }
}
italicsr <- function() enclose("_")
```

2- Créer des dialogues avec RStudio

-   `selectFile()` & `selectDirectory()`
-   `askForPassword()`
-   `showDialog()`. Exemple : `showDialog(title = "Test", message = "ceci est un test")`

3- Jouer avec le terminal

-   `terminalCreate()`
-   `terminalExecute()`
-   `terminalKill()`

<span style="color:red"> Attention! `rstudioapi`dépends de fonctions internes à RStudio et donc est intimement lié à la version de RStudio.</span>

### Faire un addin

-   Un addin est un package, donc il faut créer un package
-   Créer une fonction
-   Exécuter `usethis::use_addin()`
-   Compléter les `addins.dfc`
-   Cliquer sur install and restart

Autre exemple d'addin : datapasta (réduit la résistance associée au copy + paste vers R)

![](images/datapasta.gif)

*Plus d'informations sur :* <https://github.com/ColinFay/user2019workshop>

Il est possible de traiter des objets sur R avec Python et viceversa.
---------------------------------------------------------------------

A l'aide du package `reticulate` , R Studio 1.2 et Anaconda 3 on peut combiner les deux langages de programmation sur le même script R.

Utiliser `reticulate::use_python()` pour spécifier la version de python sur laquelle on veux travailler (et qui se trouve sur l'ordinateur).

La fonction `repl_python()` crée un console Python interactive sur R. Les objects crés sur Python sont disponibles sur R et viceversa.

![](images/python.png)

Les objets crées sur python ne s'affichent pas dans l'onglet environnement mais ce trouvent bien là.

*Plus d'informations sur :*

-   <https://github.com/3mmaRand/useR2019_tutorial>
-   <https://3mmarand.github.io/useR2019_tutorial/#1>
