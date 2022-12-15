# Feature-bloat-reduction-system
Une méthode pour prioriser l'exécution des tâches

# Proposition

Une méthode de priorisation permettrait de limiter les bouchons de fonctionnalités en rendant l'exécution du pipe de tâches plus prévisible.

## Methode de priorisation proposée 

La méthode que je propose est inspirée de **[Weighted Shortest Job First] (https://www.scaledagileframework.com/wsjf/)**.
Je l'ai un peu simplifiée, puis j'ai proposé une formule mathématique simple et abordable.

### Métriques prises en compte 

La méthode que je propose s'appuie sur **3 métriques** :
1. La valeur métier de la feature (**Business value**)
* Cette valeur me semble beaucoup plus représentative et d'intérêt que le "_cout du délais_"
*  Cette valeur devrait être fournie par le client
2. La criticité de la feature dans le temps : 
*  On pourra exprimer cette criticité en nombre de jours restant avant livraison 
* Si la feature n'est pas rendue avant la date limite, la valeur du ticket devrait décroitre dans le temps 
3. La taille estimée du ticket 
* Il s'agit de l'estimation du temps nécessaire pour livrer la feature. 
* Cette estimation est relative (et non absolue) à la taille des autres tickets.

### Formule

Appelons **RT** le temps restant avant livraison exprimé en nombre de jours _(Remaining Time)_.

Appelons **SBV** la valeur métier _(statique)_ d'un ticket _(Static Business Value)_
Cette valeur proposée par le client est statique (et ne varie donc pas dans le temps). Pour apprécier cette métrique dans le temps, il faut la corréler avec sa valorisation/dévalorisation dans le temps.

Appelons **TBV** la valeur _temporelle_ d'un ticket _(Temporal Business Value)_. Cette valeur est égale à _**la valeur métier (statique)**_ multipliée par _**l'inverse du nombre de jours restant avant livraison**_

Nous avons donc _**TBV = SBV * 1/RT**_

Appelons **Size**, la taille estimée d'un ticket.

Appelons **Weight**, le poids (valeur d'estimation de la priorité d'un ticket). Le poids est alors égal au rapport de la **valeur du ticket** par **sa taille**

Ainsi nous obtenons : 

**_Weight = TBV / Size_**

Ou de façon étendue : 

**_Weight = SBV / RT * Size_**
