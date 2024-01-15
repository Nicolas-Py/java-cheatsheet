<<<<<<< Updated upstream
# Turning stream into different data types:

### Stream to String:
```Java
public static String prettyDirections(Stream<OneWay> oneWays) {  
    return oneWays.map(OneWay::prettyPrint).collect(Collectors.joining("\n"));  
}
// Collectors.joining(...) will join all elements of stream to a string seperated by specifyed delimiter
```
=======
# Stream to Map< K, List< V > > (very useful)

train ex from pgdp
```java
Map<String, List<TrainConnection>> typeToConnections = connections
                .collect(Collectors.groupingBy(TrainConnection::type));
```

>>>>>>> Stashed changes
