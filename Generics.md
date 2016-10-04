## Example Stack Class
```
public class Stack<E extends Object> {

	private E[] stack;
	private int topIndex;
	
	public Stack() {
		stack = (E[])(new Object[6]);
		topIndex = -1;
	}
	
	public void push(E object) {
		if (topIndex == stack.length - 1) {
			E[] newStack = (E[])(new Object[stack.length * 2]);
			for (int i = 0; i < stack.length; i++) {
				newStack[i] = stack[i];
			}
			stack = newStack;
		}
		stack[++topIndex] = object;
	}
	
	public E pull() {
		if (topIndex == -1)
			throw new EmptyStackException();
		return stack[topIndex--];
	}
	
	public boolean isEmpty() {
		return topIndex == -1;
	}
	
	public static void main(String[] args) {
		String test = "t";
		Stack<String> stack = new Stack<>();
		int count = 0;
		while (count < 1000) {
			stack.push(test);
			count ++;
		}
		while (count > 0) {
			System.out.println(stack.pull());
			count --;
		}
	}
}
```
