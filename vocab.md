# xAPI Controlled Vocabulary

A controlled vocabulary is a formal list or authority file that contains terms for a subject area domain or specific taxonomy purpose.  An xAPI controlled vocabulary is a restricted, agreed-on list of terms and their meaning, developed intentionally by an xAPI Community of Practice (CoP). The objective of an xAPI controlled vocabulary is to promote canonical design, development, and implementation of xAPI statements to avoid ambiguity and ensure semantic interoperability. It is controlled because only terms from the list may be used for the subject area or domain. It is also controlled because, if it used by more than one person, there is control over who adds terms to the list, when, and how to the list. The list could grow, but only under defined policies by a CoP. The purpose of this document is to provide a basic template for generating a list of terms intended for inclusion in each CoP’s controlled vocabulary.

## Verbs
The Verb in an xAPI statement describes the action performed during the learning experience. The xAPI specification does not specify use of any particular verbs. Instead, it states that CoPs can establish verbs that are meaningful to their members and can optionally make them available for use by the public. In an xAPI statement, verbs have unique identifiers that reference a controlled vocabulary accessible at an IRI location to assist in disambiguation. However, additional human-readable metadata for each verb term is required to assist with properly understanding their intended use within a controlled vocabulary. A definition, authoritative source, and intended usage of the verb “passed” are needed to clearly understand the term and its actual origin. For example, exact definitions from WordNet (a lexical database) could be referenced as an authoritative source as it provides multiple definitions of “passed.” For example, WordNet defines “passed” as “to go successfully through a test or selection process,” and as  “an action that involves one player throwing a ball to a teammate.” Verbs are the hinge in an xAPI statement; they are the key property identifying the action in xAPI statement queries. Therefore, it is critical that a controlled vocabulary clearly specify how a particular set of verbs should be used. 

The following metadata should be agreed upon by the CoP and entered into the tables below as a working document for your controlled vocabulary list of verbs. An example verb term, “passed” is provided in the first of the table below.

### Verb Term:
The name of the verb term your CoP would like to translate and formalize as part of your domain’s controlled vocabulary. Each verb definition must correspond to the meaning of a verb, not the word. The verb entered into this column will represent the actual verb used in an xAPI statement by your CoP. 

### Verb Description:
The formal meaning or definition of the verb term. This description should be derived from an authoritative source.

### Authoritative Source:
The authoritative source is an externally referenced lexical database, dictionary, thesauri, or glossary of terms that provide a formal meaning for each verb definition in a controlled vocabulary. The authoritative source is considered to be a key informant of disambiguation and provenance information for each verb definition. 

### Usage:
The usage provides further context about the expectations and intent of how the verb might be used in a particular use case or scenario.

### Open Badges CoP xAPI Verbs
Verb Term | Verb Description | Authoritative Source | Authoritative Source URI | Usage
--- | --- | --- | --- | ---
Earned | gain a badge in return for one's behaviour or achievements | Mozilla Open Badges | http://openbadges.org/earn/ | Used to show that a user earned a badge.
Issued | supply or distribute a badge  | Mozilla Open Badges | http://openbadges.org/issue/ | Used to show that a user issued a badge.

## Activities
The Object in an xAPI statement describes what has been acted upon as a result of the experience. An Activity is the most common type of object in an xAPI statement. It can be a unit of instruction, learning experience, or performance-based activity that is intended to be recorded in a meaningful combination with a Verb. Interpretation of Activity is broad, meaning that Activities can even be real-world objects, digital objects, or non-digital objects. For example, a  printed quiz is an example of a real-world object whereas an online quiz would be an example of a digital object. 

The following metadata should be agreed upon by the CoP and entered into the tables below as a working document for your controlled vocabulary list of activities. An example activity term, “assessment” is provided in the first of the table below.

### Activity Term:
The name of the activity term your CoP would like to identify and formalize as part of your domain’s controlled vocabulary.

### Description:
The formal description and characteristics of the activity. 

### Resource Type:
The resource type column should specify whether the activity is an information resource or a non-information resource (source: Google Guide to RDF).  A resource is anything that can be defined and which can be assigned an identifier. As a matter of convenience, resources can be divided into two categories:

1. information resource - A resource for which all essential characteristics can be transmitted in a message (i.e. a digital resource). Historically, information resources have been the primary focus of the Web. When most users enter a URL into a web browser, they assume that the result will be the return of an information resource in the form of a digital file. Examples: html web page, digital image, pfd file.
2. non-information resource - A resource that cannot be transmitted electronically. Non-information resources can be further subdivided into the following categories:

  1. physical resource - a material thing. Examples: an animal, a specimen, a 35 mm slide
  2. abstract resource - a non-material, non-electronic thing. Examples: a taxonomic concept, a relationship, a determination

### Context Activities:
Context activities represent the level of granularity and relationship to other contextually relevant Activities. This metadata will also help identify the details supporting the context object when later constructing xAPI statements. This information entered in this column may provide a direct mapping to the properties of the contextActivities property for the Context Object in the xAPI specification.

### Produces Result:
The produces result column states whether the activity will produce a result (yes or no), and the properties that should be expected. This metadata will also help identify the acceptable outcomes when later constructing xAPI statements. This information entered in this column may provide a direct mapping to the properties of the Results Object in the xAPI specification.

### Open Badges CoP xAPI Activities
Activity Term | Description | Resource Type | Context Activities | Produces Result
--- | --- | --- | --- | ---
- | - | - | - | -

## Primary POC: 
[Ben Betts](mailto:ben@ht2.co.uk)

## Members:
*[Repository Contributors](https://github.com/ht2/BadgesCoP/graphs/contributors)*
