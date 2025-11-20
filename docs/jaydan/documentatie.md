# Technical Documentation


# My room: fitness room.

## Frontend (LS: #17):

For the frontend of my room i did'nt do really much because most of it was already provided. What i did do was implement images for the room.

``` css
/* Image */
    .header img {
            width: 100%;
            height: 500px;
            image-rendering: pixelated;

        }
```
In the "GameCanvas.ts" file i provided the height for the image so that it can fit nicely. 

In my "fitnessRoom.ts" file with this code i added the images. The room itself and a image of a character.

``` typescript
// main images for the room
 public images(): string[] {
        return ["fitnesroom_ai 2","staffmember" ];
    }
```

## Backend (LS: #17, #11):

For this room i added a couple of actions like : "goTo", "goBack" and "Go to locker". "GoTo" and "goBack are mainly for switching rooms. i also got a "locker room" and a "generator room" where you can go to with these buttons.

These are the actions.

``` typescript
// Actions
  public actions(): Action[] {
        return [
            new ExamineAction(), 
            new TalkAction(), 
            new CustomAction("look-around", "Look around", false), 
            new CustomAction("gotootherroom-game", "Go werkend",true),
            new GoAction(),
            new CustomAction("goToLocker", "Go to lockers", false)
        ];
    }
```
And these are for going to the different rooms that i mentioned earlier.

``` typescript
// with getplayersession, move to other rooms
public custom(alias: string, _gameObjects?: GameObject[]): ActionResult | undefined {
        if (alias === "gotootherroom-game") {

            const room: generatorRoom = new generatorRoom();
            getPlayerSession().currentRoom = room.alias;
            return room.examine();
        }

        else if (alias === "goToLocker"){

            const room: lockerRoom = new lockerRoom();
            getPlayerSession().currentRoom = room.alias;
            return room.examine();
        }
        return undefined;
    }
```

This is the "class" for the fitness room. It is not the whole code but a part of it.

``` typescript
export class fitnessRoom extends Room{
    public constructor(){
        super(fitnessRoomAlias, goToRoomAlias);
    }

    public name(): string {
        return "Fitnessroom";
    }

    public images(): string[] {
        return ["fitnesroom_ai 2","staffmember" ];
    }

    public actions(): Action[] {
        return [
            new ExamineAction(), 
            new TalkAction(), 
            new CustomAction("look-around", "Look around", false), 
            new CustomAction("gotootherroom-game", "Go werkend",true),
            new GoAction(),
            new CustomAction("goToLocker", "Go to lockers", false)
        ];
    }

    public objects(): GameObject[] {
        return [this, new securityOutfit_item(), new fitnessStaffMember(), new generatorRoom()];
    }

```