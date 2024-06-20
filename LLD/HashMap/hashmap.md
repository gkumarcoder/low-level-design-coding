
1. The first step is to design a hash function using the modulo operator
   When we are selecting a modulo base, it’s advisable to choose a prime number. This is because choosing a prime number as the modulo base helps
   minimize collisions. Since prime numbers offer better distribution of hash codes, reducing the likelihood of collisions



1st Approch
===============


```
import java.util.*;

// Define DesignHashMap class to implement the HashMap functionality
class DesignHashMap {
    public int keySpace;
    public Bucket[] buckets;

    // Constructor to initialize the HashMap
    public DesignHashMap() {
        // Initialize the hash map with a prime number of key spaces to reduce collisions
        keySpace = 2069;
        // Create an array of buckets to store key-value pairs, using the initialized prime number
        buckets = new Bucket[keySpace];
        for (int i = 0; i < keySpace; i++) {
            buckets[i] = new Bucket();
        }
    }

    // Function to add a key-value pair to the hash map
    public void put(int key, int value) {
        // Calculate the hash key using modulo operation with the key space
        int hashKey = key % keySpace;
        // Update the bucket at the hashed key with the key-value pair
        buckets[hashKey].update(key, value);
    }

    // Function to retrieve the value associated with a given key from the hash map
    public int get(int key) {
        // Calculate the hash key using modulo operation with the key space
        int hashKey = key % keySpace;
        // Return the value associated with the key from the corresponding bucket
        return buckets[hashKey].get(key);
    }

    // Function to remove a key-value pair from the hash map given a key
    public void remove(int key) {
        // Calculate the hash key using modulo operation with the key space
        int hashKey = key % keySpace;
        // Remove the key-value pair from the corresponding bucket
        buckets[hashKey].remove(key);
    }
}


// DRIVER CODE
public class Main {
    // Main method to demonstrate the usage of the HashMap
    public static void main(String args[]) {
        
        DesignHashMap inputHashMap = new DesignHashMap();
        List<Integer> keys = Arrays.asList(5, 2069, 2070, 2073, 4138, 2068);
        List<Integer> keysList = new ArrayList<>(Arrays.asList(5, 2069, 2070, 2073, 4138, 2068));
        List<Integer> values = Arrays.asList(100, 200, 400, 500, 1000, 5000);
        List<String> funcs = Arrays.asList("Get", "Get", "Put", "Get", "Put", "Get", "Get", "Remove", "Get", "Get", "Remove", "Get");
        List<List<Integer>> funcKeys = Arrays.asList(
            Arrays.asList(5), 
            Arrays.asList(2073), 
            Arrays.asList(2073, 50), 
            Arrays.asList(2073), 
            Arrays.asList(121, 110), 
            Arrays.asList(121), 
            Arrays.asList(2068), 
            Arrays.asList(2069), 
            Arrays.asList(2069), 
            Arrays.asList(2071), 
            Arrays.asList(2071), 
            Arrays.asList(2071)
        );
        
        for (int i = 0; i < keys.size(); i++) {
            inputHashMap.put(keys.get(i), values.get(i));
        }
        
        for (int i = 0; i < funcs.size(); i++) {
            if (funcs.get(i) == "Put") {
                System.out.println(i + 1 + ".\t put(" + funcKeys.get(i).get(0) + ", " + funcKeys.get(i).get(1) + ")");
                if (!(keysList.contains(funcKeys.get(i).get(0)))) {
                    keysList.add(funcKeys.get(i).get(0));
                }
                inputHashMap.put(funcKeys.get(i).get(0), funcKeys.get(i).get(1));
            } else if (funcs.get(i) == "Get") {
                System.out.println(i + 1 + ".\t get(" + funcKeys.get(i).get(0) + ")");
                System.out.println("\t Value returned: " + inputHashMap.get(funcKeys.get(i).get(0)));
            } else if (funcs.get(i) == "Remove") {
                System.out.println(i + 1 + ". \t remove(" + funcKeys.get(i).get(0) + ")");
                inputHashMap.remove(funcKeys.get(i).get(0));
            }

            // Printing the hashmap using our custom print function
            System.out.println("\nHash map:\n");
            HashPrint.print(inputHashMap, keysList);
            System.out.println(new String(new char[100]).replace('\0', '-'));
        }
    }
}
```

2nd Approch
==============

```
// Define Pair class to store key-value pairs

class Pair<K, V> {
    private K key;
    private V value;

    // Constructor to initialize key-value pair
    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    // Getter methods for key and value
    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }
  }

```

```
import java.util.ArrayList;

import java.util.ArrayList;

class Bucket {
    private ArrayList<Pair<Integer, Integer>> bucket;

    public Bucket() {
        // Constructor to initialize an empty list to store key-value pairs
        bucket = new ArrayList<>();
    }

    // Method to get the value corresponding to the given key
    public int get(int key) {
        // Iterate through each key-value pair in the bucket
        for (Pair<Integer, Integer> kv : bucket) {
            // If the key matches the provided key, return the corresponding value
            if (kv.getKey() == key) {
                return kv.getValue();
            }
        }
        // If the key is not found, return -1
        return -1;
    }

    // Method to update the value for the given key
    public void update(int key, int value) {
        // Flag to indicate whether the key is found in the bucket
        boolean found = false;
        // Iterate through each key-value pair in the bucket
        for (int i = 0; i < bucket.size(); i++) {
            Pair<Integer, Integer> kv = bucket.get(i);
            // If the key matches the key of the current key-value pair
            if (key == kv.getKey()) {
                // Update the value of the key-value pair
                bucket.set(i, new Pair<>(key, value));
                // Set the flag to true, indicating that the key is found
                found = true;
                break;
            }
        }
        // If the key is not found in the bucket, add it along with its value
        if (!found) {
            bucket.add(new Pair<>(key, value));
        }
    }

    // Method to remove the key-value pair with the given key
    public void remove(int key) {
        // Iterate through each key-value pair in the bucket
        for (int i = 0; i < bucket.size(); i++) {
            Pair<Integer, Integer> kv = bucket.get(i);
            // If the key matches the key of the current key-value pair
            if (key == kv.getKey()) {
                // Delete the key-value pair from the bucket
                bucket.remove(i);
                // Exit the loop as the key has been removed
                break;
            }
        }
    }
}
```


