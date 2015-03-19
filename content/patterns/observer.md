+++
date = "2015-03-19T10:07:40-06:00"
draft = true
title = "The Observer Pattern"

+++

## ELI5

It is close to dinner time, and you're hungry. Mommy or Daddy is cooking
dinner. You want to make sure that you know dinner is ready as soon as it's
ready. Would you walk into the kitchen every 5 minutes and ask Mommy/Daddy if
dinner is ready? Or, would you ask Mommy/Daddy to let you know when dinner's
ready? That way, you can do other things, like playing or watching a cartoon.
When dinner is ready, you'll be told so, and until then, you don't have to
think about it, except when you're tummy reminds you.

The *Observer* pattern is shown in this, because you asked your parent to tell
you when something that you care about (dinner) has changed its state (it's
ready to be eaten).

## Code Samples

### Java

{{< highlight java >}}
public class MealCooker {
  private List<Observer> observers = new ArrayList<Observer>();

  public void addObserver(Observer observer) {
    observers.add(observer);
  }

  public void cookMeal() {
    // prepareIngredients();
    // allowToCool();

    for (Observer observer : observers) {
      observer.notifyMealReady();
    }
  }
}

public interface Observer {
  public void notifyMealReady();
}

public class Child implements Observer {
  private MealCooker parent;

  public void setMealCooker(MealCooker inCooker) {
    parent = inCooker;
  }

  public void whenHungry() {
    parent.addObserver(this);
  }

  public void notifyMealReady() {
    // washUp();
    // comeToTable();
    // eat()
  }
}
{{< /highlight >}}

### Javascript (ES6)

{{< highlight javascript >}}
let hungryChildren = []

class Parent {
  constructor(name) {
    this.name = name
  }

  cookMeal() {
    // prepareIngredients()
    // allowToCool()
    console.log(`${this.name} cooked a meal!`)
    hungryChildren.forEach((kid) => kid.notifyMealReady())
    hungryChildren = []
  }
}

class Child {
  constructor(name) {
    this.name = name
  }

  isHungry() {
    hungryChildren.push(this)
    console.log(`${this.name} is hungry!`)
  }

  notifyMealReady() {
    // washUp()
    // comeToTable()
    // eat()
    console.log(`${this.name} has been fed!`)
  }
}

let mommy = new Parent('Mommy')
let daddy = new Parent('Daddy')

let joey = new Child('Joey')
let jimmy = new Child('Jimmy')
let johnny = new Child('Johnny')

joey.isHungry()   // "Joey is hungry!"
johnny.isHungry() // "Johnny is hungry!"
daddy.cookMeal()  // "Daddy cooked a meal!"
// "Joey has been fed!"
// "Johnny has been fed!"

jimmy.isHungry() // "Jimmy is hungry!"
mommy.cookMeal() // "Mommy cooked a meal!"
// "Jimmy has been fed!"
{{< /highlight >}}

[View this example on JS Bin](//jsbin.com/hagicuquru/1/edit?js,console)

### Go

{{< highlight go >}}
package main

import "fmt"

var hungryChildren = []Child{}

type Parent struct {
  name string
}

func (p Parent) cookMeal() {
  // prepareIngredients()
  // allowToCool()
  fmt.Printf("%s cooked a meal!\n", p.name)
  for _, child := range hungryChildren {
    child.notifyMealReady()
  }
  hungryChildren = []Child{}
}

type Child struct {
  name string
}

func (c Child) isHungry() {
  hungryChildren = append(hungryChildren, c)
  fmt.Printf("%s is hungry!\n", c.name)
}

func (c Child) notifyMealReady() {
  // washUp()
  // comeToTable()
  // eat()
  fmt.Printf("%s has been fed!\n", c.name)
}

func main() {
  mommy := Parent{"Mommy"}
  daddy := Parent{"Daddy"}

  joey := Child{"Joey"}
  jimmy := Child{"Jimmy"}
  johnny := Child{"Johnny"}

  joey.isHungry()   // "Joey is hungry!"
  johnny.isHungry() // "Johnny is hungry!"
  daddy.cookMeal()  // "Daddy cooked a meal!"
  // "Joey has been fed!"
  // "Johnny has been fed!"

  jimmy.isHungry() // "Jimmy is hungry!"
  mommy.cookMeal() // "Mommy cooked a meal!"
  // "Johnny has been fed!"
}
{{< /highlight >}}

[View this example on the Go Playground](https://play.golang.org/p/Fu__abGi5U)

## Explanation

The `MealCooker` object keeps track of a list of `Observer` objects. When it is
done performing its long `cookMeal` function, it spins through each `Observer`
object and notifies it.
