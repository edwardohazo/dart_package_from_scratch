# Dart Course

## Content Overview

- What is Dart?
- Type Safety
- Soundness
- Type Inference
- Null Safety
- Dart Compilers

---

## What is Dart?

Dart is a programming language highly optimized for performance and tailored to fit within its ecosystem.

The dart arrow represents the Dart programming language.
The dart player represents the developer using Dart.
The dartboard represents the ecosystem of Dart-based applications.

For the developer (the dart player) to build successful applications (hit the target on the dartboard), the Dart language (the dart arrow) must be highly optimized. This optimization ensures that developers can build precise, high-performance apps that fit well within the ecosystem of Dart-based apps

- **Precision** – Dart is designed to be as optimized as possible, ensuring high performance across different platforms.
  
- **Speed** – Like a dart, Dart is minimalist and fast to execute, making it ideal for responsive applications.

- **Tough** – Like a dart that has to be tough so to not break in peaces, Dart's design ensures scalability, maintainability, and readability, allowing developers to write clear, organized code for projects of any size.

- **Modifiable** – Dart supports hot reload, allowing for rapid development and immediate feedback during code changes.

- **Popular Framework** – Dart powers Flutter, a popular framework used for building cross-platform applications, providing developers with a rich ecosystem for app development.

---

## Particularities of Dart

- **Type Safe** – Dart is a type-safe language, meaning that operations performed on data are constrained by the data's type, ensuring correctness and reducing errors at runtime.

### Example: Type Safety in Dart

```dart
void main() {
  int number = 42; // A variable of type int
  String text = "Hello"; // A variable of type String
  
  // This works because the operation matches the type
  print(number + 10); // Outputs: 52
  
  // This will cause a compile-time error because you can't add an int to a String
  // print(number + text); // Uncommenting this will cause a type error
}
```

### Soundtype System | Type Check 

#### Soundtype System:

- Tools for checking data type errors. 

##### Why is it called sound?

- Sound refers to the sound of typing on a computer inserting data for the analizer checks its data type.

- **Static Analizer** - Check the data type at compile time. If an error compilation fails. It prevents the developer from writing wrong types

- **Run Type Check** - Check the data type at run time. If an error an exeption is thrown. Is like a double check. 

    - Dynamic - Helps the developer to tell the static analizer to ignore or stop listening the sound or the data typed on an specific variable. The only check would be at runtime using type inference.

    - Note: Even though types are mandatory in dart the type inference allows the types not to be annotated, this using var keyword.

    ```dart
    void main() {
      var number = 42; // It will check and convert the type at compile time.
    }
    ```

#### Type Inference

- Type inference is a feature in programming languages that allows the compiler or interpreter to automatically deduce the type of a variable based on the value assigned to it.

#### dynamic vs var

- var - Is not a type, it only tells the static analizer to staticly asign the type to a variable by type inference.

- dynamic - In Dart, dynamic is a standalone type on its own that allows a variable to hold values of any type without enforcing static type checks at compile time. It enables flexibility in variable assignments, as it can store integers, strings, lists, and other types. However, this flexibility comes at the cost of type safety, with type checks occurring only at runtime. Variables declared as dynamic can lead to runtime errors if the assigned values are not compatible with expected operations.

- Note: Standalone types are types that exists independently and is not derived from or a subtype of another type.

- In the case of a declared variable as "var a;" the static analyser will set it to dynamic. If at run time is not defined then it will asign a null value.

#### Null Safety

- Sound null safety is a feature in programming languages, such as Dart, that ensures variables cannot contain a null value unless explicitly allowed.

#### Compilation Process on Desktop and Mobile with JIT compiler

1. Common Front End (CFE): The CFE converts Dart source code into an intermediate representation (IR), specifically a Kernel abstract syntax tree, which is serialized into a .dill file. This file format contains the necessary structure for the Dart virtual machine (VM).

2. Kernel File: When the .dill file is loaded, the Dart VM parses it to create objects that represent entities like classes and libraries. Each entity retains a pointer back to the Kernel binary to access the original data when needed. Importantly, during this process, only the signatures of the entities are deserialized, which helps improve performance by minimizing the amount of data that needs to be loaded.

3. JIT Compilation: When a Dart application runs, the JIT (Just-In-Time) compiler takes the entities from the Kernel file and converts them into an intermediate language (IL). This IL is then compiled into non-optimized machine code for execution.

4. Optimization on Subsequent Runs: For subsequent calls to the same entities, the JIT compiler utilizes information gathered from the previous execution to optimize the intermediate language. This optimization process improves performance by generating optimized machine code.

For Develoment Phase

- JIT (Just in Time Compiler): Part of the VM. It only compiles the amount of code needed at an specific moment. If you re run the code and nothing changed it will use the already compiled code, otherwise it will recompile the code changes only when it´s needed (incremental recompilation). JIT compiler convert the source code into an intermediate language / Representation (IR) so it can be optimized more easely than the machine code, this helps for fast develoment cycles.

- Features of JIT:
  - Testing
  - Debugging
  - Live Metrics Support
  - Fast Development Cycles
  - Incremental compilation

- JIT Hot Reload - Automatically reloads the modified source code after the changes has been made while the application is running.


For Production Phase

AOT (Ahead of Time Compiler) - It compiles all the code to machine code to run fast.

- In this phase user doesn´t care about JIT features


#### Compilation Process on Web

- The compiler converts the source code into Javascript

For Development Phase

- Dartdevc

For Production Phase

- dart2js 

#### Dart Package

- Is a Dart project

#### Files Structure

- pubspec.yalm: Converts a project into a package and Contain the MAIN PACKAGE CONFIGURATIONS and the direct dependencies (packages on which your package directly rely on) and versions of them.

- pubpec.lock: Contains all the packages and their resolved VERSIONS, including both the direct dependencies and the transitive dependencies (packages on which your direct dependencies rely).

- package_config.json: Specifies the LOCATIONS and CONFIGURATIONS of all the packages used in your package, including both direct and transitive dependencies and your package.

NOTE: A package installed is usefull only if it has lib files.

#### Dart Packages Main Phases on its Lifetime

- Development Phase:

    Focuses on the experience of the developer

- Production Phase

    Focuses on the experience of the user

#### Layers a Dart Program Goes Thru When Running

- VM: A collection of software components created by the hypervisor that provides an execution environment, specifying how the hypervisor interacts with the underlying physical computer components that the VM simulates. 

- Dart VM: Collection of components aiding towards natively run the Dart code providing an execution enviorment.

            - Run Time System
            - Development components:
                * Debugging
                * Hot Reload
            - JIT and AOT compilers

    NOTE: The native machine code wich is the code for production phase is run inside a stripped version of the Dart VM whothout features like debugging and hot reload.
 
Any code within VM is running within an isolate wich is a completely independent environment for running code with its own memory heap, its own thread of control called the mutator thread and its own helper threads.

    - Heap: Memory storage managed by garbage collector.
    - Mutator thread: Is a component in the Dart VM that executes Dart code and creates, stores, modifies and delete objects in the memory heap. It operates under the management of the virtual CPU, which schedules its execution and allocates CPU resources for it.

#### PUBSPEC.YAML FILE

- Converts a project into a package and Contain the MAIN PACKAGE CONFIGURATIONS and the direct dependencies (packages on which your package directly rely on) and versions of them.

- The simplest posible pubspec.yaml file contains the name of the package and the enviorment containing the sdk constrains.nExample:

name: dart_package_from_scratch
environment:
  sdk: ^3.4.4

Environment: Focuses on the execution and configuration of Dart applications.

Ecosystem: Encompasses the entire landscape of development resources, tools, frameworks, and community that support Dart.

dart pub get (command): Sets up a package so that it is ready to use and has all the necessary configurations and dependencies in place.























 








