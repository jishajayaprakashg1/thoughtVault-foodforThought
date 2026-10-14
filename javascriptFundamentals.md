## History of the web
- 1986 : Charles Golffarb : SGML (Standard General Markup Language)
- 1990 : Tim Berners-Lee : HTML (Hyper Text Markup Language) : hrf: links were introduced: to embed links into a document
Gave birth to HTTP
- 1994: Marc Andreessen : First commercial browser: Netscape was launched
- 1995: Brendon Eich : JavaScript : initially called mocha then liveScript: to make the html page more animated and interactive
- 1998: Haykon Wium Lee : CSS : Cascading Style Sheet : for fonts and styles

### Compilation and process map in general
- We write the code in high level languages like: C++, Java, etc, which is not understood my the machine.
- Compiler converts the source code into object code ( zero's and one's understood by the machine).
- Link it to the respective function using Linker ( printf function is a library)
- and generate an executable called program stored on the disk.
- OS picks up the program from disk and executes it as a process on RAM.
- OS creates a process map on the RAM where process is arranged into
  + code_text : compiled machine instructions
  + data : Global and static variables
  + heap : dynamically allocated memory
  + stack : Local variables, function params, return addresses
 
## JavaScript Process Map
```
g = 10; //Global variable
var x = 5;  //local to anonymous function
var y = 10; //local to anonymous function

function add(a,b){
  var c = a+  b; //local to add function
  return c;
}

add(x, y);  // call function
```
When this program is executed as a process, it is loaded onto RAM on a process map with below sections:
- JavaScript Engine : Memory management, Interpreter, JIT compiler, Garbage collector : Interpreter will read it and JIT compiler will convert it into 0 and 1
- Global Area : a pointer(global if executed on node/ window if executed on browser) is created for g = 10
- Heap : a dictionary is created with key value pair stored as g = 10 and pointer from global area will point to this
  another dictionary is created with key value pair stored x = 5 and pointer from call stack will point to this
- Call Stack : it keeps track of the running code. First a function execution context called anonymous function is created.
 this will contain a pointer for local variables x and y
 Another function execution context is created for add (x,y) with pointer for a,b,c



