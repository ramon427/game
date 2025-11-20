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

export class digitCode extends Item implements Pickup, Search, Examine {

    public constructor() {
        super(digitCodeAlias, PickUpActionAlias, SearchActionAlias, ExamineActionAlias);
    }

    public name(): string {
        return "4-Digit Code";
    }
}
```
De GameObject class is een abstract class en de basis voor alle GameObjecten in de game. Item is ook een abstract class en overerft alle methodes en eigenschappen van class GameObject. digitCode class overerft de abstract class Item die ook weer GameObject overerft. digitCode class is dus een uitbreiding van Item (en gameObject). Het doel van abstraction is om alleen de belangrijke eigenschappen etc te tonen. Een abstract class is er gewoon als basis voor subclasses. Abstraction is het alleen meegeven van de belangrijke eigenschappen aan een class / object. Bijvoorbeeld met inheritance kan je die eigenschappen overerven en daar weer andere eigenschappen aan toevoegen.

### Encapsulation
```typescript
export class digitCode extends Item implements Pickup, Search, Examine {

    public constructor() {
        super(digitCodeAlias, PickUpActionAlias, SearchActionAlias, ExamineActionAlias);
    }

    public name(): string {
        return "4-Digit Code";
    }
}
```
hier gebruik ik encapsulation. public constructor en public name. Ze zijn public zodat ze buiten de klasse ook gebruikt kunnen worden. De 4 digit code heb ik nodig in andere bestanden vandaar dat ze direct op public staan. Encapsulation is eigenlijk het openbare , beschermen of prive zetten van een object.

### Inheritance
```typescript
export class digitCode extends Item implements Pickup, Search, Examine {}
```
 Er staat DigitCode extends Item, dat betekent dat de class digitCode van de klasse Item alle eigenschappen en methodes overerft en uitbreidt met eigen eigenschappen. ( Item overerft weer GameObject dus indirect erft digitCode die eigenschappen ook over.)

 ### super en constructor 
 De constructor methode in de digitCode klasse wordt gebruikt om een nieuw object van de digitCode klasse te maken wanneer deze wordt aangeroepen.

 Omdat ik wil dat de class pickup search en examine impelenteert, moet je die aliassen in de super zetten. deze worden doorgegeven aan de constructer van de super class Item.

## Als student wil ik leren hoe ik het OO-principe polymorfisme toepas in mijn code 
```typescript
export const InspectActionAlias: string = "inspect";

export interface Inspect {
    inspect(): ActionResult | undefined;
}

export class InspectAction extends Action{
    public constructor(){
        super(InspectActionAlias, "Inspect", true);
    }

    public static handle(gameObject: GameObject): ActionResult | undefined {
        if (implementsInterface(gameObject, InspectActionAlias)) {
            return castTo<Inspect>(gameObject).inspect();
        }
        return undefined;
    }
}
```

De Inspect interface definieert een methode inspect(), en de handle methode in de InspectAction klasse maakt gebruik van deze interface. Hierdoor kunnen verschillende klassen die de Inspect interface implementeren, hun eigen specifieke implementatie van de inspect() methode hebben. Dus als ik nu in twee andere bestanden onder een class de inspect methode aanroep kan ik ze beiden iets anders laten returnen.

## Als student wil ik leren hoe ik abstracte classes toepas in mijn code 
Een abstracte class is eigenlijk de basis voor andere objecten van subclasses. Een abstractt class geeft de gemeenschappelijke kenmerken weer. Dus bijvoorbeeld van een auto kan je merk, model, jaar, prijs. Elke auto heeft die eigenschappen.

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

export const InspectActionAlias: string = "inspect";

export interface Inspect {
    inspect(): ActionResult | undefined;
}

export class InspectAction extends Action{
    public constructor(){
        super(InspectActionAlias, "Inspect", true);
    }

    public static handle(gameObject: GameObject): ActionResult | undefined {
        if (implementsInterface(gameObject, InspectActionAlias)) {
            return castTo<Inspect>(gameObject).inspect();
        }
        return undefined;
    }
}
```
De static is public en accepteert een parameter: GameObject die een ActionResult of undefined returned. Daarna wordt er gecontroleerd of het GameObject de interface van de alias implementeert.

In het voorbeeld van de SearchAction-klasse wordt de handle-methode gedeclareerd als static. Hierdoor kan de methode direct worden aangeroepen op de klasse zelf, zonder dat je een instantie van SearchAction hoeft te maken. Je hoeft niet telkens 

Als het gameObject de interface implementeert, wordt de castTo-functie gebruikt om het gameObject te casten naar het type Inspect. Vervolgens wordt de inspect()-methode aangeroepen op het gecastte object. Je hoeft niet voor elke methode.functie een aparte cast to functie aan te maken. Je hoeft niet telkens new masterkeyitem bijvoorbeeld te coderen.

```typescript
export class DeskRoom extends Room implements Inspect, Pickup, Break{
    public constructor() {
        super(DeskRoomAlias, InspectActionAlias, PickUpActionAlias, BreakActionAlias);
    }
    public name(): string {
        return "Desk";
    }
}
```
In een ander bestand heb ik dus een andere class de Inspect( methode /interface) laten implementeren zodat ik hier de functie kan gebruiken.

Interfaces daarentegen specificeren een set methoden die een klasse moet implementeren, maar bevatten geen implementatie zelf.

## Als student wil ik leren wat generics zijn en hoe ik ze gebruik in mijn code 

```typescript


public static handle(gameObject: GameObject): ActionResult | undefined {
        if (implementsInterface(gameObject, GoToActionAlias)) {
            return castTo<GoTo>(gameObject).goto();
        }
}
```

generics je hoeft niet de hele tijd nieuwe functies te maken. De goto kan ik nu gewoon gebruiken in verschillende classes.

## Dat je een UML class-diagram hebt gemaakt van jouw kamer.

![UML Class HotelLobby](<HotelLobby uml class.jpeg>)
