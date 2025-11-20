## Als student wil ik leren hoe ik de OO-principes abstraction, encapsulation en inheritance toepas in mijn code.

### Abstraction & Inheritance & Als student wil ik leren hoe ik abstracte classes toepas in mijn code 
Subclass wordt gemaakt door de super class room te extenden, en erft de functies. (inheritance met een abstract class)

```typescript
/**
 * Hotel room to get the wallet and fire extuinguisher
 */
export class HotelTwoRoom extends Room {
    /**
     * Create a new instance of this room + call the super constructor
     */
    public constructor() {
        super(HotelTwoRoomAlias);
    }

    /**
     * Switch room
     *
     * @returns Success feedback to switching room
     */
    public goto(): ActionResult | undefined {
        getPlayerSession().currentRoom = this.alias;
        return new TextActionResult(["You have now entered " + this.name()]);
    }
    ...
}
```
Verberging van complexe systemen door een class (abstraction)
````typescript
    case HotelTwoRoomAlias:
        return new HotelTwoRoom();
````

### Encapsulation
Interne werking kan gewijzigd worden zonder invloed op andere delen

```typescript
    private roomName: string = "Room 2";

    public name(): string {
        return this.roomName;
    }
```



## Als student wil ik leren hoe ik het OO-principe polymorfisme toepas in mijn code
## Als student wil ik leren hoe ik interfaces toepas in mijn code 

Open functie kan geimplementeerd worden door verschillende items, het moet geimplementeerd worden. 
Je zou dus een functie kunnen maken die als paramter Open heeft waardoor je items kan openen met verschillende open functies, zonder de bepaalde sub class te gebruiken in de functie (Alleen om te passeren).

```typescript
/**
 * Interface for GameObjects that need to support an open action
 */
export interface Open {
    /**
     * Execute open action
     *
     * @returns Result of the open action
     */
    open(): ActionResult | undefined;
}
```

```typescript
/**
* Implemented open function so you can open the laptop
* It checks if the player has the required finger print item
*
 * @returns Switch to laptop room || Finger print does not match
*/
public open(): ActionResult | undefined {
    const inventory: string[] = getPlayerSession().inventory;

    if (!inventory.includes(FingerPrintItemAlias)) {
        return new TextActionResult(["Your finger print does not match."]);
    } else {
        const room: LaptopRoom = new LaptopRoom();
        getPlayerSession().currentRoom = room.alias;

        return room.examine();
    }
}
```

## Als student wil ik leren hoe ik static functies en variabelen gebruik in mijn code 
## Als student wil ik leren wat generics zijn en hoe ik ze gebruik in mijn code

Static functies zodat je geen instantie nodig hebt om de functie aan te roepen, omdat je geen open action class instantie wilt aanmaken. Je wilt alleen de interface functie aan roepen.

Ook wordt hier gebruik gemaakt van generics zodat we niet een functie moet maken voor elk type.
voorbeeld:
castToInteger
castToString
Nu kunnen we castTo gebruiken en de type doorgeven tussen de <>
Zoals bij een Java Hashmap

```typescript
/**
* Handle the open action, static function, no instance needed
* Typescript can't cast to something it's not sure about
*
* @param gameObjects GameObject on which the open action should be executed.
*
* @returns Result of the action
*/
public static handle(gameObject: GameObject): ActionResult | undefined {
    if (implementsInterface(gameObject, OpenActionAlias)) {
        return castTo<Open>(gameObject).open();
    }

    return undefined;
}
```

