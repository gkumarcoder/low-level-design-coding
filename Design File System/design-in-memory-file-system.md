Problem Statement: Design a data structure that simulates an in-memory file system.

FileSystem fileSystem = new FileSystem();

fileSystem.ls("/");                                // return []

fileSystem.mkdir("/a/b/c");

fileSystem.addContentToFile("/a/b/c/d", "hello");

fileSystem.ls("/");                              // return ["a"]

fileSystem.readContentFromFile("/a/b/c/d");      // return "hello"


**Approach #1 Using separate Directory and File List** 

The root directory acts as the base of the directory structure. Each directory contains two hashmaps namely *dirs* and *files* 

The dirs contains data in the form:

 [(subdirectory1_name: subdirectory1_structure),(subdirectory2_name : subdirectory2_structure)]

 The files contains data in the form

 [(file1: file1_contents),(file2:file2_contents)...]


 ![image](https://github.com/gkumarcoder/low-level-design-coding/assets/25560217/6def7208-d7b2-4fdb-a76f-955b5d10519c)

 Now, we'll discuss how we implement the various commands required.

**1. ls:** 

In this case, we start off by initializing t, a temporary directory pointer, 

To the root directory. We split the input directory path based on / and obtain the individual levels of directory names in a d array. 

Then, we traverse over the tree directory structure based on the individual directories found and we keep on updating the t directory pointer to point to the new level of directory(child) as we go on entering deeper into the directory structure. 


At the end, we will stop at either the end level directory or at the file name depending upon the input given. If the last level in the input happens to be a file name, we simply need to return the file name. So, we directly return the last entry in the ddd array. If the last level entry happens to be a directory, we can obtain its subdirectory list from the list of keys in its dirsdirsdirs hashmap. Similarly, we can obtain the list of files in the last directory from the keys in the corresponding filesfilesfiles hashmap. We append the two lists obtained, sort them and return the sorted appended list.

```
   public List < String > ls(String path) {
        Dir t = root;
        List < String > files = new ArrayList < > ();
        if (!path.equals("/")) {
            String[] d = path.split("/");
            for (int i = 1; i < d.length - 1; i++) {
                t = t.dirs.get(d[i]);
            }
            if (t.files.containsKey(d[d.length - 1])) {
                files.add(d[d.length - 1]);
                return files;
            } else {
                t = t.dirs.get(d[d.length - 1]);
            }
        }
        files.addAll(new ArrayList < > (t.dirs.keySet()));
        files.addAll(new ArrayList < > (t.files.keySet()));
        Collections.sort(files);
        return files;
    }
```

