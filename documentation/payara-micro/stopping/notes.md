# Uber-JAR

- Unshaded: All biscuits out of wrappers in shopping bag
 - One big jar
 all in same cl
- Shaded: All biscuits out of wrappers, then carve "BONBON" in place of "BOURBON"
all in same cl
- Nested: Shopping bag full o' biscuits
 - One big jar with jars

 classloader knows of jar files, and can load files it knows of

 Parnt - child relationships with cl - parent cl and child pl

 cl asks parent first if it knows of class, otherwise does it itself. Never asks children

 cant resovle class conflicts as with application classloaders you can have two cls with same class
