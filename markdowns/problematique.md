# introduction

Imaginons, nous avons un objet ayant de nombreux attribut.

exemple simple:
    Pizza(String pate, String sauce, String contenu)
    
Notre objectif est d'instancier plusieurs fois cette classe Pizza. Comment faire?

- solution 1 : copier-coller
``` java
Pizza pizzaHawaienne1 = new Pizza("moelleuse", "douce", "jambon+ananas");
Pizza pizzaHawaienne2 = new Pizza("moelleuse", "douce", "jambon+ananas");

Pizza pizzaNorvegienne1 = new Pizza("cuite", "huile d'olive", "saumon+mozzarella");
Pizza pizzaNorvegienne2 = new Pizza("cuite", "huile d'olive", "saumon+mozzarella");
Pizza pizzaNorvegienne3 = new Pizza("cuite", "huile d'olive", "saumon+mozzarella");
```

On comprend assez rapidement le problème ici.

- solution 2 : la bonne méthode !!

    **le design pattern builder**
