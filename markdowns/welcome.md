# Bienvenue

Nous allons vous présenter le design pattern builder. Tout d'abord commençons par définir ce qu'est un design pattern.


# Un Design pattern, Quézako ?

Un design pattern est un modèle de conception permettant de simplifier des problèmes couramment rencontrés lors du développement d'applications.
On peut les séparer en 3 catégories:
- les modèles de création, qui permettent de déléguer à d'autres classes la construction d'objet.
- les modèles de structuration, qui tendent à concevoir un regroupement de classes avec des macro-composants.
- les modèles de comportement, qui tentent de répartir les responsbilités entre chaque classe.
  
Maintenant que nous avons défini ce qu'est un design pattern, revenons à notre design pattern builder.


# Pattern Builder

# Le builderzer 
Le builder est un design pattern appartenant à la catégorie des modèles de création.
Il sert donc à créer des objets d'une autre classe et il possede la plupart du temps les différentes variables de la classe qu'il crée.

Ainsi lors de la création d'un nouvel objet de la classe, les paramètres sont directement insérés sans avoir besoin de les renseignés. Pour faire simple, 
il sert a rendre le code plus lisible et mieux organisé. Un exemple vaut mieux qu'un long discours, place à la démo.



# Exemple de la pizzeria

Supposons le cas suivant d'une pizzéria, ou il existe plusieurs sorte de pizzas(chaque pizza ayant des ingrédients différents).

 produit 
``` java 
class Pizza {
    private String pate = "";
    private String sauce = "";
    private String contenu = "";

    public void setPate(String pate){
        this.pate = pate;
    }

    public void setSauce(String sauce) {
        this.sauce = sauce;
    }

    public void setContenu(String contenu) {
        this.contenu = contenu;
    }
}
```  
On a donc une classe pizza, qui est défini par des attributs pate, sauce et contenu.


 builder abstrait 
``` java
abstract class PizzaBuilder {
    protected Pizza pizza;

    public Pizza getPizza() {
        return pizza;
    }

    public void createNewPizzaProduct() {
        pizza = new Pizza();
    }

    public abstract void buildPate();
    public abstract void buildSauce();
    public abstract void buildContenu();
}
```  

On crée ensuite une classe abstraite, pizzaBuilder, qui permettra de créer différentes sortes de pizza sans avoir besoin de redefinir les attributs de chacune.



 builder concret 
``` java    
class PizzaHawaienneBuilder extends PizzaBuilder {
    public void buildPate() {
        pizza.setPate("moelleuse");
    }

    public void buildSauce() {
        pizza.setSauce("douce");
    }

    public void buildContenu() {
        pizza.setContenu("jambon+ananas");
    }
}
```  
 builder concret 
``` java
class PizzaNorvegienneBuilder extends PizzaBuilder {
    public void buildPate() {
        pizza.setPate("pate cuite");
    }

    public void buildSauce() {
        pizza.setSauce("huile d'olive");
    }

    public void buildContenu() {
        pizza.setContenu("saumon+mozzarella");
    }
}
```  

On crée donc plusieurs classes héritant de pizzaBuilder, et qui permettent donc de définir les différents attributs constituant chaque pizza.



 Directeur 
``` java 
class Serveur{
    private PizzaBuilder pizzaBuilder;

    public void setPizzaBuilder(PizzaBuilder pb) {
        pizzaBuilder = pb;
    }

    public Pizza getPizza() {
        return pizzaBuilder.getPizza();
    }

    public void constructPizza() {
        pizzaBuilder.createNewPizzaProduct();
        pizzaBuilder.buildPate();
        pizzaBuilder.buildSauce();
        pizzaBuilder.buildContenu();
    }
}
```  
On crée ensuite une classe serveur, que l'on appelle directeur, ca sera cette classe qui permettra de construire les différentes sorte de pizza.



 client commandant une pizza. 
``` java runnable 
  public class Pizza {
    private String pate = "";
    private String sauce = "";
    private String contenu = "";

    public void setPate(String pate){
        this.pate = pate;
    }

    public void setSauce(String sauce) {
        this.sauce = sauce;
    }

    public void setContenu(String contenu) {
        this.contenu = contenu;
    }
}
public abstract class PizzaBuilder {
    protected Pizza pizza;

    public Pizza getPizza() {
        return pizza;
    }

    public void createNewPizzaProduct() {
        pizza = new Pizza();
    }

    public abstract void buildPate();
    public abstract void buildSauce();
    public abstract void buildContenu();
}
public class PizzaHawaienneBuilder extends PizzaBuilder {
    public void buildPate() {
        pizza.setPate("moelleuse");
    }

    public void buildSauce() {
        pizza.setSauce("douce");
    }

    public void buildContenu() {
        pizza.setContenu("jambon+ananas");
    }
}
  
public class PizzaNorvegienneBuilder extends PizzaBuilder {
    public void buildPate() {
        pizza.setPate("pate cuite");
    }

    public void buildSauce() {
        pizza.setSauce("huile d'olive");
    }

    public void buildContenu() {
        pizza.setContenu("saumon+mozzarella");
    }
}
public class Serveur{
    private PizzaBuilder pizzaBuilder;

    public void setPizzaBuilder(PizzaBuilder pb) {
        pizzaBuilder = pb;
    }

    public Pizza getPizza() {
        return pizzaBuilder.getPizza();
    }

    public void constructPizza() {
        pizzaBuilder.createNewPizzaProduct();
        pizzaBuilder.buildPate();
        pizzaBuilder.buildSauce();
        pizzaBuilder.buildContenu();
    }
}

    public static void main(String[] args){
        Serveur serveur = new Serveur();
        PizzaBuilder pizzaHawaienneBuilder = new PizzaHawaienneBuilder();
        PizzaBuilder pizzaNorvegienneBuilder = new PizzaNorvegienneBuilder();

        serveur.setPizzaBuilder( pizzaHawaienneBuilder);
        serveur.constructPizza();

        Pizza pizza = serveur.getPizza();
    }

```  


::: Source

https://fr.wikipedia.org/wiki/Monteur_(patron_de_conception)

https://blog.xebia.fr/2016/12/28/design-pattern-builder-et-builder-sont-dans-un-bateau/

https://sourcemaking.com/design_patterns/builder

https://sourcemaking.com/design_patterns/builder/java/2

:::



# QCM

?[A quoi sert un design pattern?]
-[ ] à avoir une représentation graphique d'une classe
-[x] à résoudre plus simplement des problèmes rencontrés lors de la phase de developpement
-[ ] à faire parler les curieux

?[Le design pattern builder fait partie de la catégorie des design pattern de:]
-[x] création
-[ ] structuration
-[ ] comportement

?[Le builder sert à créer des objet de sa propre classe.]
-[ ] VRAI
-[x] FAUX

?[Lors de la création d'un nouvel objet à l'aide du builder, il faut renseigner les paramètres de la classe.]
-[ ] VRAI
-[x] FAUX

?[Quel est l'avantage principal du builder?]
-[ ] gagner du temps
-[x] avoir un code propre et plus lisible
-[ ] l'ergonomie
-[ ] l'I.A.

---
Merci d'avoir suivi cette petite présentation, nous espèrons qu'elle vous aura plu.


