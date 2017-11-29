# How Events Works in Java

As i can see inside JButton Class, it simply uses **Publish-Subscribe Pattern** for Implementation of Events.  
these patterns are defines **One-to-Many** Communication.

An Object has a list of Subscribers, when Something happens ,the object will tell everyone on the list about the thing that happened.  
Now, How the subscriber will know What things Should listen to OR How Room will tell the subscribers about supported Events.  
Here is the role of Listener, the Listener is the one who know about events exposed by the Object.
So now the Subscriber will use Listener to listen to events exposed by the Object.  
`Listener = Interface` between Object and Subscriber

## Let’s Do it

Our Example will be :
- a Room (The Object) which has two Events.
- a MainWindow (The Subscriber) which is interested in Room Events.
- RoomListener (The Listener) which knows about Room Events and will tell Subscriber about the events.

So, Now converting this to Java will result in:

- a class to represent the Room              (Object)
- a class to represent the RoomListener      (Listener)
- a class to represent the MainWindow        (Subscriber)
--- 

## The Object:

### Room Class

Start by Creating a new Class called Room.java

```java
public class Room {
 
}
```

make a place to store Persons inside it
```java
public class Room {
 
    /* Store Persons inside Room */
    List<Person> PersonsList = new ArrayList<>();
 
    public Room(){
          /* Just Empty Constructor */
    }
}
```
The List is like the Array in C++, but here you can add new element or remove an element during runtime.
So, List is an array with variable length during Runtime.

Now, we will add a two basic functions to our Room Class
```java
/* Add New Person to PersonsList */
public void AddPerson(Person PersonInfo) {
       //Add Person to List
       PersonsList.add(PersonInfo);
}
 
/* Remove a Person from PersonsList */
public void RemovePerson(Person PersonInfo) {
       //Remove a Person from List
       PersonsList.remove(PersonInfo);
}
```

### Person Class

make a new file called Person.java and put the following code
```java
public class Person{
     String Name;    //Store Person Name
     int ID;         //Store Person ID
 
     /* Class Constructor */
     public Person(String person_name,int person_id){
           Name = person_name;
           ID  = person_id;
     }
}
```
it just a simple class to represent a person

---

### TheListener

make a new Class Called RoomListener.java
```java
public abstract class RoomListener {
 
}
```
Why we make it abstract class ?
Because, abstract classes can’t be instantiated, it doesn’t make sense to allow instantiation of empty class
So Something like

```java
RoomListener Rl = new RoomListener() //is not valid
```

Add The Following Two Functions to RoomListener Class

```java
public abstract void TellMeWhoComes(Person PersonInfo);
public abstract void TellMeWhoLeaves(Person PersonInfo);
```
`TellMeWhoComes()`: will called by Room whenever a Person enters the room
`TellMeWhoLeaves()`: will called by Room whenever a Person leaves the room


Now let’s go back to Room class

---

### Back to Object:

Open Room.java and Now we will implement listeners list and when events will be fired.

1. Implementing Listeners List

add the following definition

```java
List<RoomListener> listeners = new ArrayList<>();
```
add the following function, so a subscriber can add new listener to the list
```java
/* Add New RoomListener to the List of Listeners */
public void AddRoomListener(RoomListener pl) {
        listeners.add(pl);
}
```
2. Implementation of Event Firing
Modify Function `AddPerson()`, So it will look like this
```java
/* Add new Person to PersonsList */
public void AddPerson(Person PersonInfo) {
 
       //Add Person to List
       PersonsList.add(PersonInfo);
 
      // Notify All Subscribers that a New Person has Entered the Room
      for (RoomListener p : listeners) {
          p.TellMeWhoComes(PersonInfo);
      }
}
```
What we added here is for loop on all listeners in the list to notify them about the person entered the room.

Modify Function RemovePerson(), So it will look like this
```java
/* Remove a Person from PersonsList */
public void RemovePerson(Person PersonInfo) {
       //Remove a Person From List
       PersonsList.remove(PersonInfo);
 
       // Notify All Subscribers that a Person has left the Room
       for (RoomListener p : listeners) {
           p.TellMeWhoLeaves(PersonInfo);
       }
}
```
---

The Subscriber

The Subscriber is the class which will use listener to catch the events fired by Room

if you are building a GUI application then open your JFrame class and do the following:

1. Create New Instance of Room

1
Room EmbeddedSystemsRoom = new Room();
2. Add Event Handlers

```java
public MainWindow() {
         initComponents();
 
        /* MainWindow (Subscriber) will Add a new Listener */
        EmbeddedSystemsRoom.AddRoomListener(new RoomListener() {
 
            /* I'm interested to know who Enters the Room */
            @Override
            public void TellMeWhoComes(Person p)
            {
                /* Do Whatever you want here */
 
                /* in this example: it will update a label on the UI */
                lbl_LastEnter.setText(p.Name);
            }
 
            /* I'm interested to know who Leave the Room */
            @Override
            public void TellMeWhoLeaves(Person p)
            {
                /* Do Whatever you want here */
 
                /* in this example: it will update a label on the UI */
                lbl_LastExit.setText(p.Name);
 
            }
        });
 ```

 **Finally: I hope this Tutorial give you a good start with Custom Events in Java**