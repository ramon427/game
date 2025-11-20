## Als student wil ik leren hoe ik de OO-principes abstraction, encapsulation en inheritance toepas in mijn code. 

### Abstraction

```typescript
export abstract class GameObject implements HasInterfaces {
    private _alias: string;
    private _interfaces: string[];

}

export abstract class Item extends GameObject {
    //Do nothing
}

export class freePass extends Item implements Obtain {
    public constructor() {
        super(freePassAlias,ObtainAlias);
    }
    public name(): string {
        return "freePass";
    }
```
De GameObject-class vormt de abstracte basis voor alle objecten in het spel. Item is ook een abstracte klasse en erft alle methoden en eigenschappen van de GameObject-klasse over. freePass overerft de abstract class Item die ook weer GameObject overerft. Deze maakt een uitbreiding van Item (en dus ook van GameObject). Abstraction is er meer voor de belangrijke dingen. Een abstracte klasse is als basis voor subclasses en biedt alleen de meest relevante kenmerken.  Abstraction is het alleen meegeven van de belangrijke eigenschappen aan een class / object.

### Encapsulation

Bij de code hierboven gebruik ik encapsulation, public constructor en public name. Ze zijn public zodat ze buiten de klasse ook gebruikt kunnen worden. De freePass heb ik nodig in andere bestanden vandaar dat ze direct op public staan. Encapsulation is in een korte zin het beschermen van een object

### Inheritance
```typescript
export class freePass extends Item implements Obtain 
```
 "freePass extends Item". dat betekent dat de class freepass van de item class alle eigenschappen en methodes overerft en uitbreidt met eigen eigenschappen. 

 ### super en constructor 
 De constructor methode in de digitCode klasse wordt gebruikt om een nieuw object van de class te maken wanneer het wordt aangeroepen.

 Omdat ik wil dat de class obtain impelenteert, moet je die alias in de super zetten. deze worden doorgegeven aan de constructer van de super class Item.

## Als student wil ik leren hoe ik het OO-principe polymorfisme toepas in mijn code 
```typescript
/** Alias used to identity the Examine action and interface */
export const ExamineActionAlias: string = "examine";

/**
 * Interface for GameObjects that need to support the Examine action
 */
export interface Examine {
    /**
     * Execute the Examine action
     * 
     * @returns Result of the Examine action
     */
    examine(): ActionResult | undefined;
}

/**
 * Class used to represent the Examine action
 */
export class ExamineAction extends Action {
    /**
     * Create a new instance of the Examine action
     */
    public constructor() {
        super(ExamineActionAlias, "Examine", true);
    }

    /**
     * Handle the Examine action
     *
     * @param gameObject Reference to the GameObject on which the Examine action should be executed
     *
     * @returns Result of the action
     */
    public static handle(gameObject: GameObject): ActionResult | undefined {
        if (implementsInterface(gameObject, ExamineActionAlias)) {
            return castTo<Examine>(gameObject).examine();
        }

        return undefined;
    }
}
```

De examine interface definieert een methode examine(), en de handle methode in de examineAction class maakt gebruik van deze interface. Hierdoor kunnen verschillende klassen die de interface implementeren, hun eigen specifieke implementatie van de inspect() methode hebben. 

## Als student wil ik leren hoe ik abstracte classes toepas in mijn code 
Een abstracte class is de basis voor andere objecten van subclasses. Een abstractt class geeft de gemeenschappelijke kenmerken weer. Dus bijvoorbeeld van een persoon, geeft het de persoonseigenschappen zoals gezicht, huidskleur, haar weer.

```Typescript

/**
 * Base class used to represent a game object
 */
export abstract class GameObject implements HasInterfaces {
    private _alias: string;
    private _interfaces: string[];

    /**
     * Create a new instance of this game object
     * 
     * @param alias Alias of this game object
     * @param interfaces List of interfaces this game object implements
     */
    protected constructor(alias: string, ...interfaces: string[]) {
        this._alias = alias;
        this._interfaces = interfaces;
    }

    /**
     * Name of this game object
     */
    public abstract name(): string;

    /**
     * Alias of this game object
     */
    public get alias(): string {
        return this._alias;
    }

    public get interfaces(): string[] {
        return this._interfaces;
    }

    /**
     * Convert this game object into a UI-specific object
     *
     * @returns UI-specific object representing this game object
     */
    public toReference(): GameObjectReference {
        return {
            alias: this._alias,
            name: this.name(),
        };
    }
}

```


## Als student wil ik leren hoe ik static functies en variabelen gebruik in mijn code + Als student wil ik leren hoe ik interfaces toepas in mijn code 

```typescript

/** Alias used to identity the Examine action and interface */
export const ExamineActionAlias: string = "examine";

/**
 * Interface for GameObjects that need to support the Examine action
 */
export interface Examine {
    /**
     * Execute the Examine action
     * 
     * @returns Result of the Examine action
     */
    examine(): ActionResult | undefined;
}

/**
 * Class used to represent the Examine action
 */
export class ExamineAction extends Action {
    /**
     * Create a new instance of the Examine action
     */
    public constructor() {
        super(ExamineActionAlias, "Examine", true);
    }

    /**
     * Handle the Examine action
     *
     * @param gameObject Reference to the GameObject on which the Examine action should be executed
     *
     * @returns Result of the action
     */
    public static handle(gameObject: GameObject): ActionResult | undefined {
        if (implementsInterface(gameObject, ExamineActionAlias)) {
            return castTo<Examine>(gameObject).examine();
        }

        return undefined;
    }
}
```
De static is public en accepteert een parameter: GameObject die een ActionResult of undefined returned. Daarna wordt er gecontroleerd of het GameObject de interface van de alias implementeert.

In het voorbeeld van de SearchAction-klasse wordt de handle-methode gedeclareerd als static. Hierdoor kan de methode direct worden aangeroepen op de klasse zelf, zonder dat je een instantie van SearchAction hoeft te maken. Je hoeft niet telkens 

Als het gameObject de interface implementeert, wordt de castTo-functie gebruikt om het gameObject te casten naar het type Inspect. Vervolgens wordt de inspect()-methode aangeroepen op het gecastte object. Je hoeft niet voor elke methode.functie een aparte cast to functie aan te maken. 



## Als student wil ik leren wat generics zijn en hoe ik ze gebruik in mijn code 

```typescript

    public static handle(gameObject: GameObject): ActionResult | undefined {
        if (implementsInterface(gameObject, cutWireAlias)) {
            return castTo<Cut>(gameObject).cut();
        }
        return undefined;
    }
```

generics je hoeft niet de hele tijd nieuwe functies te maken. cutAction kan ik nu meerdere keren geberuiken.

## Dat je een UML class-diagram hebt gemaakt van jouw kamer.

![Alt text](<uml diagram fitness.drawio.png>)