
Example
``` java
import java.util.ArrayList;  
import java.util.List;  
  
public class Generics {  
    public static  <T extends List<?>, V> V count (T thing1, V thing2) {  
        
        // possible because T must be a list or subclass
        for (Object x: thing1) { // Object is needed because of Wildcard 
            System.out.println(x);  
        }  
  
        return thing2;  
    }  
  
    public static void main(String[] args) {  
        ArrayList<Integer> list = new ArrayList<>();  
        list.add(1);  
        list.add(2);  
        list.add(3);  
        list.add(4);  
        System.out.println(count(list, 5));  
    }  
}
```