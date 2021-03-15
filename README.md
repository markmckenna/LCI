# LCI
## Logical Container Infrastructure

The idea behind this (currently placeholder, PoC) project is to create functional infrastructure for enclosing units of computation authored in one language, within units of computation authored in another language. For example, being able to write a library in Javascript and ship it as a native Android library; or writing cross-platform code in Kotlin that executes in a containerized fashion within a desktop application.

The basic thinking is this:
* Writing programs that take advantage of asymmetric multiprocessing is hard;
* Different languages are good at different things;
* Most programming languages lack a large-scale runtime encapsulation scheme;
* Spreading a computation across multiple languages is difficult;
* Sharing code between projects is useful;
* Broad-scale abstraction-based platforms generally are not.

You can think of this project as a collection of small, encapsulated abstraction frameworks that create strongly isolated module spaces that can be embedded in another application. Each of these encapsulated modules can be embedded in any application environment for for which a proper container is available. You can instantiate as many instances of a module as you have resources for in the containing environment, and (to the extent possible on the host platform) each module will be isolated. Modules generally run in their own thread and memory spaces, so they provide coarse grained concurrency opportunities, as well as strong isolation. Code running in a module generally needs to rely on the host system to provide most services, so it is fairly self-contained and unit testable. The module's API has to be well defined in order for the container to be able to interact with it.

In general, building a system using this framework would go something like this:
* Determine what your system's major logical components are going to be
* Author each one as a module, in the language that seems most suitable for that component, with exports that express how that component will be used by others. Use unit tests to verify the behaviour of the module.
* Author one or more 'connective tissue' applications that bring a selection of your (and other partys') components together and wire them up into a functional system.
