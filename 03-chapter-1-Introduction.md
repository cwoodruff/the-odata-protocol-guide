# Why OData: An Introduction to the Open Data Protocol

The Internet today is undergoing a revolution. Somewhere around 1995, the Internet exploded in growth as browsers became commonplace and businesses started creating Web sites en masse. In the early 2000's DHTML surged in popularity, standardizing on the core technologies of HTML, JavaScript and CSS. Another five years down the road AJAX provided a radically different way to load data onto Web pages without forcing the browser to reload the page. Now (in the early 2010's), we are seeing a proliferation of data APIs: Web services that encourage the consumption and modification of data through custom clients, mashups, et cetera.

If history is any indicator, this is likely what we will see: first, data APIs will become incredibly popular. This has already happened for the most part. Next, the data API community will experience increasing pain due to lack of standardization. It would be easy to argue that we are currently in that phase. Finally, the data API community will coalesce around a set of technologies that standardize how data APIs are accessed. Although we have seen some early efforts to standardize data APIs, no one technology has emerged as the clear leader.

OData (the Open Data protocol) was born of the belief that data APIs should follow a set of conventions that simplify both the production and the consumption of the API by following a standard. SOAP, REST, and other technologies have all headed in this direction but have only simplified parts of consuming APIs. OData is a strong contender for unification of data APIs. In this book we will examine the standardized version of the OData protocol and analyze whether it is capable of providing the data API standardization the community needs.

# A Brief History of Web APIs

## The Advent of Data APIs

Programmable Web has been registering data APIs since 2005. At the end of 2005 there were barely 100 APIs registered. These APIs included such notables as Flickr, Skype, eBay, Google Maps and Salesforce.com as well as a number of lesser known APIs like Ning and TypePad. Data APIs were registered slowly over the next three years, taking until late 2008 to reach the 1,000 mark. However, this was just the beginning of a hockey stick growth curve. The first thousand registered APIs were built over eight years (2000-2008). It took only 18 months to accrue the next thousand APIs, and just over 9 months for the thousand APIs after that. Growth accelerated dramatically in 2011, which saw more than 2,000 new API registrations for a total of nearly 5,000 APIs. By the end of 2012 there were more than 8,000 registered data APIs at ProgrammableWeb.com.

The point of all these numbers is that data APIs are more likely an expectation than a luxury for new Web properties. Although these are publicly registered APIs we see similar growth in enterprise services. Where the three tier model used to commonly be database, Web site, browser, it would be easy to argue that now the three tier model is database, data API, client. One really interesting trend is the uptick in Web sites that are built on top of a public data API (that is, the Web site acts as just another client of the data API).

## The Lack of Standardization

The rapid proliferation of data APIs has created a problem, however: the data API space is incredibly fragmented. In the past decade we have seen the rise &ndash; and arguably the fall &ndash; of XML and SOAP, we've recently seen JSON and &ldquo;REST&rdquo; take over mainstream data APIs, and we've seen a major shift from RPC-style architectures to resource-oriented architectures. The result is an ecosystem that in most cases requires developers to read documentation intended for human consumption and write custom code for each service they want to consume. This lack of standardization makes it impossible to scale the data API ecosystem as a whole.

## The Path to Standardization

John Musser of Programmable Web points out an interesting pattern that emerged as the World Wide Web grew to maturity. In 1995, businesses asked whether they needed a Web site at all. In 2000, the need for a Web site was a foregone conclusion. John has drawn a parallel from this observation to a similar pattern with data APIs. In 2005, businesses started to ask whether they needed a data API. In 2010, most of the Web sites that care about scale and reach had data APIs.

**TODO: Reference - http://www.slideshare.net/jmusser/pw-glue-conmay2010**

There is, perhaps, a third phase to this pattern that has recently emerged. In the early days of the Web, sites were created with a combination of browser-specific HTML, CSS and JavaScript. As the Web matured standards and frameworks absorbed the most popular extensions and many Web sites replaced browser-specific code with new standards-based code that adhered to standards like CSS3 or used frameworks like jQuery. (Note that this cycle continues to occur even as this book is being written. Although we now have things like rounded corners in CSS, there are other common practices, like CSS normalization, that have not yet been pulled into one of the major frameworks.)

Data APIs have recently begun the transition into this standardization phase. The vast majority of data APIs use XML or JSON as a serialization format. Many data APIs use OAuth or OAuth2 to authenticate users. There are many such influencers on data APIs. **TODO: Patch this segue up to fit the new content.**&nbsp;Arguably the most notable influencer to this point has been the REST architectural style.

## The problem with Ad-Hoc Data APIs

It may not be immediately apparent what the problem with ad-hoc APIs is even after all this discussion. Why does it matter whether data APIs are standardized or not? Some people might be saying: &ldquo;If we're in an enterprise scenario, chances are we control both the server and the client. Even when we're not in that scenario, there are an array of obvious technologies at hand: HTTP, JSON, URI templates. We should just be able to select some of those technologies (all of which have wide support in a variety of languages), create some pretty URIs and be up and running with a simple service, right?&rdquo; Wrong.

### Ad-Hoc Data APIs Require Documentation

Ad-hoc services always require significant documentation, even when service authors build their service from the most commonly used building blocks. This documentation is typically quite easy to read: here's how you form URIs, this is what the response looks like, and if the response is a collection, the documentation will usually define what fields are available on the items of the collection. While most developers can technically read and implement according to this documentation, there are at least four fundamental problems with ad-hoc service documentation.

#### Problem 1: Consuming documentation does not scale

The first fundamental problem is that consuming ad-hoc service documentation does not scale. A developer who wants to consume a major calendar API, a popular microblogging API, or the premier photo-sharing API is facing a minimum of several hours of reading. More to the point, that time investment is worth absolutely nothing when the developer moves on to consume a different public API.

#### Problem 2: Documentation is often inaccurate and incomplete

Another fundamental problem is that the documentation for an ad-hoc service quite frequently has drifted from the actual implementation of the service. This happens because typically humans are the translation agent that reflect on the actual implementation of the service and decide what documentation needs to be written. As the implementation is transcribed into documentation, small inaccuracies are introduced or details are missed. These small gaps compound over time and sometimes result in documentation that is nearly useless.

#### Problem 3: Ad-hoc services are not guaranteed to be uniform

Another problem is the fact that ad-hoc services almost inevitably lack uniformity. Lack of uniformity can originate from a number of sources: a service that evolves over time, a service that was authored by different developers, or simply a service where the developers weren't particularly diligent about uniformity. At any rate, because ad-hoc services are not guaranteed to be uniform, developers need to read the service documentation almost exhaustively. There can be no assumption that the means of forming URLs in one part of the service is the same means of forming URLs elsewhere in the service.

#### Problem 4: Most developers can't be bothered to read the documentation

Even if none of the above were fundamental problems, there is yet another problem: the fact is that most developers can't be bothered to read the documentation in detail. Although this observation is a sweeping generalization that may not be true of individual developers, the fact is that the majority of developers don't want to be bothered with fine details and nuances. They would rather get a basic idea of how to approach the problem, try some stuff, adjust the approach if necessary, and ultimately move on to another problem.

### Ad-Hoc Data APIs Require Significant Design Investment

The problem of documentation exists because ad-hoc data APIs by definition have a custom design. This custom design frequently affects every part of the API above the HTTP layer. While API designers may adopt common technologies such as JSON and XML, there are still many thousands of decisions that need to be made for even the smallest API.

As we&rsquo;ll see later in the chapter, these design decisions are precisely the reason that OData exists. The OData protocol enables API designers to apply a consistent set of principles to their API. For ad-hoc data APIs, each of these decisions takes time. A few such issues that ad-hoc API designers will need to address:

*   What happens if the resource isn&rsquo;t there? Should the error always be 404 Not Found or is 204 No Content appropriate in some scenarios?
*   How should the API represent null? What does null mean?
*   How should collections be formatted?
*   Does the service support searching? Do the search parameters come across in the URL? The request payload? Headers?
*   Is there a need for payload extensibility? How do consumers distinguish between extensibility data and &ldquo;real&rdquo; data?
*   How are URLs constructed?

Some of these design decisions, such as URL construction, are both a significant time investment and critical to the success of the API. In spite of the potential for getting it wrong, data API designers seem to disproportionately suffer from Not Invented Here syndrome. Mike Amundsen and Leonard Richardson talk about this in their new book _Restful Web APIs_:

**TODO: Sidebar

The main problem I&rsquo;m trying to solve in this book is that hundreds of person-years of design work is locked up in fiat standards where it can&rsquo;t be reused. This needs to stop. Designing a new API today means reinventing a long series of wheels. Once your API is finished, your client developers have to reinvent corresponding wheels on the client side.&rdquo;

### Creating and Updating Documentation

Creating and updating documentation for ad-hoc data APIs is one of the most time consuming effects of this lack of uniformity. There is a rapidly growing amount of similar-but-different ad-hoc data API documentation, such as [Twitter's API documentation](https://dev.twitter.com/docs/api/1.1). This documentation puts an incredible burden on both service authors and consumers. Service authors need to make certain that the documentation is unambiguous and correct. Service consumers need to ensure that they have parsed the documentation correctly (which could be even more of an issue if the documentation isn't written in their primary language &ndash; remember that this documentation comes in the form of human-readable prose) and that their custom client is implemented according to the documentation.

Peter Gruenbaum, founder of SDK Bridge, explores the possibility of [Automated Documentation for REST APIs](http://blog.programmableweb.com/2012/03/28/automated-documentation-for-rest-apis/) in a blog post at [ProgrammableWeb](http://www.programmableweb.com/). Peter suggests three possible approaches for automating documentation:

1.  Use a framework that generates both the API and the documentation
2.  Create a 1:1 mapping between API requests and methods in code
3.  Write documentation as structured data

Interestingly, the first two approaches (the approaches with less overhead) point toward uniformity as the solution.

Subbu Allamaraju also discusses this problem in the [RESTful Web Services Cookbook](http://oreilly.com/catalog/9780596801687/):

The best way to promote design- and development-time discoverability is to unambiguously document the information needed to implement clients.

</aside>

**Problem**

You want to know how to document your web service.

**Solution**

Fully describe the following in human-readable documentation:

*   All resources and methods supported for each resource
*   Media types and representation formats for resources in requests and responses
*   Each link relation used, its business significance, HTTP method to be used, and resource that the link identifies
*   All fixed URIs that are not supplied via links
*   Query parameters used for all fixed URIs
*   URI templates and token substitution rules
*   Authentication and security credentials for accessing resources

For XML representations, if your clients and servers are capable of supporting XML schemas, use a schema language as a &ldquo;convention&rdquo; to describe the structure of XML documents used for representations in requests and responses. For other formats, use conventions to describe representations in prose.

**Discussion**

No machine-readable description can replace human-readable documentation. Documenting your web service in human-readable format such as HTML is the most useful way to enable design-time discovery. When documenting your service, include all the information necessary to implement a client.

Uniformity would solve a number of the problems Subbu proposes documenting above. For instance, OData defines what each of the HTTP methods means, how to tunnel through POST, common serialization formats, common query parameters, etc. Having an OData service won't negate the need for documentation &ndash; for instance, service consumers will still need to understand the domain and authentication models &ndash; but much of the documentation that is out there today **_could_** be generated from an OData service. More importantly, that uniformity is shared by service consumers that use an OData client. These consumers will be able to query, page, add/modify/delete and more without any additional effort.

### Other Problems with Ad-Hoc Data APIs

The problems presented by lack of uniformity extend beyond just documentation. Similar to the documentation requirement, ad-hoc data APIs are incapable of reusing frameworks or test code wisely, are unlikely to work with generic tools, and are frequently constrained to fewer deployment scenarios.

#### Framework reuse

Imagine for a moment a fictional world in which all data APIs share some degree of uniformity. In this world let's assume that there are a finite set of shared serialization formats, a shared understanding of what groups of objects are available and a shared understanding of how to implement the create, read, update and delete (CRUD) pattern. Given these constraints and a set of objects such as customers or movies, it would be possible to generate both the APIs and a set of tests that verify API functionality.

**TODO: MORE**

### Sidebar: How do developers consume ad-hoc data APIs?

How, then, do developers actually consume ad-hoc data APIs if they aren&rsquo;t able to or willing to read the documentation? Developers frequently turn to SDKs and interactive tooling to reduce the amount of time required to consume an ad-hoc data API.

Most of the well-known and widely used ad-hoc data APIs come with an SDK. Google offers a unified SDK for most or all of their APIs. Similarly, Windows Azure offers a unified SDK for several APIs. Facebook, Twitter, Yelp and other APIs all offer SDKs. In many cases these SDKs are offered in a number of different languages. SDKs go a long way toward reducing the amount of custom code required of developers to consume an API, but it&rsquo;s still custom code. And while these SDKs are extremely valuable, the fact is that they are frequently so low-level that developers still need to read too much documentation.

If an SDK isn&rsquo;t available, perhaps an interactive tool is available that provides developers a UI for building a syntactically valid request. These tools then frequently allow developers to supply their API key (or an API key for test data) that will enable the developer to send the request and see the format and structure of the response.

If neither of these options are available, developers frequently turn to basic HTTP debuggers to facilitate learning about the API. HTTP debuggers like Fiddler allow developers to both capture and inspect requests and responses as well as formulate full HTTP requests from scratch. The control these tools have over tweaking and inspection of HTTP payloads simplifies the process of learning an ad-hoc API.

## What about REST, SOAP and Other Technologies?&nbsp;

OData certainly doesn&rsquo;t have an exclusive claim to conventions in data APIs. There are an enormous variety of other technologies that have tried to meet the need for shared conventions. Among these technologies, two stand out from the crowd.

### REpresentational State Transfer (REST)

REpresentational State Transfer or REST, as it is better known, is simply an architectural style that specifies an optimal way to design data APIs for scalability and decoupling. The term REST was derived from a doctoral dissertation written by Roy Fielding in 2000. Although the dissertation was primarily concerned with describing &ldquo;a framework for understanding software architecture via architectural styles&rdquo;, the value for most readers has been Fielding's description of REST and its impact on HTTP and the Web as a whole. In his words:

&ldquo;REST emphasizes scalability of component interactions, generality of interfaces, independent deployment of components, and intermediary components to reduce interaction latency, enforce security, and encapsulate legacy systems.&rdquo;

#### A Formal View of REST

Section content goes here

#### A Layman's View of REST

Whether accurate or not, there are a number of readers who feel that there is plenty of room for interpretation in Fielding&rsquo;s dissertation. This has led to&nbsp;

#### Why REST Isn't Enough

It would be fair to say that many of the principles of REST are principles of uniformity. So why isn't it enough to say that we should just write RESTful APIs? There are two primary reasons why we need something more than RESTful principles. First, as Roy Fielding [points out](http://roy.gbiv.com/untangled/2008/no-rest-in-cmis), &ldquo;REST is an architectural style, not a protocol&rdquo;. Second, even if REST were a protocol there are too many conventions (purposefully) left undefined to provide significant uniformity.

To be fair, it was never the intention of REST to provide API uniformity. REST is a description of the architectural style used to build the modern Web and so it has implications for data APIs but was not primarily intended to make data APIs uniform. REST does, however, provide foundational principles that are useful in our quest for uniformity. For example, using hypermedia as the engine of application state ensures that data APIs consistently describe potential interactions with hypertext.

There are a significant number of conventions left undefined, however. Although this is by no means an exhaustive list, let's look at three examples:

1.  REST does not provide for any form of URI templating. In fact, true REST goes even further &ndash; as Fielding [says](http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven), &ldquo;A REST API should be entered with no prior knowledge beyond the initial URI (bookmark) and set of standardized media types that are appropriate for the intended audience&rdquo;.
2.  REST assumes that any mime type can be used to represent a resource. The problem with this assumption is that it effectively makes it impossible to write a framework or generic client as the framework or client would need to support every possible mime type.
3.  REST does not have any conventions for filtering, ordering or paging resource representations. These are common operations across sets of resources, but REST has little to nothing to say about them.
</section>
</section>

### Simple Object Access Protocol (SOAP)

Unlike REST, Simple Object Access Protocol (SOAP) is actually a protocol. As a gross simplification this means that SOAP defines a large number of conventions about how to consume data APIs. In fact, many of the experiences you can get with OData are similarly rich with SOAP. Conventions confer a number of advantages to a data API. While this is by no means exhaustive, three such advantages true of both OData and SOAP are as follows:

*   Frameworks: Since OData and SOAP are both protocols, developers can easily create a new OData or SOAP service using an existing framework. Frameworks frequently allow you to mark up existing code to create a data API with that protocol. This significantly reduces the up-front design and development costs.
*   Code generation: Both OData and SOAP services have tooling in popular integrated development environments (IDEs) that facilitate code generation. When a developer uses an IDE to add a reference to an OData or SOAP service, the IDE generates proxies that make it very easy to interact with the service.

Generic tooling: Both OData and SOAP services are able to work with generic information worker tools. Getting data from an API into these tools greatly extends the reach of your API.

#### Why SOAP Isn&rsquo;t Enough

You might be asking why SOAP isn&rsquo;t enough if it has so many of the same benefits as OData. The fundamental issue with SOAP is the architectural impact of how SOAP was designed. In _RESTful Web Services_, Leonard Richardson and Sam Ruby classify three common API architectures: RESTful Resource-Oriented, RPC-Style and REST-RPC Hybrid.

A RESTful, resource-oriented API typically uses the HTTP method to represent the operation the client wants to perform and the URI to represent the resource the client wants to perform the operation on. These are the two fundamental pieces of information necessary to interact with an API. In the author&rsquo;s words:

&ldquo;Given the first line of an HTTP request to a resource-oriented RESTful web service (&lsquo;GET /reports/open-bugs HTTP/1.1&rsquo;), you should understand basically what the client wants to do. The rest of the request is just details; indeed, you can make many requests using only one line of HTTP.&rdquo;

An RPC-style API, on the other hand, frequently puts both the operation the client wants to perform and the resource the client wants to perform the operation on in a message or envelope. This message is then sent to a single endpoint which unpacks the message, executes the desired operation, and pack up and sends back a response similar to the manner in which the request was sent. Unlike the RESTful-style API, an RPC-style API requires you to unpack the message or envelope in order to understand the request.

&ldquo;To a first approximation, every current web service that uses SOAP also has an RPC architecture.&rdquo;

## Building Blocks of OData

The OData protocol attempts to address this issue of uniformity in data APIs by building on a foundation of standardized protocols. This foundation provides a solid basis for addressing resources, sending requests and responses, and serializing payloads. As discussed earlier there are a number of additional areas that need to be addressed in addition to this foundation. We need a way to compose resource addresses. We need a way to specify filtering, sorting and paging operations. We need additional constraints around serialization. And finally, we need a common understanding of key points like what the various HTTP methods mean and how to publish metadata.

### URI Conventions

URIs are used to identify and locate OData resources. Each entity (identifiable resource) should have one canonical URI. The default URI conventions use URI composition to compose the resource path. To talk meaningfully about the default URI conventions, we need to touch briefly on a few OData-specific terms first.

*   Service Root: The entry point to or identity of the OData service. A GET to this URI should return a service document.
*   Entity Set: One of the values returned by the service document. All OData resources other than root level functions and actions must be accessed through an entity set.
*   Resource Path: The part of the URI between the service root and the query string. The resource path identifies a single resource or a feed of resources that share a common base type.
*   Key Literal: The representation of an entity's key in the URI literal format, surrounded by parentheses. E.G., (4) or ('a','b').
*   System Query Option: A canonical query option of the set defined in the OData protocol (e.g., $filter, $top, $skip). System query options are identifiable by the leading $ in the query parameter name.
*   Property: Any property of an entity or complex type in the model.

<div data-type="note">

# Helpful Note

Many of these terms are defined in more detail in _Chapter 3, The Metadata and Service Model of OData_.</div>

For instance, let's talk about a very basic model of a social graph. For the purpose of discussion, let's consider this very simple model:

<figure>![](images/simple_model.jpg)</figure>

Let's also assume that we have an OData service with the service root [http://social.example.org/api/](http://social.example.org/api/). The service root returns a service document containing an entity set named People for the Person entity type and an entity set named Photos for the Photo entity type.

OData URIs can address one of four things:

1.  A service document (a concept from AtomPub in which a document is served up indicating the next-level URIs). For many OData services, the service document will contain an entry for each entity set (a collection of entities).
2.  A collection of entities such as an entity set, or a property of an entity that contains a collection of entity, complex or primitive types.
3.  An individual resource such as an entity, complex or primitive type.
4.  A service operation like an action or function.

The address for the service document by definition is the service root. This means that the address for the service document for the model above would be [http://social.example.org/api/](http://social.example.org/api/). In our case a GET to this URI would result in a small service document that contains two collections: People and Photos.

The address for a collection of entities is built by composing the service root together with a navigation path through the service. All OData URIs other than the service root begin by addressing a collection or a service operation. The two most obvious collections in our service are People and Photos. If we compose the names of those collections with the service root, we get [http://social.example.org/api/People](http://social.example.org/api/People) and [http://social.example.org/api/Photos](http://social.example.org/api/Photos). GETs to these URIs will result in a collection of Person entities and a collection of Photo entities respectively.

The only way to navigate further than a collection is to address an individual member of the collection. With entity sets it is possible to address an individual member of the set by composing the collection URI with a key literal with the value of the desired member's key. For instance, let's assume that there exists a Person with the Id &ldquo;jimhawkins&rdquo;. The default URI conventions for OData would compose this value in the URI literal syntax with the collection URI, resulting in [http://social.example.org/api/People('jimhawkins')](http://social.example.org/api/People(). Similarly, [http://social.example.org/api/Photos(17)](http://social.example.org/api/Photos(17)) is the URI that identifies the Photo with the Id 17.

Additional navigation segments can be added to the URI for an individual resource. The OData specification does not place any limits on the number of navigation segments possible in a URI, which means that some servers will allow very complex URIs. In some cases the navigation will be simple. For instance, to get the Caption for the Photo with the Id 17, we simply compose the URI for the Photo together with the name of the property, which gives us [http://social.example.org/api/Photos(17)/Caption](http://social.example.org/api/Photos(17)/Caption). In other cases the navigation is more complex. Consider the case where we want to know who uploaded that photo. Like Caption, we simply compose the name of the property together with the URI for the photo: [http://social.example.org/api/Photos(17)/UploadedBy](http://social.example.org/api/Photos(17)/UploadedBy). This gives us another entity (a Person), which gives us additional navigation options.

Putting these two types of composition (from collection to single resource and from single resource to a property of the resource) together results in the ability to construct extremely complex and powerful URIs that identify OData resources. Consider some of the following examples:

*   [http://social.example.org/api/Photos(17)/UploadedBy/Name](http://social.example.org/api/Photos(17)/UploadedBy/Name) yields the name of the person that uploaded Photo 17.
*   [http://social.example.org/api/Photos(17)/UploadedBy/Photos](http://social.example.org/api/Photos(17)/UploadedBy/Photos) yields all of the photos uploaded by the person who uploaded Photo 17.
*   [http://social.example.org/api/Photos(17)/UploadedBy/Photos(21)](http://social.example.org/api/Photos(17)/UploadedBy/Photos(21)) yields Photo 21 if both photos were taken by the same Person (or a 404 if they were taken by different people).

&ldquo;When you write a client for an existing API, you&rsquo;re at the mercy of the API designer. I can&rsquo;t give you any general advice, because right now there&rsquo;s no consistency across APIs. That&rsquo;s why, in this book, I&rsquo;m trying to drum up enthusiasm for a little server-side consistency. When APIs become more similar to each other, we&rsquo;ll be able to write more sophisticated client-side tools.&rdquo;

## What is the Open Data Protocol?

The Open Data (OData) protocol is a set of conventions that allow service authors to rapidly build Web APIs that have a significant degree of uniformity. The high predictability of OData services enables generic frameworks (such as WCF Data Services) to expose or consume Web APIs. For instance, a Java developer can download and use the open source odata4j to consume an OData service built on top of WCF Data Services.