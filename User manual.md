C-CUBE Programming Language: Designed for Game Development
C-CUBE is a dynamic, object-oriented programming language specifically crafted to streamline game development processes. It brings together high-performance capabilities with a developer-friendly syntax, enabling both rapid prototyping and the creation of complex game mechanics.

Key Features of the C-CUBE Language
Dynamic and Flexible Structure
C-CUBE offers dynamic typing. This means variables can hold different data types without requiring explicit type declarations. This flexibility is ideal for the rapid changes and iterations often encountered in game development.

Object-Oriented Programming
C-CUBE supports fundamental object-oriented programming (OOP) constructs such as classes, objects, methods, and inheritance. This allows you to model entities in your game world (players, enemies, items, etc.) like real-world objects, making your code more modular and manageable.

Kod snippet'i
```
class Character {
    init(name, health) {
        this.name = name;
        this.health = health;
    }

    takeDamage(amount) {
        this.health = this.health - amount;
        print(this.name + " took " + amount + " damage. Health: " + this.health);
    }
}

class Player inherits Character {
    init(name, health, score) {
        super.init(name, health);
        this.score = score;
    }

    collectCoin() {
        this.score = this.score + 10;
        print(this.name + " collected a coin. Score: " + this.score);
    }
}

var player1 = Player("Hero", 100, 0);
player1.takeDamage(20);
player1.collectCoin();
```
Simple and Understandable Syntax
C-CUBE's syntax will feel quite familiar to developers accustomed to C//C++ like languages (such as C++, Java, or JavaScript). Code blocks are delimited by curly braces {}, and statements are terminated with semicolons ;. This lowers the learning curve and simplifies integration with existing C++ or C# based game engines.

Memory Management: Generational Garbage Collection
C-CUBE comes with a Generational Garbage Collection (GGC) system, lifting the burden of manual memory management from your shoulders. This advanced memory management system automatically tracks the lifespan of dynamically created objects and cleans up those no longer in use, ensuring your games run smoothly. GGC categorizes objects into "young" and "old" generations, allowing short-lived in-game objects (like bullets, effects) to be quickly reclaimed, while ensuring long-lived objects (like player data, level assets) are scanned less frequently. This reduces performance bottlenecks and allows developers to focus on game logic rather than memory leaks.

Module System and import Statement
C-CUBE features a powerful module system for organizing large projects. With the import statement, you can divide your code into separate files and logical units. This reduces code duplication, facilitates teamwork, and enhances the scalability of your project.

Kod snippet'i
```
// math_utils.ccb file
fun add(a, b) {
    return a + b;
}

fun subtract(a, b) {
    return a - b;
}

// main.ccb file
import "math_utils" as Math;

var result = Math.add(10, 5);
print(result); // Output: 15
```
Multi-Language Interoperability (Native Interoperability)
C-CUBE boasts an architecture that can seamlessly integrate with libraries compiled in native languages like C++. Thanks to this feature, you can directly call high-performance engine components or existing libraries written in other languages (such as C, C++, Rust, etc.) from your C-CUBE code. Through the ModuleLoader, external functions and data structures can be easily linked into the C-CUBE environment. This allows you to develop performance-critical areas (graphics rendering, physics engine, AI algorithms) in other languages, while implementing game logic, user interfaces, and rapid prototyping in C-CUBE. This "mixed-language" approach offers developers both performance and flexibility.

How to Use the C-CUBE Interpreter
To run your C-CUBE programs, simply use the c-cube interpreter. The interpreter reads your code and executes it directly.

Running a C-CUBE File
To run a C-CUBE file (typically with a .ccb extension), just specify the interpreter and the filename on the command line:

Bash
```
c-cube game_mechanics.ccb
```
The command above will execute the C-CUBE code within the game_mechanics.ccb file.

Using the Interactive Shell (REPL)
If you don't specify any file, the c-cube interpreter will launch an interactive shell (Read-Eval-Print Loop - REPL). In this mode, you can type C-CUBE code line by line and see the results instantly:

Bash
```
c-cube
```
```
> var x = 10;
> x = x * 2;
> print(x);
20
> class Cube { init(size) { this.size = size; } }
> var myCube = Cube(5);
> print(myCube);
<instance of Cube>
> exit() // To exit (if supported by default) or Ctrl+C
```
The REPL is excellent for testing small code snippets, exploring language features, and quickly experimenting.

Step into the world of game development with C-CUBE and combine your creativity with performance and flexibility!
