

## Dataflow vs Scalding 

### Intro, Pipelines and Pcollections

The basic structure of a Dataflow Job has 3 essential parts. 

Pipeline, the object that encapsulates a data processing task from start to finish.

Pcollection, the distributed data that the pipeline operates on. Although Pcollections can be created in-memory, they are generally created via reading some external source.

Ptransform, a data processing operation or step in the pipeline. Every Ptransform takes a Pcollection, performs a function on that Pcollection and outputs either one or more Pcollection objects.

Special Note: I/O transforms are special beam PTransform functions that read and write data from different data formats. 

A typical beam program consists of:

1. The creation of a Pipeline Object.

2. Reading external data sources into a Pcollection object via I/O transforms.

3. Apply transformations to the data via PTransform functions.

4. Use IOs to write the final, transformed PCollection(s) to an external source.


Scalding has Pipes and TypedPipes to provide a unified interface to data that is distributed among a cluster of machines, likewise, spark has Datasets and RDDs. On a similiar analogy, Beam has Pcollections. These Pcollections can be bounded (they come from a fixed source like a folder with x number of files or a file), or they can be unbounded (a continuosly updating source such as a subscription).

Note: The elements of a PCollection may be of any type, but must all be of the same type.

When reading an input source, that is automatically transformed into a Pcollection by the beam pipeline. 

````
lines = pipeline | 'ReadMyFile' >> beam.io.ReadFromText(
    'gs://some/inputData.txt')
````

### Transformations 

Remember that `PTransforms` are the actions you take to transform a `PCollection` ?

Well, in order to do so, you must use the generic apply operator `|` that allows you to chain transformations. Once you pipe the transformation, the transformed PCollection is then piped down to the next transformation and so on and so forth until the final node of PCollections is retrieved. (Remember PTransform can output zero, one or many PCollections)

````
[Final Output PCollection] = ([Initial Input PCollection] | [First Transform]
              | [Second Transform]
              | [Third Transform])
````


#### Map

In scalding map is used to 

