

# Singleton 
```
/**
 * Ensure a class has only one instance and provide a global point of access to it.
 * Why? There's only one instance exists or it comsumes too much resources and we cannot afford two.
 * 
 * Know how to write code!
 * 
 * @author Phoenix
 */
public class Singleton {

	private static final Singleton INSTANCE = new Singleton();
	
	private Singleton() {};
	
	public static Singleton getInstance() {
		return INSTANCE;
	}
	
}
```

# Builder

```
public class User {

	String firstName;
	String lastName;
	String phone;
	String address;
	int age;
	
	// No default constructor
//	public User () {}
	
	/**
	 * Why private? Encourage the use of Builder class
	 * @param builder
	 */
	private User(UserBuilder builder) {
		/**
		 * Any variable could be or not be here
		 */
		this.firstName = builder.firstName;
		this.lastName = builder.lastName;
		this.age = builder.age;
		this.phone = builder.phone;
		this.address = builder.address;
	}
	
	public static void main(String[] args) {
		// Problems with this normal program:
		//		User user1 = new User("Master", "Lv");
		//		user1.age = 5;
		
		/**
		 * When will this object be "complete"? If we try to access "age" now, we may get null
		 * Builder pattern: Once the object is created, 
		 */
		// 1. One line
		User user2 = new User.UserBuilder("First","Last").age(25).address("My address").phone("412-537-2008").build();
		
		// 2. Separate
		User.UserBuilder builder = new User.UserBuilder("first", "last");
		builder.age(25);
		builder.address("My address");
		builder.phone("412-537-2008");
		User user3 = builder.build();
		
	}
	
	/**
	 * Static nested class (not a non-static inner class)
	 * @author Phoenix
	 */
	// With "static", UserBuilder will not be object-dependable
	// With "public", Buildercan be accessed outside, instead of User class
	public static class UserBuilder {
		/**
		 * final fields are required
		 */
		private final String firstName; // final = required
		private final String lastName;  // final = required
		private String phone;
		private String address;
		private int age;
		
		public UserBuilder (String firstName, String lastName) {
			this.firstName = firstName;
			this.lastName = lastName;
		}
		
		public User build() {
			return new User(this);
		}
		
		public UserBuilder phone(String phone) {
			this.phone = phone;
			return this;
		}

		public UserBuilder address(String address) {
			this.address = address;
			return this;
		}

		public UserBuilder age(int age) {
			this.age = age;
			return this;
		}
		
	}
	
}
```

# Factory

##### Layers/complexity:
1. Family manufacturer: One method for each component (like this)
2. Local factory: One class for each component 
3. Modern factory: Multiple classes for each component

```
/**
 * Factory method - factory class - abstract factory
 * Factory method: easy, single purpose
 * Factory class: medium, one group/kind of product(room)
 * Abstract factory: complex, many different kinds of products (button, window, bar...) 
 * @author Phoenix
 */
public class AbstractFactory {}

interface RoomFactory {
	public Room makeRoom();
}

class OrdinaryRoomFactory implements RoomFactory {
	
	@Override
	public Room makeRoom() {
		return new OrdinaryRoom();
	}
}

class MagicRoomFactory implements RoomFactory {
	
	@Override
	public Room makeRoom() {
		return new MagicRoom();
	}
}

class MazeGame2 {
	private final RoomFactory factory;
	public MazeGame2(RoomFactory factory) {
		this.factory = factory;
	}
	
	void createGame() {
		Room r1 = factory.makeRoom();
		Room r2 = factory.makeRoom();
	}
}

```

```
/**
 * A creational pattern for creating new objects
 * Separate out the object creation logic and delegate it to factory class or method
 * @author Phoenix
 */
public class MazeGame {
	public void createGame() {
		Room room1 = makeRoom();
		Room room2 = makeRoom();
		room1.connect(room2);
		this.addRoom(room1);
		this.addRoom(room2);
	}
	
	// Factory method
	protected Room makeRoom() {
		return new OrdinaryRoom();
	}
	public void addRoom(Room room){}
	
	
	public static void main(String[] args) {
		MazeGame game1 = new MazeGame();
		game1.makeRoom(); // make two ordinary rooms
		MagicMazeGame game2 = new MagicMazeGame();
		game2.makeRoom(); // make two magic rooms
	}
}


class MagicMazeGame extends MazeGame {
	@Override
	protected Room makeRoom() {
		return new MagicRoom();
	}
}

class Room {
	public void connect(Room room) {}
}
class OrdinaryRoom extends Room {}
class MagicRoom extends Room {}
```
