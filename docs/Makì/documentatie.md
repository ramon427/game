## Learing Stories
1. Als student wil ik leren hoe ik de OO-Principes abstraction, encapsulation en inheritance toepas in mijn code.
2. Als student wil ik leren hoe ik de basis van web components toepas in mijn code.
3. Als student wil ik leren hoe ik interfaces toepas in mijn code.

## OOP
hotelroomcard4.ts

```typescript
export const HotelRoomCard4Alias: string = "hotelroomcard4";

export class HotelRoomCard4 extends Item implements Obtain {
    public constructor() {
        super(HotelRoomCard4Alias,ObtainAlias);
    }
    public name(): string {
        return "HotelRoomCard4";
    }
    public obtain(): ActionResult | undefined {
        return new TextActionResult(["You received HotelRoomCard4 from the Employee"]);
    }
}
```
abstraction: wordt hier niet gebruikt.
inheritance: extends Item -> erft over.
encapsulation: public obtain -> die textactionresult kan nu dus in een ander bestand opgeroepen worden.

## Web Components

``` typescript

        .header img {
            width: 100%;
            height: 500px;
            image-rendering: pixelated;
        }
```

Hier wordt in ts css toegepast. Ik heb de height aangepast zodat de afbeelding goed op het scherm zichtbaar is.

## Dialoog

``` Typescript
public talk(choiceId?: number | undefined): ActionResult | undefined {
        if (choiceId === 1) {
            return new TalkActionResult(this, ["OMG! I saw a man leave with a woman in his arms.... I think they went to room 3 or 4..."], [new TalkChoiceAction(2, "I can't believe this, what was she wearing ?"), new TalkChoiceAction(3, "I am going to knock down the doors now!!")]);

        } else if (choiceId === 2) {
            return new TalkActionResult(this, ["She had a Black Q TrackSuit on and Jordan 4's. "], [new TalkChoiceAction(4, "Give me the cards now!!!!!!"), new TalkChoiceAction(5, "That's def my girl, I need the hotelcards to the rooms, can you give it to me please.. I will only ask it one time nicely...")]);

        } else if (choiceId === 3) {
            return new TalkActionResult(this, ["The security was called... GAME OVER."], [new TalkChoiceAction(6, "game over")]);
            // game over
        } else if (choiceId === 6) {
            return this.custom("start-over");

        } else if (choiceId === 4) {
            return new TalkActionResult(this, ["The security was called... GAME OVER."], [new TalkChoiceAction(7, "game over")]);
        }
        // game over
        else if (choiceId === 7) {
            return this.custom("start-over");
        }

        else if (choiceId === 5) {
            return new TalkActionResult(this, ["Yes I want to help you find your girlfriend!", "", "I can only give you one hotelroomcard, which one do you want ?"], [new TalkChoiceAction(8, "Card 3"), new TalkChoiceAction(9, "Card4")]);
        }
        else if (choiceId === 9) {
            const card4ObtainResult: ActionResult | undefined = ObtainAction.handle(new HotelRoomCard4());
            return card4ObtainResult;
        }

        // return standard text & choice
        return new TalkActionResult(this, ["Hello, how can I help you?"], [new TalkChoiceAction(1, "Hey, My girlfriend is missing, did you saw her leavee Hotel Room 2 around 10 minutes ago?")]);
    }
```

laatste regel codes is de standaard waarde die gegeven worden. De else if codes zijn mogelijkheden die aan de hand van je keuzes voortzetten. 
