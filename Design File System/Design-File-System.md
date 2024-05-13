**Problem Statement:** We will implement using java 

![image](https://github.com/gkumarcoder/low-level-design-coding/assets/25560217/9f67aa70-796b-452b-9008-6b0f05bf347d)


Design a file system that allows you to create new paths and associate them with different values.

The format of a path consists of one or more concatenated strings, each starting with a forward slash (/) followed by one or more lowercase English letters. For instance, “/documents” and “/documents/pictures” are valid paths, while an empty string (”“) and a single slash (”/“) are not.

Implement the FileSystem class as follows:

**bool createPath(string path, int value) Creates a new path and associates a value to it if possible and returns true. Returns false if the path already exists or its parent path doesn't exist.**

**int get(string path) Returns the value associated with path or returns -1 if the path doesn't exist.**

**Example 1:**

FileSystem fileSystem = new FileSystem();

fileSystem.createPath("/a", 1); // return true

fileSystem.get("/a"); // return 1

**Example 2:**

FileSystem fileSystem = new FileSystem();

fileSystem.createPath("/users", 100); // return true

fileSystem.createPath("/users/desktop", 2); // return true

fileSystem.get("/users/desktop"); // return 2

fileSystem.createPath("/c/d", 1); // return false because the parent path "/c" doesn't exist.

fileSystem.get("/c"); // return -1 because this path doesn't exist.


JAVA SOLUTION :

```
class FileSystem{
    Folder root; // trie root
    
    public FileSystem() {
        root = new Folder();
    }
    
    public boolean createPath(String path, int value) {
        if (pathExists(path)) { 
            return false;
        }
        int lastIndex = path.lastIndexOf("/");
        boolean result = pathExists(path.substring(0, lastIndex));
        if (result) {
            addPath(path, value);
        }
        return result;
    }
    
    public int get(String path) {
        if (!pathExists(path)) {
            return -1;
        }
        Folder folder = root;
        for (String foldername : path.split("/")) {
            folder = folder.subfolders.get(foldername);
        }
        return folder.value;
    }
    
    private void addPath(String path, int value) {
        root.addSubfolder(path.split("/"), 0, value);
    }
    
    private boolean pathExists(String path) {
        if (path.isEmpty()) {
            return true;
        }
        Folder folder = root;
        for (String folderName : path.split("/")) { 
            if (folder.subfolders.containsKey(folderName)) {
                folder = folder.subfolders.get(folderName);
            } else {
                return false;
            }
        }   
        return true;
    }
}

// Trie Node
class Folder {
    public String name;
    public int value; // applies to to the folder that marks end of a path
    public HashMap<String, Folder> subfolders = new HashMap<>();

    public Folder() {}
    public Folder(String name) {
        this.name = name;
    }
    
    public void addSubfolder(String[] path, int index, int value) {
        String subfolderToBeCreated = path[index];
        if (!subfolders.containsKey(subfolderToBeCreated)) {
            subfolders.put(subfolderToBeCreated, new Folder(subfolderToBeCreated));
        }
        if (index < path.length - 1) {
            Folder subfolder = subfolders.get(subfolderToBeCreated);
            subfolder.addSubfolder(path, index + 1, value);
        } 
        if (index == path.length - 1) {
            subfolders.get(subfolderToBeCreated).value = value;
        }
    }

}
/**
 * Your FileSystem object will be instantiated and called as such:
 * FileSystem obj = new FileSystem();
 * boolean param_1 = obj.createPath(path,value);
 * int param_2 = obj.get(path);
 */

```























REF: https://leetcode.ca/2019-02-08-1166-Design-File-System/




