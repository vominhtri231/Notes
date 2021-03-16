Since Enums are full-fledged class, they could have fields or methods, which better than a bunch of switch-case. Using switch-case with enum could cause problem when the enum change.

``` java
enum Planet {
    Earth(10), Mercury(20), Mars(30);
    
    double mass;
    
    Planet(double mass) {
        this.mass = mass;
    }
}

enum Operation {
    Plus() {
        double apply(double a, double b) {
            return a + b;
        }
    }
    
    Subtract() {
        double apply(double a, double b) {
            return a - b;
        }
    }
        
    abtract double apply(double a, double b);
}
````

One of the disadvantage of associating behaviors enum is code duplication if multiple enum contains have a same behavior. 
This could be solved by **strategy enum**.