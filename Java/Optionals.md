# Java Optionals
[Optionals: Pattern](https://forums.oracle.com/ords/apexds/post/optionals-patterns-and-good-practices-2540)

## Optionals: First Patterns
```
Optional<Person> opt = ...;

if (opt.isPresent()) {

    int value = opt.get(); // there is a value

} else {

    // decide what to do

}
```

