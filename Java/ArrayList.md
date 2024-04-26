# Array List

## Remove Objects from a List with (list.removeIf)
```
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        // Create a list of objects
        List<Object> objectList = new ArrayList<>();
        objectList.add("String 1");
        objectList.add(123);
        objectList.add("String 2");
        objectList.add(456);
        objectList.add("String 3");

        // Remove all objects of a specific class (e.g., String)
        objectList.removeIf(obj -> obj.getClass().equals(String.class));

        // Print the modified list
        for (Object obj : objectList) {
            System.out.println(obj);
        }
    }
}
```
