## Spatula -- A New, Extended Architecture, for General Purpose Scrapping

<span style = "font-family:'Courier New', monospace; font-size:7pt;">


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


</span>

### Prolegomena in Regards to Terminology:

`Classes` are denoted by the plural. `Objects` that are instances of a given class are refered to by the singular. In that way, _`Targets`_ is the class
of the _`Target`_ objects; a _`Requester`_ object belongs to the category ("class") of _the `Requesters`_.

#### A comment regarding what constitutes a DataSource:

A DataSource can be thought of as something that exposes a _flow of data_, an indeterminate I/O entity (from the point of view of the project) to which we want to interface. A DataSource could be taking information from, or bringing information to, potentially any kind of source, and the only thing that's of interest to us is that such DataSource gives/takes data.
	Such an entity has a way of being accessed that we cannot in general know in advance, particularly not from the point of view of the code.
	In order to clarify this, some examples of what might constitute a DataSource might come in hand:
	
* **Files:** what constitutes the DataSource in this case _is not_ *the file* itself, but it's interface. We're never dealing with a file "directly", we always do that in accordance to, and through, an interface. Even if we're not in Python, we access files as abstractions provided by some layer above which we operate and with which we interact. E.g: objects/methods exposed by the built-ins of Python's runtime, SysCalls to the Operating System, you name it...). It's that interface the thing that we conceive as *A DataSource*.
	 
* **Directories:** if a Directory is conceptualized as a "container" that holds a set of files and maybe other directories "inside" of it, a directory can be conceptualized as a DataSource that provides, for example, file after file as its data. In turn, each such files, could be thought of as a DataSource each one. Directories share some common characteristics with files (e.g.: they "contain" something) while in other regards, they're fundamentally different: while a file might, for example, give or take lines of text for which an order is guaranteed, a directory would deal with a collection of files/other directories, for which an order is by no means guaranteed.
	 	 	 
* **Module, Method Call, or Fields Exposed by an Object:** As such, a module (like a Python module) might expose an interface to an underlying "service". The module itself could be thought as a DataSource that provides data when queried to do so. In general such module is of more interest to be employed as an intermediary to abstract some other sources, but conceptually
	 
* **DataBase:** DataBases are a major concern for this project in its present state and they represent a major DataSource with which to deal. Interfaces to such entities are usually provided as modules with a set of methods that 'do stuff'. Differences among the variety of existing databases are usually exposed as differences in the interface that the interface modules provide. These differences arise from factors like:
	* The database paradigm in question, e.g.: RDMS vs Document-oriented vs 
	* The vendor: different vendors do provide or might provide variations in the bells-and-whistles of their products, even for a given paradigm or standard (e.g.: MySQL vs MS SQLServer vs PostreSQL vs etc)
		
* **API:** For example, a REST API accessible through an HTTP connection. Tipically we would be dealing with these entities by means of, again, 'canned' modules that are provided by a third-party. While in effect we're dealing with a module, what we're interested in is in what the API provides and for which a module is a mere means for that end.
	 
* **HTTP Request:** A single HTTP Request could be thought as a DataSource. What such request returns with a GET method, could be thought as the content of a file, and that would be an aspect of this DataSource that has a commonality with a file, for example. Other aspects, nonetheless, are different: if we thing about HTTP's methods as an interface, these are fundamentally different to those of a file. An HTTP connection is referred in a fundamentally different way, with an http:// schema, port, parameters, etc., and, as a DataSource, it deals with fundamentally different entities: essentially, whole documents.
	 
Now, let's get a little wild:
	 
* **Terminal:** As a DataSource, it could be thought of as a stream of characters. The application in question is going to dictate how we abstract such a stream. Are we agnostic to that character stream? Do we differentiate control-characters? Do we interpret a whole terminal control syntax (VT-100, ANSI X3.64, etc.)? How we abstract such access is the competence of the classes in the Targets hierarchy.
	 
* **Serial-port:** as a bit stream, byte/n-bit-word stream (RS-232), frame-stream (Ethernet), etc. While a low-level interface, it is perfectly legitimate to think about these in such raw terms, because we're discussing about DataStreams. How we interpret and access this stream, is the competence of the Targets class hierarchy
	 
* **Audio, Video or Audio/Video File:** Audio could be thought of as a series of samples, or a series of blocks containing samples. Video could be likewise be thought of as a stream of frames.
	 
* **Audio, Video or Audio/Video Stream:** Idem but with differences. While an audio/video source from a file by nature has a beginning and an end, a stream not necessarily share this characteristic. The reason to make this distinction will become clear later. A continuous broadcast could fall into this category. 

To summarize: A DataSource is a source of information in a *wide sense*, for which we are interested to get access to. Different DataSources share some characteristics, while being different in other regards. In order to maximize the flexibility and generality of the design, the similarities are going to be abstracted as a class/classes with a uniform interface(s), while the differences are to be captured by subclassing that/those superclass(es).

Some characteristics that come into mind when considering some random DataSources:

* *"Single-Shot"*: A DataSource that, when queried for data, *"gives a whole Response and 'finishes'"*.
* *Iterability*: Data could be repeatedly queried to the DataSource, yielding Response after Response.
* *Boundedness*: *Boundedness* has to do with the extension of the data being retrieved (being *responded by* the DataSource in question)
	* *Bounded*:
	* *Unbounded*:
* *"Real-Time"*:
* *Cacheability*:

#### Spatula's General Architecture:

 * `Targets` Class/`Target` Objects : The `Targets` class aims to abstract the peculiarities that appear in the access of different DataSources; its subclasses are meant to articulate this abstractions. Each DataSource has characteristics that are amenable to be abstracted in an uniform way.

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
