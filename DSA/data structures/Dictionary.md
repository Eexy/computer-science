Un dictionnaire (**Dictionary**) est une structure qui s'inspire des [[Array]]. En effet dans un tableau on peut récupérer un élément avec son index. Dans un dictionnaire pour recréer cela on va associer une clé à un élément.

On peut imaginer cela comme un répertoire de contact où en ayant le nom de la personne on peut récupérer son numéro de téléphone

Les opérations que doit supporter un dictionnaire sont : 
- Search($D,k$) : On renvoi l'élément du dictionnaire $D$ qui possède la clé $k$
- Insert($D,x$): On insert l'élément $x$ dans notre dictionnaire $D$
- Delete($D,x$) : On supprime l'élément $x$ de $D$

On peut créer un dictionnaire avec plusieurs structure comme un [[Array]] en utilisant l'index en tant que clé mais on préféra les [[Hash table]] ou les [[Map]]
