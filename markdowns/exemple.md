# Exemple de la pizzeria

Supposons le cas suivant d'une pizzéria, ou il existe plusieurs sorte de pizzas(chaque pizza ayant des ingrédients différents).

![diagramme de classe pizza](https://github.com/jubidatiloki/playground-kNAwesXw/edit/master/class_diagram_pizza.png)


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
    
    @Override
	public String toString() {
		return "Pizza [pate=" + pate + ", sauce=" + sauce + ", contenu=" + contenu + "]";
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

