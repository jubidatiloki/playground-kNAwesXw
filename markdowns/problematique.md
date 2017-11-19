# introduction

Imaginons, nous avons un objet complexe ayant de nombreux attribut.

exemple simple:
    Chmilblic(Element eltComplex, Bidule biduleChelou, String nomImprobable, Comportement comportementInattendu)
    
Notre objectif est d'instancier plusieurs fois cette classe Chmilblic. Comment faire?

- solution 1 : copier-coller
```
new Chmilblic(new Element("chassis"), new Bidule("roues"), "prototype de déplacement", new Comportement("roule"));
new Chmilblic(new Element("chassis"), new Bidule("jambes"), "prototype de déplacement", new Comportement("marche"));
new Chmilblic(new Element("chassis"), new Bidule("ailes"), "prototype de déplacement", new Comportement("vole"));
```
