## Comparable
```
package comparableAndComparator;

public class _Comparable implements Comparable {
	
	
	@Override
	public int compareTo(Object o) {
		return 0;
	}
}

```

## Comparator

```

import java.math.BigInteger;
import java.util.Scanner;

public class Main {

	public static void main(String[] args) {

		// Get the message to be encrypted.
		String inputText = getUserInput();

		// Start encrypting
		BigInteger base = new BigInteger("1");
		BigInteger multiplier = new BigInteger("2");
		BigInteger wSum = new BigInteger("0");

		// Get superincreasing sequence w
		DoublyLinkedList superincreasingSequence = new DoublyLinkedList();
		for (int index = 0; index < 640; index++) {
			superincreasingSequence.addBigIntegerAtEnd(base);
			wSum = wSum.add(base);
			base = base.multiply(multiplier);
		}

		// Generate q and r
		BigInteger q = wSum.add(base.divide(multiplier)); // q = 1.5 * sum
		BigInteger r = calculateR(q);

		// Generate public key
		DoublyLinkedList publicKey = new DoublyLinkedList();
		DoubleNode dummy = superincreasingSequence.getHead();
		for (int index = 0; index < 640; index++) {
			publicKey.addBigIntegerAtEnd((dummy.getC().multiply(r)).mod(q));
			dummy = dummy.getNext();
		}

		// Encrypt the text
		BigInteger encryptSum = new BigInteger("0");
		int position = 0; // 0 - 640
		for (int index = 0; index < inputText.length(); index++) {

			// Get the binary string
			char currentChar = inputText.charAt(index);
			int ascii = currentChar;
			String binary = Integer.toBinaryString(ascii);
			while (binary.length() < 8) {
				binary = "0" + binary;
			}

			// Get the sum (encrypted code) for this node and add it to total
			BigInteger nodeSum = new BigInteger("0");
			for (int n = 0; n < binary.length(); n++) {
				BigInteger currentDigit = new BigInteger(binary.charAt(n) + "");
				nodeSum = nodeSum.add(currentDigit.multiply(publicKey.getNthValue(position)));
				position++;
			}
			encryptSum = encryptSum.add(nodeSum);
		}

		System.out.println(inputText + " is encryped as\n" + encryptSum);

		// Decrypt
		BigInteger decryptKey = encryptSum.multiply(r.modInverse(q)).mod(q);

		// Restore the original binary sequence
		int[] binary = new int[position];
		for (int index = position - 1; index >= 0; index--) {
			if (decryptKey.compareTo(superincreasingSequence.getNthValue(index)) >= 0) {
				binary[index] = 1;
				decryptKey = decryptKey.subtract(superincreasingSequence.getNthValue(index));
			} else {
				binary[index] = 0;
			}
		}

		// Calculate and print original string.
		String result = getResult(binary);
		System.out.println("Result of decryption: " + result);
	}

	/**
	 * Get user input and display required information.
	 * 
	 * Precondition: none. 
	 * Postcondition: return user input as a string.
	 * 
	 * @return user input as a string.
	 */
	public static String getUserInput() {
		
		System.out.println("Enter a string and I will encrypt it as single large integer.");
		Scanner input = new Scanner(System.in);
		String inputText = input.nextLine();
		while (inputText.length() >= 80) {
			System.out.println("Your input is too long, please try again (within 80 characters)");
			inputText = input.nextLine();
		}

		System.out.println("Clear text:");
		System.out.println(inputText.toString());

		int textBytes = 0;
		for (int index = 0; index < inputText.length(); index++) {
			textBytes++;
		}
		System.out.println("Number of clear text bytes = " + textBytes);
		return inputText;
	}
	
	/**
	 * Calculate r using given q.
	 * 
	 * @param q key q.
	 * @return key r.
	 */
	public static BigInteger calculateR(BigInteger q) {
		BigInteger r = new BigInteger("1111111111111111111111111111111111111111");
		while (r.compareTo(q) != 0) {
			// If the greatest common divisor is 1, they are coprime.
			if (q.gcd(r).equals(new BigInteger("1"))) {
				break;
			}
			r = r.add(new BigInteger("2")); // Increment r
		}
		return r;
	}
	
	
	/**
	 * Calculate the original string with binary sequence provided. 
	 * 
	 * Precondition: input should be a valid binary array that has 8n elements of 0 or 1.
	 * Postcondition: return the original string the user entered.
	 * 
	 * Time complexity: No case Θ(n)
	 * 
	 * @param binary binary sequence of original string.
	 * @return original string.
	 */
	public static String getResult(int[] binary) {
		// Restore the original text according to the binary sequence
		StringBuilder temp = new StringBuilder();
		StringBuilder result = new StringBuilder();
		for (int index = 0; index < binary.length; index++) {
			temp.append(binary[index]);
			if (temp.length() == 8) {
				// Transfer the binary sequence back to char, and append it to
				// our result
				result.append((char) Integer.parseUnsignedInt(temp.toString() + "", 2));
				temp.setLength(0);
			}
		}
		return result.toString();
	}
}
```
