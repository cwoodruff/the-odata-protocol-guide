<section data-type="chapter">

# The Metadata and Service Model of OData

Let&rsquo;s go back 15 years ago when I started professionally developing software and using relational databases. The relational database was a great tool to deal with data. No more did we have to use flat files to store our data with tools named Paradox, dBase and other such data management systems. We now had more flexibility to build our solutions and the new design pattern Client-Server that was the rage for all developers circa 1996.

Relational databases gave us the SQL language and that in turn allowed the developers of the day to quickly create, read, update and delete (CRUD) data that was stored on the server and build our applications at the client. Life was great (for me at least) because I knew nothing different. If I wanted to learn about a new database, I would get the schema either in a text file that had a set of Create SQL calls for all the objects that made up the database. If we were really lucky we received a printed graph of the database that gave the developers a nice graphical layout of the data tables and views with the relationships between the tables and views. It took time to understand the meaning of the database but that is what we did.

Let&rsquo;s step back and take a look at what Metadata is and how it works within OData. Metadata is defined broadly as &ldquo;Data about Data&rdquo;. Think of metadata as the Dewey Decimal we learned as kids when we visited the library. The card catalog does not carry the information about the content inside the books but it does describe the books and information that the books contain in a broad level to allow readers to find and locate the books they are interested in on the shelves. Metadata does the same for us as users of the data that the OData feeds allow us to consume.

<section data-type="sect1">

# Service Metadata Document: The $metadat Endpoint

In OData, the Service Metadata Document allows the consumers of the data provided by the OData feed to understand the Entity Data Model (Day 3 of the series). The Service Metadata Document does not carry any details of the data held within the data repository of the OData feed. It contains the roadmap to the data. In the SOAP world the Service Metadata Document would be the equivalent of the WSDL file. Let&rsquo;s look at the structure of the Service Metadata Document (in XML) and walk through its map. We will use the Baseball Statistics OData feed found here as our example.

We first need to query the Service Metadata Document from the OData feed. How this is accomplished is my using the $metadata query option at the base of the OData feed as shown below:

<pre data-original-title="" data-type="programlisting" title="">
http://baseball-stats.info/OData/baseballstats.svc/$metadata
</pre>

The Service Metadata Document is returned in the payload after the $metadata query and has three parts: the EDM which is made up of the OData Model and also the Entity Collection.

</section>

<section data-type="sect1">

# Entity Containers

Section content goes here

</section>

<section data-type="sect1">

# Primitive Types

Section content goes here

</section>

<section data-type="sect1">

# Complex Types

Section content goes here

</section>

<section data-type="sect1">

# Entity Types

Section content goes here

</section>

<section data-type="sect1">

# Inheritance

Section content goes here

</section>

<section data-type="sect1">

# Relationships

Section content goes here

</section>

<section data-type="sect1">

# Containment

Section content goes here

</section>

<section data-type="sect1">

# Actions

Section content goes here

</section>

<section data-type="sect1">

# Functions

Section content goes here

</section>

&nbsp;

</section>
<!-- Files for the following:
	Copyright
-->