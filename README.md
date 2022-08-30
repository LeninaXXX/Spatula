## Spatula -- A New, Extended Architecture, for General Purpose Scrapping

             +------------------+ +------------------+             +------------------+                +------------------+
             |   DataSource_0   | |   DataSource_0   |             |   DataSource_0   |                |   DataSource_0   |
             +------------------+ +------------------+             +------------------+                +------------------+
                      .                    .                                .                                   .
                      .                    .                                .                                   .
             +------------------+ +------------------+             +------------------+                +------------------+
             | DataSource_(m-1) | | DataSource_(p-1) |             | DataSource_(q-1) |                | DataSource_(r-1) |
             +------------------+ +------------------+             +------------------+                +------------------+
					  A	



             +------------------+ +------------------+             +------------------+                +------------------+
             |     Target_0     | |     Target_1     |     ...     |     Target_i     |       ...      |   Target_(n-1)   |
             +------------------+ +------------------+             +------------------+                +------------------+
               V                    V                                V                                   V
               |                    |                                |                                   |
               |                    |                                |                                   |
               |                    |                                |                                   |
               |                    |                                |                                   |
               |                    |                                |                                   |
               |                    |                                |                                   |
               |                    |                                |                                   |
               |                    |                                |                                   |
               | +----------+       | +--------------------+         | +----------------------+          | +--------------------+
               | |Response  |       | |ContainerResponse   |         | |ContainerResponse     |          | |ContainerResponse   |
               | |          +       | |                    |         | |                      |          | |                    |
               | |         /        | |   +------------+   |         | |    +------------+    |          | |   +------------+   |
               | +--------+         | |   |Response_0  |   |         | |    |Response_0  |    |          | |   |Response_0  |   |    
               |                    | |   |            +   |         | |    |            +    |          | |   |            +   |    
               | A singular         | |   |           /    |         | |    |           /     |          | |   |           /    |    
               | response.          | |   +----------+     |         | |    +----------+      |          | |   +----------+     |
               |                    | |                    |         | |                      |          | |                    |
               |                    | |   +------------+   |         | |    +------------+    |          | |   +------------+   |
               |                    | |   |Response_1  |   +         | |    |Response_1  |    |          | |   |Response_1  |   |
               |                    | |   |            +  /          | |    |            +    |          | |   |            +   |
               |                    | |   |           /  /           | |    |           /     |          | |   |           /    |
               |                    | |   +----------+  /            | |    +----------+      |          | |   +----------+     |
               |                    | |                /             | |                      |          | |                    |
               |                    | +---------------+              | |                      |          | |                    |
               |                    |                                | |           .          |          | |          .         |
               |                    |  Finite, definite (its         | |           .          |          | |          .         |
               |                    |  size is known ahead of        | |           .          |          | |          .         |
               |                    |  time), and iterable set       | |                      |          | |                    |
               |                    |  of Response objects           | |    +------------+    |          | |   +------------+   |
               |                    |  contained in a Response,      | |    |Response_i  |    |          | |   |Response_i  |   |
               |                    |  an iterable                   | |    |            +    |          | |   |            +   |
               |                    |  ContainerResponse object.     | |    |           /     |          | |   |           /    |
               |                    |                                | |    +----------+      |          | |   +----------+     |
               |                    |                                | |                      |          | |                    |
               |                    |                                | |           .          |          | |          .         |
               |                    |                                | |           .          |          | |          .         +
               |                    |                                | |           .          |          | |          .        /
               |                    |                                | |                      |          | |                  /  
               |                    |                                | |  +----------------+  |          | +-----------------+   
               |                    |                                | |  |Response_(n-1)  |  +          | 
               |                    |                                | |  |                +  /          | Infinite, unbounded,
               |                    |                                | |  |               /  /           | and iterable set of 
               |                    |                                | |  +--------------+  /            | Response objects 
               |                    |                                | |                   /             | contained in iterable
               |                    |                                | +------------------+              | ContainerResponse.
               |                    |                                |                                   |
               |                    |                                | Finite, indefinite, and           |
               |                    |                                | iterable set of Response          |
               |                    |                                | objects contained in iterable     |
               |                    |                                | ContainerResponse object.         |
               |                    |   +----------------------------+                                   |
               |                    |   |                                                                |
               +----------------+   |   |   +------------------------------------------------------------+
								|   |   |   |                         
								|   |   |   |                         
								|   |   |   |                         
								|   |   |   |                         
								|   |   |   |                 +-------+
								|   |   |   |                 |Query  +                
								|   |   |   |                 |      /                 
								V   V   V   V                 +-----+                  
                           +---------------------+                                +----------------+
                           |                     |<------------------------------<|                |
                           | Requester           |                                | Scrapper       |
                           |                     |>------------------------------>|                |
                           +---------------------+                                +----------------+
                                                             +---------+    
                                                             |Request  +
                                                             |        /
                                                             +-------+ 
							      
							      
							      
							      
							      
                             .      .   .  .
                             .      .   .  . 
                             .      .   .  . 
                             .      .   .  . 
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |         
                             |      |   |  |         +-------+                
                             |      |   |  |         |Query  +                
                             V      V   V  V         |      /                 
                          +---------------------+    +-----+                     +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_0     |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---------------------+                +---------+     +----------------+
                             |      |   |  |                     |Request  +
                             |      |   |  |                     |        /
                             |      |   |  |                     +-------+  
                             |      |   |  |         +-------+               
                             |      |   |  |         |Query  +                
                             V      V   V  V         |      /                 
                          +---------------------+    +-----+                     +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_1     |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---------------------+                +---------+     +----------------+
                                                                 | Request +    
                                                                 |        /
                                                                 +-------+ 
                                                                 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                             +---------+    
                                                             | Request +
                                                             |        /
                                                             +-------+ 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                             +---------+    
                                                             | Request +
                                                             |        /
                                                             +-------+ 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                             +---------+    
                                                             | Request +
                                                             |        /
                                                             +-------+ 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                             +---------+    
                                                             | Request +
                                                             |        /
                                                             +-------+ 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                             +---------+    
                                                             | Request +
                                                             |        /
                                                             +-------+ 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                             +---------+    
                                                             | Request +
                                                             |        /
                                                             +-------+ 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                             +---------+    
                                                             | Request +
                                                             |        /
                                                             +-------+ 
							      
                             |      |   |  |                                                  
                             |      |   |  |        
                             |      |   |  |                 +-------+
                             |      |   |  |                 | Query +                
                             |      |   |  |                 |      /                 
                             V      V   V  V                 +-----+                  
                          +---    --------------+                                +----------------+
                          |                     |<------------------------------<|                |
                          | Re    quester_(n-1) |                                | Scrapper_(n-1) |
                          |                     |>------------------------------>|                |
                          +---    --------------+                                +----------------+
                                                         +---------+    
                                                         | Request +
                                                         |        /
                                                         +-------+ 

                             |  |   |  |                                                  
                             |  |   |  |        
                             |  |   |  |                 +-------+
                             |  |   |  |                 | Query +                
                             |  |   |  |                 |      /                 
                             V  V   V  V                 +-----+                  
                          +-----------------+                                +----------------+
                          |                 |<------------------------------<|                |
                          | Requester_(n-1) |                                | Scrapper_(n-1) |
                          |                 |>------------------------------>|                |
                          +-----------------+                                +----------------+
                                                         +---------+    
                                                         | Request +
                                                         |        /
                                                         +-------+ 

            Example 1: A single Requester object (Instance of the superclass Requester via its subclasses) can operate  
            multiple Target objects (Instances of the superclass Targets via its subclasses) to build a Request (of the
            superclass Requests, via its subclasses), when queried to do so. 
            The different Targets subclasses articulate uniform interfaces across comparable DataSources, seeking to 
            abstract comparable characteristics (Format, Behavior, Interface). For example, some Targets might be 
            single-shot readable, like a FileTarget, or an HTTPTarget, or amenable to iterability, let's say, a 
            DirectoryTarget. Such abstraction would allow, for example, to return an iterable response which iterates 
            over the files on such a directory, giving access to them as FileResponse objects. While Targets abstracts 
            DataSource interfaces (what differentiates, let's say, accessing a TextFileTarget from accessing an 
            HTTPTarget, Responses abstract the responses of such DataSources. 
            This approach allows for maximum flexibility. 
            For example, a live IRC chat (or any other for that matter) could be abstracted as a Target (e.g.: 
            IRCTarget) which, for example, returns TextResponse objects as unbounded infinite iterable ContainerResponse
            objects, themselves Responses (but with an iterable interface, particular to IRCTarget's IterableResponses) 
            that, when iterated, might yield individual lines of text corresponding to an IRC server traffic. Such a 
            traffic is better modeled as unbounded given the nature of the DataSource (i.e.: people just chat 
            indefinitely). This infinite unbounded iterability of the Response object returned by a given Target 
            instance (A Response object, in particular, belonging i.e.: to Responses's subclass UnboundedResponses).
            , allows for the management of RealTimeTargets. RealTimeTargets could naturally be a superclass
            whose subclasses abstract in an homogeneous way, those aspects of the Target interface that are peculiar to
            real-time, open-ended, DataSources. Such 
            Finite indefinite Responses, let's say, modeled with a subclass of BoundedResponses