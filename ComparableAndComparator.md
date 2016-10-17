## Comparable
```
public class _Comparable implements Comparable {
	
	@Override
	public int compareTo(Object o) {
		return 0;
	}
}

```

## Comparator

```
import java.util.*;

class Car {

	int weight = 500;

	public Car(int weight) {
		this.weight = weight;
	}
}

class CarComparator implements Comparator<Car> {
	@Override
	/**
	 * Parameter type has to be the same class as declared above
	 */
	public int compare(Car c1, Car c2) {
		if (c1.weight > c2.weight)
			return 1;
		else if (c1.weight == c2.weight)
			return 0;
		else
			return -1;
	}
}

public class ComparatorDemo {

	public static void main(String[] args) {
		CarComparator cc = new CarComparator();
		Car c1 = new Car(400);
		Car c2 = new Car(800);
		System.out.println(cc.compare(c1, c2));

		ArrayList<Car> list = new ArrayList<>();
		Collections.sort(list, cc); // Collection, Comparator

		/**
		 * Another example from my project.
		 */

		// Get all followers' profiles from MySQL
		ArrayList<String[]> allProfiles = new ArrayList<>();

		// Sort the result according to ascending alphabet
		Collections.sort(allProfiles, new Comparator<String[]>() {

			@Override
			public int compare(String[] s1, String[] s2) {
				int response = 0;
				if (s1[0].compareTo(s2[0]) > 0) {
					response = 1;
				} else if (s1[0].compareTo(s2[0]) < 0) {
					response = -1;
				} else if (s1[0].compareTo(s2[0]) == 0) {
					if (s1[1].compareTo(s2[1]) > 0) {
						response = 1;
					} else if (s1[1].compareTo(s2[1]) < 0) {
						response = -1;
					}
				}
				return response;
			}
		});

	}

}
```
