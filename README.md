## Spatula -- A New, Extended Architecture, for General Purpose Scrapping

```
        DataSource/DataSink  DataSource/DataSink              DataSource/DataSink                 DataSource/DataSink
        of Type 0            of Type 1                ...     of Type i                  ...      of Type (n-1)
        
        +------------------+ +------------------+             +------------------+                +------------------+
        |   DataSource_0   | |   DataSource_0   |             |   DataSource_0   |                |   DataSource_0   |
        +------------------+ +------------------+             +------------------+                +------------------+
                 .                    .                                .                                   .
                 .                    .                                .                                   .
        +------------------+ +------------------+             +------------------+                +------------------+
        | DataSource_(m-1) | | DataSource_(p-1) |             | DataSource_(q-1) |                | DataSource_(r-1) |
        +------------------+ +------------------+             +------------------+                +------------------+
                 
                 AA                   AA                               AA                                  AA  
                 ||                   ||                               ||                                  ||
                 ||                   ||                               ||                                  ||
    ...___________________________________________________________________________________________________________________________________________________...   
    
    ...---------------------------------------------------------------------------------------------------------------------------------------------------...            
                 ||                   ||                               ||                                  ||   Spatula
                 ||                   ||                               ||                                  ||   
                 VV                   VV                               VV                                  VV
        
        +------------------+ +------------------+             +------------------+                +------------------+
        |     Target_0     | |     Target_1     |     ...     |     Target_i     |       ...      |   Target_(n-1)   |
        +------------------+ +------------------+             +------------------+                +------------------+
          V              A     V              A                 V              A                    V              A
          |              |     |              |                 |              |                    |              |
          |              |     |              |                 |              |                    |              +------------------------+
          |              |     |              |                 |              +------------------- | --------------------------------+     |
          |              |     |              +---------------- | --------------------------------- | --------------------------+     |     |
          |              +---- | ------------------------------ | --------------------------------- | -------------------------+|     |     |
          |                    |                                |                                   |                          ||     |     |
          |                    |                                |                                   |                          ||     |     |
          |                    |                                |                                   |                          ||     |     |
          | +----------+       | +--------------------+         | +----------------------+          | +--------------------+   ||     |     |
          | |Response  |       | |ContainerResponse   |         | |ContainerResponse     |          | |ContainerResponse   |   ||     |     |
          | |          +       | |                    |         | |                      |          | |                    |   ||     |     |
          | |         /        | |   +------------+   |         | |    +------------+    |          | |   +------------+   |   ||     |     |
          | +--------+         | |   |Response_0  |   |         | |    |Response_0  |    |          | |   |Response_0  |   |   ||     |     |
          |                    | |   |            +   |         | |    |            +    |          | |   |            +   |   ||     |     |    
          | A singular         | |   |           /    |         | |    |           /     |          | |   |           /    |   ||     |     |    
          | response.          | |   +----------+     |         | |    +----------+      |          | |   +----------+     |   ||     |     |
          |                    | |                    |         | |                      |          | |                    |   ||     |     |
          |                    | |   +------------+   |         | |    +------------+    |          | |   +------------+   |   ||     |     |
          |                    | |   |Response_1  |   +         | |    |Response_1  |    |          | |   |Response_1  |   |   ||     |     |
          |                    | |   |            +  /          | |    |            +    |          | |   |            +   |   ||     |     |
          |                    | |   |           /  /           | |    |           /     |          | |   |           /    |   ||     |     |
          |                    | |   +----------+  /            | |    +----------+      |          | |   +----------+     |   ||     |     |
          |                    | |                /             | |                      |          | |                    |   ||     |     |
          |                    | +---------------+              | |           .          |          | |          .         |   ||     |     |
          |                    |                                | |           .          |          | |          .         |   ||     |     |
          |                    |  Finite, definite (its         | |           .          |          | |          .         |   ||     |     |
          |                    |  size is known ahead of        | |                      |          | |                    |   ||     |     |
          |                    |  time), and iterable set       | |    +------------+    |          | |   +------------+   |   ||     |     |
          |                    |  of Response objects           | |    |Response_i  |    |          | |   |Response_i  |   |   || ... | ... |
          |                    |  contained in a Response,      | |    |            +    |          | |   |            +   |   ||     |     |
          |                    |  an iterable                   | |    |           /     |          | |   |           /    |   ||     |     |
          |                    |  ContainerResponse object.     | |    +----------+      |          | |   +----------+     |   ||     |     |
          |                    |                                | |                      |          | |                    |   ||     |     |
          |                    |                                | |           .          |          | |          .         |   ||     |     |
          |                    |                                | |           .          |          | |          .         +   ||     |     |
          |                    |                                | |           .          |          | |          .        /    ||     |     |
          |                    |                                | |                      |          | |                  /     ||     |     |
          |                    |                                | |  +----------------+  |          | +-----------------+      ||     |     |
          |                    |                                | |  |Response_(n-1)  |  +          |                          ||     |     |
          |                    |                                | |  |                +  /          | Infinite, unbounded,     ||     |     |
          |                    |                                | |  |               /  /           | and iterable set of      ||     |     |
          |                    |                                | |  +--------------+  /            | Response objects         ||     |     |
          |                    |                                | |                   /             | contained in iterable    ||     |     |
          |                    |                                | +------------------+              | ContainerResponse.       ||     |     |
          |                    |                                |                                   |                          ||     |     |
          |                    |                                |                                   |                          ||     |     |
          |                    |                                | Finite, indefinite, and           |                          ||     |     |
          |                    |                                | iterable set of Response          |                          ||     |     |
          |                    |                                | objects contained in iterable     |                          ||     |     |
          |                    |                                | ContainerResponse object.         |                          ||     |     |
          |                    |     +--------------------------+                                   |                          ||     |     |
          |                    |     |                                                              |                          ||     |     |
          +----------------+   |     |     +--------------------------------------------------------+                          ||     |     |
                           |   |     |     |                                                                                   ||     |     |
                           |   |     |     |                                                                                   ||     |     |
                           |   |     |     |                                                                                   ||     |     |
                           |   |     |     |                                                                                   ||     |     |
                           |   | ... | ... |                                                                                   ||     |     | 
                           |   |     |     |                                                                                   ||     |     |
                           |   |     |     |                                                                                   ||     |     |
                           |   |     |     |                      +---------------+                                            ||     |     |
                           |   |     |     |     +-------+       /.................\                                           ||     |     |
                           |   |     |     |     |Query  +      /...................\                 +----------------+       ||     |     |
                           V   V     V     V     |      /      /.....................\                |                |>------+|     |     |
                        +---------------------+  +-----+      /.......................\               |                |>-------+     |     |  
                        |                     |              +.........................+              |                |    .  ||     |     |
                        |                     |<--------<... |.........................| ...<--------<|                |    .  ||     |     |
                        |     Requester_0     |              |.........................|              |   Scrapper_0   |    .  ||     |     |
                        |                     |>-------->... |.........................| ...>-------->|                |>-------------+     |
                        |                     |              |.........................|              |                |    .  ||     |     |
                        +---------------------+              |.........................| +---------+  |                |    .  ||     |     |
                           .   .     .     .                 |.........................| |Request  +  |                |    .  ||     |     |
                           |   |     |     |                 |.........................| |        /   |                |>-------------------+
                           |   |     |     |                 |.........................| +-------+    +----------------+       ||     |     |            
                           |   | ... | ... |                 |.........................|                                       ||     |     |
                           |   |     |     |     +-------+   |.........................|                                       ||     |     | 
                           |   |     |     |     |Query  +   |.........................|              +----------------+       ||     |     |
                           V   V     V     V     |      /    |.........................|              |                |>------+|     |     |
                        +---------------------+  +-----+     |.........................|              |                |>-------+     |     |  
                        |                     |              |.........................|              |                |    .  ||     |     |
                        |                     |<--------<... |.........................| ...<--------<|                |    .  ||     |     |
                        |     Requester_1     |              |.........................|              |   Scrapper_1   |    .  ||     |     |
                        |                     |>-------->... |.........................| ...>-------->|                |>-------------+     |
                        |                     |              |.........................|              |                |    .  ||     |     |
                        +---------------------+              |.........................| +---------+  |                |    .  ||     |     |
                           .   .     .     .                 |.........................| |Request  +  |                |    .  ||     |     |
                           |   |     |     |                 |.........................| |        /   |                |>-------------------+
                           |   | ... | ... |                 |.........................| +-------+    +----------------+       ||     |     |
                           |   |     |     |                 |.........................|                                       ||     |     |
                                                                                                    
                           .   .     .     .                 .                         .                      .                ..     .     .
                           .   .     .     .                 .                         .                      .                ..     .     .
                           .   .     .     .                 .                         .                      .                ..     .     .
                                                                                                                            
                           |   |     |     |                 |.........................|                                       || ... | ... |
                           |   | ... | ... |     +-------+   |.........................|                                       ||     |     |
                           |   |     |     |     |Query  +   |.........................|              +----------------+       ||     |     |
                           V   V     V     V     |      /    |.........................|              |                |>------+|     |     |
                        +---------------------+  +-----+     |.........................|              |                |>-------+     |     |  
                        |                     |              |.........................|              |                |    .  ||     |     |
                        |                     |<--------<... |.........................| ...<--------<|                |    .  ||     |     |
                        |     Requester_i     |              |.........................|              |   Scrapper_j   |    .  ||     |     |
                        |                     |>-------->... |.........................| ...>-------->|                |>-------------+     |
                        |                     |              |.........................|              |                |    .  ||     |     |
                        +---------------------+              |.........................| +---------+  |                |    .  ||     |     |
                           .   .     .     .                 |.........................| |Request  +  |                |    .  ||     |     |
                           |   |     |     |                 |.........................| |        /   |                |>-------------------+
                           |   | ... | ... |                 |.........................| +-------+    +----------------+       ||     |     |
                           |   |     |     |                 |.........................|                                       ||     |     |                      
                                                                                                                               
                           .   .     .     .                 .                         .                      .                ..     .     .
                           .   .     .     .                 .                         .                      .                ..     .     .
                           .   .     .     .                 .                         .                      .                ..     .     .
                                                                                                                               
                           |   |     |     |                 |.........................|                                       ||     |     |
                           |   | ... | ... |     +-------+   |.........................|                                       ||     |     |                 
                           |   |     |     |     |Query  +   |.........................|              +----------------+       ||     |     |
                           V   V     V     V     |      /    |.........................|              |                |>------+|     |     |
                        +---------------------+  +-----+     |.........................|              |                |>-------+     |     |  
                        |                     |              |.........................|              |                |    .         |     |
                        |                     |<--------<... |.........................| ...<--------<|                |    .         |     |
                        |   Requester_(s-1)   |              |.........................|              | Scrapper_(t-1) |    .         |     |
                        |                     |>-------->... |.........................| ...>-------->|                |>-------------+     |
                        |                     |              +.........................+              |                |    .               |
                        +---------------------+               \......................./  +---------+  |                |    .               |
                                                               \...................../   |Request  +  |                |    .               |
                                                                \.................../    |        /   |                |>-------------------+
                                                                 \................./     +-------+    +----------------+
                                                                  +---------------+    
```

#### A Prolegomena in Regards to Terminology:

 * `Classes` are denoted by the plural. `Objects` that are instances of a given class are refered to by the singular. In that way, _`Targets`_ is the class
of the _`Target`_ objects; a _`Requester`_ object belongs to the category ("class") of _the `Requesters`_.

 * A comment in what in here constitutes a DataSource:
A DataSource can be thought of as simply something that exposes a _flow of data_, an indeterminate I/O entity (from the point of view of the project) to which we want to interface. A DataSource could be taking information from, or bringing information to, a variety of sources, and the only thing that's of interest to us, is that such DataSource gives/takes data.
	Such an entity has a way of being accessed that we cannot in general know in advance, particularly not from the point of view of the code.
	In order to clarify this, some examples might come in hand:
	 * Files: what constitutes de DataSource in this case _is not_ *the file* itself, but it's interface. We're never dealing with a file "directly" (we always do that in accordance to an interface. Even if we're not in Python, we access files as abstractions provided by some layer above which we operate and with which we interact. E.g: objects/methods exposed by the built-ins of Python's runtime, SysCalls to the Operating System, you name it...). It's that interface the thing that we conceive as *A DataSource*.
	 
	 * Directories: a directory can be conceptualized as a DataSource that provides, for example, file after file as its data. Or, given that 
	 	 	 
	 * A Module, method call, or fields exposed by an object: As such, a module (like a Python module) might expose an interface to an underlying "service". The module itself could be thought as a DataSource that provides data when queried to do so. In general such module is of more interest to be employed as an intermediary to abstract some other sources, but conceptually
	 
	 * A DataBase: DataBases are a major concern for the project in its present state and they represent a major DataSource with which to deal. Interfaces to such entities are usually provided as modules with a set of calls that 'do stuff'. Differences among the variety of existing databases are usually exposed as differences in the interface that the interface modules provide. These differences arise from factors like:
		* The database paradigm in question, e.g.: RDMS vs Document-oriented 
	 
	
#### Spatula's General Architecture:

 * `Targets` Class/`Target` Objects : The `Targets` class aims to abstract the peculiarities that appear in the access of different DataSources; its subclasses are meant to articulate this abstractions. Each DataSource has characteristics that are amenable to be abstracted in an uniform way.
For example:
 * Some DataSources lend themselves to be treated as an iterable entity (IterTarget), for example, an API source for which the interface exposes


```
                              |   |     |     |                                                                                   ||     |     |
                              |   |     |     |                                                                                   ||     |     |
                              |   |     |     |              +-------+                                                            ||     |     |
                              |   |     |     |              |Query  +                                   +----------------+       ||     |     |
                              V   V     V     V              |      /                                    |                |>------+|     |     |
                           +---------------------+           +-----+                                     |                |>-------+     |     |  
                           |                     |                                                       |                |    .         |     |
                           |                     |<-----------------------------------------------------<|                |    .         |     |
                           |     Requester       |                                                       |    Scrapper    |    .         |     |
                           |                     |>----------------------------------------------------->|                |>-------------+     |
                           |                     |                                                       |                |    .               |
                           +---------------------+          +---------+                                  |                |    .               |
                                                            |Request  +                                  |                |    .               |
                                                            |        /                                   |                |>-------------------+
                                                            +-------+                                    +----------------+
```                                                                       


*Example 1*: A single Requester object (Instance of the superclass Requester via its subclasses) can operate multiple Target objects (Instances of the superclass Targets via its subclasses) to build a Request (of the superclass Requests, via its subclasses), when queried to do so. 
The different Targets subclasses expose uniform interfaces across comparable DataSources, seeking to abstract comparable characteristics (Format, behavior, interface, etc). For example, some Targets might be single-shot readable, like a FileTarget, or an HTTPTarget, or amenable to iterability, let's say, a DirectoryTarget. Such abstraction would allow, for example, to return an iterable response which iterates over the files on such a directory, giving access to them as FileResponse objects. While Targets abstracts 
DataSource interfaces (what differentiates, let's say, accessing a TextFileTarget from accessing an HTTPTarget, Responses abstract the responses of such DataSources. This approach allows for maximum flexibility. 
For example, a live IRC chat (or any other for that matter) could be abstracted as a Target (e.g.: IRCTarget) which, for example, returns TextResponse objects as unbounded infinite iterable ContainerResponse objects, themselves Responses (but with an iterable interface, particular to IRCTarget's IterableResponses) that, when iterated, might yield individual lines of text corresponding to an IRC server traffic. Such a traffic is better modeled as unbounded given the nature of the DataSource (i.e.: people just chat indefinitely). This infinite unbounded iterability of the Response object returned by a given Target instance (A Response object, in particular, belonging i.e.: to Responses's subclass UnboundedResponses), allows for the management of RealTimeTargets. RealTimeTargets could naturally be a superclass whose subclasses abstract in an homogeneous way, those aspects of the Target interface that are peculiar to real-time, open-ended, DataSources. Such Finite indefinite Responses, let's say, modeled with a subclass of BoundedResponses
