If one.equals(two), one.hashCode must equal to two.hashCode
If one.hashCode = two.hashCode, it is not necessary that one.equals(two)

## hashCode()
Default implementation: memory address in integer value   

## equals()
```
public boolean equals(Object obj) {
    return (this == obj);
}
```
## ==
Returns true if and only if both variables refer to the same object, if their references are one and the same.

