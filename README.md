# JavaTest
Testing java code

These are the concepts about variables in java and how they are use and their difference:

- Variables
- Final variables
- Fields
- Final fields
- Static fields
- Final static fields

The keyword __static__ makes sense only for fields, but in the code you show you are trying to use it inside a function, where you cannot declare fields (fields are members of classes; variables are declared in methods).

Let's try to rapidly describe them.

### Variables
**Variables** are declared in methods, and used as some kind of mutable local storage (int x; x = 5; x++)

### Final Variables
**final variables** are also declared in methods, and are used as an immutable local storage (final int y; y = 0; y++; // won't compile). They are useful to catch bugs where someone would try to modify something that should not be modified. I personally make most of my local variables and methods parameters final. Also, they are necessary when you reference them from inner, anonymous classes. In some programming languages, the only kind of variable is an immutable variable (in other languages, the "default" kind of variable is the immutable variable) -- as an exercise, try to figure out how to write a loop that would run an specified number of times when you are not allowed to change anything after initialization! (try, for example, to solve fizzbuzz with only final variables!).


fields define the mutable state of objects, and are declared in classes (class x { int myField; }).

final fields define the immutable state of objects, are declared in classes and must be initialized before the constructor finishes (class x { final int myField = 5; }). They cannot be modified. They are very useful when doing multithreading, since they have special properties related to sharing objects among threads (you are guaranteed that every thread will see the correctly initialized value of an object's final fields, if the object is shared after the constructor has finished, and even if it is shared with data races). If you want another exercise, try to solve fizzbuzz again using only final fields, and no other fields, not any variables nor method parameters (obviously, you are allowed to declare parameters in constructors, but thats all!).

static fields are shared among all instances of any class. You can think of them as some kind of global mutable storage (class x { static int globalField = 5; }). The most trivial (and usually useless) example would be to count instances of an object (ie, class x { static int count = 0; x() { count++; } }, here the constructor increments the count each time it is called, ie, each time you create an instance of x with new x()). Beware that, unlike final fields, they are not inherently thread-safe; in other words, you will most certainly get a wrong count of instances of x with the code above if you are instantiating from different threads; to make it correct, you'd have to add some synchronization mechanism or use some specialized class for this purpose, but that is another question (actually, it might be the subject of a whole book).

final static fields are global constants (class MyConstants { public static final double PI = 3.1415926535897932384626433; }).

There are many other subtle characteristics (like: compilers are free to replace references to a final static field to their values directly, which makes reflection useless on such fields; final fields might actually be modified with reflection, but this is very error prone; and so on), but I'd say you have a long way to go before digging in further.

Finally, there are also other keywords that might be used with fields, like transient, volatile and the access levels (public, protected, private). But that is another question (actually, in case you want to ask about them, many other questions, I'd say).
