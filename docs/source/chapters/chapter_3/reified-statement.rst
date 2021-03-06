.. _reified-statement:

Reified Statement
=================

*How can we make statements about statements?*

Context
#######

The foundation of the RDF model is the triple. This simple
structure can be combined to create complex descriptions that can
support any kind of data model. But in some circumstances there
may be a need to annotate an individual triple, e.g. to indicate
when the statement was made, or who by. How can this be achieved?

Solution
########

Use a technique known as reification and model the triple as a
resource, with properties referring to its subject, predicate and
object.

Example(s)
##########

.. code-block::

   _:ex rdf:type rdf:Statement;
     rdf:subject <http://www.example.com/book/1>;
     rdf:predicate <http://xmlns.com/foaf/0/1/maker>;
     rdf:object <http://www.example.com/author/joe>;
     dc:created "2010-02-13".

           
Discussion
##########

Reification is a much maligned technique but has its role to play
in RDF modelling. Understanding its limitations allows it to be
used where appropriate and avoided when other techniques like
:ref:`Named Graphs <named-graphs>` are a better fit.

RDF triples cannot be directly annotated. Reification is a
modelling approach to dealing with this that involves changing the
structure of the model. Each triple that needs to be annotated is
instead modelled as a resource in its own right; an instance of
the rdf:Statement class. The statement resource then has subject,
predicate, and object properties that describe the original
triple; additional properties can then be added to annotate the
statement.

The obvious limitation of this approach is that the data model no
longer contains a simple set of triples, instead it contains
*descriptions of triples*. The triples themselves have not been
explicitly asserted. This makes a reified model harder to query,
more difficult to manipulate, and at least three or four times
larger in terms of number of triples.

In contrast to reification the :ref:`Named Graph <named-graphs>`
pattern offers a data management approach to annotating triples or
sets of triples, by associating them with a URI which can itself
be the subject of additional assertions.

So where is reification best used? Current practice seems to
suggest that reified statements are best used as a technique for
describing changes to the structure of a graph, e.g. statements
that have been added or removed, along with additional properties
to indicate the time of the change, etc. In other circumstances it
is best used with a reasoner or rule engine that can support
surfacing the original triples, thereby simplifying querying. But
this still comes with a cost of increased storage as well as
potentially performance issues.


- :ref:`Named Graphs <named-graphs>`
