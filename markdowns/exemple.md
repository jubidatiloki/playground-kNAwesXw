# Exemple de la pizzeria

Supposons le cas suivant d'une pizzéria, ou il existe plusieurs sorte de pizzas(chaque pizza ayant des ingrédients différents).

![diagramme de classe pizza](https://raw.githubusercontent.com/jubidatiloki/playground-kNAwesXw/master/class_diagram_pizza.png)


# 1. class produit

On commence par créer une class produit, ici pizza, qui sera l'élément que l'on voudra créer par la suite.

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
    
    @Override
	public String toString() {
		return "Pizza [pate=" + pate + ", sauce=" + sauce + ", contenu=" + contenu + "]";
	}
}
```  

# 2. class builder abstrait 

On crée ensuite une classe abstraite, pizzaBuilder, qui permettra de créer différentes sortes de pizza sans avoir besoin de redefinir les attributs de chacune.

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

# 3.  builder concret 

On crée donc plusieurs classes héritant de pizzaBuilder, qui permettent donc de définir les différents type de pizza et donc les ingrédients(pâte, sauce, contenu) les constituants.


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


# 4. class directeur 

On crée ensuite une classe directeur, serveur ici. Cette classe permettra de construire les différentes sorte de pizza.

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


# application

 client commandant une pizza. 
``` java runnable 
// class Pizza { autofold
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
    @Override
	public String toString() {
		return "Pizza [pate=" + pate + ", sauce=" + sauce + ", contenu=" + contenu + "]";
	}
}
// }
// class PizzaBuilder { autofold
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
// }
// class PizzaHawaienneBuilder { autofold
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
// }
// class PizzaNorvegienneBuilder { autofold
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
// }
// class Serveur { autofold
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
// }

public class Main{ // on remplace le nom par Main pour pouvoir etre exécutable sur tech.io
     static public void main(String[] args){
   
        Serveur serveur = new Serveur();
        PizzaBuilder pizzaHawaienneBuilder = new PizzaHawaienneBuilder();
        PizzaBuilder pizzaNorvegienneBuilder = new PizzaNorvegienneBuilder();

        serveur.setPizzaBuilder( pizzaHawaienneBuilder);
        serveur.constructPizza();

        Pizza pizza = serveur.getPizza();
        System.out.println(pizza);
        
        serveur.setPizzaBuilder( pizzaNorvegienneBuilder);
        serveur.constructPizza();

        pizza = serveur.getPizza();
        System.out.println(pizza);
    }
}
```  

