DIF FAQ
==================

**You Are Here (or should be):**
  [https://identity.foundation/faq](https://identity.foundation/faq)

Editors:
~ [DIF Staff](https://www.linkedin.com/in/dbuchner/)

Participate:
~ [GitHub repo](https://github.com/decentralized-identity/faq)
~ [File a bug](https://github.com/decentralized-identity/faq/issues)
~ [Commit history](https://github.com/decentralized-identity/faq/commits/master)

------------------------------------

## Abstract

This is a general-purpose frequently-asked questions document,
initiated/straw-manned by some regular contributors to the DIF Interoperability
Working Group, DIF Staff, and volunteers organized on DIF's member Slack.

## Layer 1: Identifiers and namespaces

<details><summary>
What’s the difference between decentralized identity and IAM? 
</summary><br>
Identity and Access Management tends to be associated with centralized hierarchies of delegation (i.e., the “Access Control List” approach, credentials that “phone home” to their issuer at each use, etc.). Cqentralized and/or “Federated” architectures are common in today’s IAM, but they are not inherent to IAM: many IAM companies are rolling out products and systems for managing and provisioning decentralized identities and/or verifiable credentials at enterprise scale. If those identities and credentials are portable and interoperable, that’s decentralized enough for this decentralized identity foundation!

> Using DIDs (Decentralized Identifiers) and VCs (Verifiable Credentials) does
> not automatically lead to decentralized infrastructure and decentralization of
> authority.
</details>

<details><summary>
DID methods: should I support just one or multiple?
</summary><br>
Most people presume only one DID method will be enough for a given product, use-case, or ecosystem, but consuming credentials from other DID systems requires at least a passive level of support (i.e., resolution), and being able to issue VCs to holders of multiple kinds of identifiers (including but not limited to other DID methods) requires considerable development work as well.  Options to support resolutions of several DID methods is either to build a full-featured, native/direct mechanism for each method or to use a variant or subset of the forkable, open-source, community-maintained [Universal Resolver](https://medium.com/decentralized-identity/the-universal-resolver-infrastructure-395281d2b540) project at DIF. There is a more nascent [Universal Registrar](https://github.com/decentralized-identity/universal-registrar) project for information about how to “outsource” CRUD on foreign DID methods to a trusted agent.
</details>

<details><summary>
How do I pick between DID methods?
</summary><br>
This is a very complex question, and one which DIF cannot give advice in a way that is neutral and fair to all its members. There are, however, a number of resources that might help.  One is the W3C DID working group’s [DID Rubric](https://w3c.github.io/did-rubric/) project for ranking the apples and the oranges against each other.

DIF Member Eric Welton presented at the January 2021 F2F a project called the
DID Method Dataset, which is a "Community Journalism" model. The idea there is
to set up google forms to mirror both the W3C DID Rubric as well as
"professional question sets" - the answers to these questions. one early
prototype looks like
[this](https://docs.google.com/forms/d/e/1FAIpQLSc0Dn9LrYBtqJ1t7eVHMzq2PsMGeJbYKfEYGuYEQXJeaFaGBQ/viewform).
Similar and cooperative/synergistic efforts are also underway at [Legendary
Requirements](http://legreq.com/).
</details>

<details><summary>
So if I were to design my own DID Method, where to start? How to approach the design?
</summary><br>
The open-endedness and extensibility of DIDs is liberating, daunting, and staggeringly complex. What can you put into a DID Doc? What are the tradeoffs? How do people protect or compensate for the privacy and security risks of putting more into the Doc? These are massive questions, way beyond an FAQ. A hopefully smaller question is whether the overhead and interoperability costs of creating a new method outweigh adapting an existing method: even if so, a thorough review of prior art can be eye-opening and fortify the design process anyways If you decide to design a new DID Method, DIF’s longest-running working group, Identifiers and Discovery, would be a good place to start. Skim the minutes of recent meetings for DID method design and specification topics, or just reach out to propose an agenda item at a future meeting.
</details>

<details><summary>
Certain use-cases are only possible given certain properties of a method/did:doc design. How do I find out which DID methods I should be looking at? 
</summary><br>
This is, again, too large a question for a one-paragraph answer. But understanding the requirements of a given use-case or problem space takes time and extensive research-- and neutrality. Try to read against the grain in marketing materials and arrive at your own conclusions about what different systems “optimize for”.

Here are some key coarse-grain categories and families of features on which DID
method differ significantly:
- Are VC’s completely “off-chain” or are hashes or pointers encoded in immutable
  storage of some kind?
- Are VC’s revocable? How?
- Does the DID layer support selective disclosure (including ZKP or specific forms of ZKP)?
- Does the DID layer include mechanisms for storing and referencing semantics
  (i.e. credential definitions)? Is it a required mechanism?
</details>

<details><summary>
Why aren’t x509 and DIDs compatible? Why aren’t DIDs and eIDAS compatible?
</summary><br>
They are! VCs are neutral and un-opinionated by design as to what kinds of identifier URIs are provided for issuer and holder identification. DID methods could be designed to use x.509 structures to manage key material for DIDs, or simply contain x.509 addresses in their DID:Documents.  For bibliography on eIDAS and DIDs, see the [Vienna Identity Meetup](https://www.thedinglegroup.com/blog/2021/3/11/eidas-and-self-sovereign-identity) and [SSI Meetup](http://ssimeetup.org) recordings on the subject.

Whether or not a specific x.509 system is decentralized enough, or private
enough, is up for debate-- but there is no technological conflict, and plenty of
work has been commissioned by governments around the world to align their
existing identity/transaction auditing infrastructures with this new paradigm
for verifiable credentials. 
</details>

<details><summary>
What’s the difference between a DOI or other “persistent identifier” and a DID?
</summary><br>
Digital Object Identifiers ([DOIs](https://www.doi.org/)) are the most famous form of persistent identifier, and differ in two main aspects from decentralized identifiers: on the one hand, they are very centralized, in that one global registry of all DOIs is maintained and governed by a non-profit called the International DOI Foundation or [IDF](https://www.doi.org/doi_handbook/7_IDF.html). On the other, they are static in both senses of the word: they are neither updatable/reusable nor interactive, which are the two main superpowers of DIDs.

There are, however, many more persistent identifiers, some of them less
centralized and some of them more interactive or dynamic. Indeed, a whole
community working with such “PIDs” exist, primarily in the fields of library
science, academic publishing, and other fields where unique identifiers and
namespaces for opaque identifiers are of paramount importance. For more
information about that other world, see Markus Sabadello’s article on our blog,
“[DIDs are PIDs](https://blog.identity.foundation/dids-are-pids/)”.
</details>

<details><summary>
What exactly is a SCID?
</summary><br>
Self-certifying identifiers are deterministically derived from public keys, such that they can be widely published and control of the public key from which they derive can be proven with its corresponding private key. They are "self-"certifying in the same way that DIDs generally require reading a blockchain or other verifiable data registry to certify-- the identifier itself, being a hash or other deterministic derivation of the public key, validates the public key. For this reason, some forms of SCID such as those used in KERI or Sidetree can be called “microledgers,” as explained in this [DIF blog post](https://blog.identity.foundation/keri--for-every-did--a-microledger/) about KERI. 

See also this [glossary
entry](https://github.com/decentralized-identity/keri/blob/master/docs/Glossary.md#self-certifying-identifier)
or an [early
paper](https://github.com/WebOfTrustInfo/rwot7-toronto/blob/master/topics-and-advance-readings/ZeroTrustComputingWithDidsAndDads.md)
by Sam Smith. There is also a very concise and clear contradefinition of SCIDs,
DIDs, and traditional PKI in section 3 of the DID chapter by Markus Sabadello
and Drummond Reed in **Self-Sovereign Identity** (Manning Press, 2021), from
which the following illustration is taken:

![diagram of SCID, DID, and PKI conceptual boundaries](https://user-images.githubusercontent.com/37127325/116748222-f899c800-a9b3-11eb-923a-0b605b6bc339.png)

Src: https://livebook.manning.com/book/self-sovereign-identity/chapter-8/v-2/139 
</details> 

## Layer 2: Agent Frameworks

<details><summary>
What are agent frameworks? How big, how broad, or even how small can they be? Do we need them? Or just enough modules that work together?
</summary><br>
One way of thinking of agent frameworks is that they encompass confidential/privacy-preserving equivalents to many of the “invisible” layers of the internet stack that we non-specialists rarely think about or even know by name: Content Delivery Networks (CDNs), service workers, replication and redundancy services, network routing. Agent frameworks allow lightweight frontends like single-page apps or decentralized apps (dApps) to interact directly and discretely with each other and verifiable data registries while exposing less information and correlation risk than if they went through conventional clouds and server infrastructures.

There are many use-cases where agents bring more complexity or performance issues than they are worth; they are particularly well-suited to human-identity use-cases, high-privacy use-cases, and large ecosystems that are homogenous in terms of decentralized identity tooling and formats. 
</details>

<details><summary>
Do existing agent frameworks have some simple overview documentations I can peruse to compare them? Getting close to interoperability? Or inspiration?
</summary><br>

- Aries currently has four major “Agent Frameworks” (“Acapy”(Python), AriesGo,
  AriesJS, Aries.NET) 
- See the [Aries Interop Info site](https://aries-interop.info/) for automated
  testing harness and results and see a good (BC-gov-focused) Discussion of
  Aries can be found
  [here](https://docs.google.com/document/d/1JmPh7X1-MNl_EuIVUodf1hWHTrt4vLvFT1N_lAjfoEQ/edit#heading=h.g1t45w61ipue)
- Microsoft's Authenticator framework portal and
  [overview](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---16-dec-2020---usapac-time-1400-pt---vc-deep-dive-series-a-vc-focused-tour-of-the-authenticator-architecture-with-tim-capalli-msft)
  (aka "just-in-time issuance")
- Consensys's Veramo portal and
  [overview](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---20-jan-2021---useu-time-0600-pt---tour-of-the-os-veramo-suite-from-consensys-meshdaf-team)
  (aka "Aries Agent+ for Ethereum")
- [Affinidi](https://www.affinidi.com/developers)/Bloom - [Portal](https://www.affinidi.com/developers) 
- Spruce [Portal](http://spruceid.dev) 
- Mattr Platform ([launch
  blogpost](https://mattr.global/introducing-the-mattr-platform/))

&nbsp;
</details>

<details><summary>
How can I choose between frameworks? This feels like an even bigger commitment than a choice of DID method.
</summary><br>
It might in fact be a bigger commitment! That said, many frameworks listed above are deliberately modular and open-ended, allowing not just forking and customization, but even recombination between them. Frameworks are not as binding as they were a year ago, and will likely be even less so a year from now: they are a growth hack and a means to greater decentralization, in the long view.  Open source is all about trust, after all!

</details>

<details><summary>
Is it smart to try to make one agent/framework to rule them all?
</summary><br>
No one is trying to make that! Agent frameworks have varying degrees of interoperability planned on their published roadmaps, and many will likely support DIDComm, Presentation Exchange, and other common protocols at *some* level, for inter-framework VC exchange and other interoperability/cross-auditing purposes. See discussion of this topic [here](https://docs.google.com/document/d/1O3A0MSSKmVJVPUotFE2H7kGbB4WuBjw1ELHBcer2F3E/edit).
</details>

<details><summary>
Are there any agents that is flexible outside their domain today?
</summary><br>
So far, verification of "foreign" VC formats (and "representations") from other systems has been slow to be fully integrated into frameworks, but great progress is being made-- DIF is optimistic that this answer will have to be completely rewritten by 2022. DIF member Animo Solutions has built LD VC support into Aries Cloud Agent Python (and hopefully the other Aries agents will soon follow suit).  Furthermore, DIF member [Bloom](https://bloom.co/) has been driving some [WACI work](https://github.com/hellobloom/waci-demo) on top of the Presentation Exchange specification to facilitate the initiation and negotiation of exchanges, which is feeding into a new C&C work item, which might well pave the way to full VC-HTTP-API support across frameworks.
</details>

<details><summary>
What exactly is a “connection”? Is it a transport? Can I exchange VCs over one?
</summary><br>
“Connection” is very much an Aries-centric concept: it is an abstraction of a relationship between two identifiers/data subjects, first described in an [Aries RFC](https://github.com/hyperledger/aries-rfcs/blob/master/features/0160-connection-protocol/README.md). A more generic version of the concept is included in the [Universal Wallet draft specification](https://w3c-ccg.github.io/universal-wallet-interop-spec/#connection) at W3C-CCG, for the sake of portability and equivalences. A little further afield of the SSI world proper, in the ActivityPub community which develops tooling for bottom-up/community-driven federated social media and micropublication systems, there is also a related notion of “[pet names](https://socialhub.activitypub.rocks/t/petnames-gui/1066)” that may be of interest to connection & UX researchers: these are local aliases for opaque/privacy-preserving identifiers, with certain best practices and privacy models baked in.

Technically, one does not exchange VCs over a “connection,” even if the process can be described colloquially using this construction. Instead, an Aries connection is how exchange protocols are initiated and expressed to an end-user; for the actual mechanics of transport protocols, see the relevant [subprotocols](https://github.com/hyperledger/aries-rfcs/blob/master/features/0160-connection-protocol/README.md#0-invitation-to-connect) and Aries RFCs.
</details>

<details><summary>
Key management: what are the pro's and con's to custodial approaches? What recovery options exist today? Are end-users ready for a private-key based future?
</summary><br>
Product Managers had a [stellar session](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-10th-2021) about this last week, which is being continued next week. Much like "connections", there is very little starting point for a universal standard, and most blockchains try to tackle this problem from one angle or another so universalizing is very tricky but there are definitely ways to align without boiling the ocean.
</details>

## Layer 3: VC Infrastructure

<details><summary>
Are there different “types” or “formats” of VCs? Are they incompatible?
</summary><br>
There are 4 major “representations'', which are not exactly “formats” in the sense that word documents or PDFs are a “file format,” but rather more like 4 encoding systems from 4 different operating systems or file systems. They have slightly different relationships to external semantic anchoring, which makes translating *losslessly* between them or “roundtripping” a very tricky, but not impossible, technical problem. Most of today’s solutions opt to translate with a little loss if it is acceptable to their usecases. DIF Interop WG has hosted a lot of conversations on this topics, and Kaliya Young's recent [article about exactly this](https://www.lfph.io/wp-content/uploads/2021/02/Verifiable-Credentials-Flavors-Explained.pdf) was crowd-edited on a [very special episode](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---13-jan-2021---usapac-time-1400pt---communications-problem-explaining-the-vc-format-wars-to-decision-makers). The article is definitely the best place to start further reading. 
</details>

<details><summary>
These things are revocable, right?
</summary><br>
Actually, most VC systems currently have limited revocation capabilities, as they add significant scaling costs and complexity. Different use cases justify different approaches to revocation (including none at all).  Martin Riedel's overview of approaches to revocation/status mechanisms at interop [in February](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---10-feb-2021---usapac-time-1400pt---revocation-method-comparison) was really helpful in introducing these approaches at a high level, and a series of events in the months since have explored the topic further; see the Interop WG notes for more [details](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md).
</details>

<details><summary>
I’ve never used JSON-LD and I get confused by all this LD talk. Can you explain it to me like I’m 5? What’s the difference between a JSON-LD “Context”/Vocabulary, the traditional “Data Schemata” I use every day?
</summary><br>
Traditional data schemata are used to express (and thus validate against that expression) the **syntax** of data objects-- the type, length, form, presence/absence, etc of values in the key/value pairs that make up most data structures. The primary function of JSON-LD contexts is to express the **semantics** of the keys, not the values-- they facilitate the translation between schemata or systems and the reconstruction of lost or foreign contexts in which data can have meaning.
</details>

<details><summary>
That sounds hard, and/or I don’t think my boss/investors/CISO would like that. Is JSON-LD the only way to express semantics? Do I have to use JSON-LD to use VCs?
</summary><br>
There are other systems for expressing semantics for data, such as the young IETF standard [JSON-Schema](https://json-schema.org/learn/getting-started-step-by-step.html) which does not require keys to be defined against public definitions and that does not require the immutable publication of contexts. This simpler and easier for some use cases but may inhibit interoperability with LD-based systems and the vocabularies of organizations like the W3C and GS1. Like LD Schema, it requires special linters and validators, which can be found in the [JSON Schema Section](https://extendsclass.com/json-schema-validator.html) at extendsclass.com . DIF work items like the [Credential Manifest](https://identity.foundation/credential-manifest/) use JSON Schema extensively.

Also, the low-level VC libraries in the Aries ecosystem abstract out much of the complexity specific to LD and semantic anchoring. See [RFC47](https://github.com/hyperledger/aries-rfcs/tree/master/concepts/0047-json-ld-compatibility), [RFC250](https://github.com/hyperledger/aries-rfcs/blob/master/concepts/0250-rich-schemas/README.md), Implementer’s Call [Notes 12-17-20](https://wiki.hyperledger.org/display/IWG/2020-12-17+Identity+Implementers+WG+Call), and the archives of the AriesGo framework [discussion channels](https://wiki.hyperledger.org/display/ARIES/aries-framework-go), where much low-level JSON-LD work has taken place; to expand Aries support for JSON-LD, check the [Code With Us](https://digital.gov.bc.ca/marketplace/opportunities/code-with-us/3f9f0e86-b8bf-47ee-9f3d-5b272f9ec845) for open grants.
</details>

<details><summary>
Where do “Credential Definitions” fit in?
</summary><br>
The core VC libraries of the Hyperledger Aries project work on a kind of hybrid “credential definition” that includes both semantic and syntactic definitions of what can go into a given VC called a [Rich Schema](https://github.com/hyperledger/aries-rfcs/blob/master/concepts/0250-rich-schemas/README.md). VCs are not only validated against these definitions, but the CL-ZKP algorithms available in the same libraries also use the definitions to allow for verifiable selective disclosure of subsets of credential data via “framing”-- this process requires the definition as one of the inputs, however, so Indy-conformant credential definitions must be used. These have historically been written to the Indy blockchain, but other forms of immutable/highly-available storage are being pioneered in the Aries ecosystem.
</details>

<details><summary>
How do I interpret credentials that require validating them against JSON-LD Contexts? Should I be scared?
</summary><br>
Fetching new contexts and revocation lists at runtime is generally frowned upon and could raise serious privacy and security issues in a production environment; for this reason, JSON-LD, like most graph-model data systems, makes extensive use of caching, pre-loading, and periodically refreshing its dependencies to build a “local graph.” One crucial building-block in such a secure pre-loading system specific to the JSON-LD concept of a “document” is the “document loader” described in many specifications and tutorials on how to build for JSON-LD verification. DIF hosts a general-purpose reference [implementation](https://github.com/decentralized-identity/jsonld-document-loader) of such a tool, and its donator, Orie Steele of Transmute Industries, gave an overview of [why and how to use it](https://youtu.be/-yUbMDft5O0) at DIF Interop WG.
</details>

<details><summary>
How do I make my own JSON-LD Context?
</summary><br>
Basically, the process of creating schemata (whether for syntax, for semantics, or both) is best thought of as a *recombinatory* process-- mixing and matching composable prior art and adding properties or methods to existing building blocks is the name of the game, and the more you can recycle or use common building blocks, the better. Developers often refer to this as “extending classes,” i.e. adding properties and methods to a pre-existing object.

Most schema development for JSON-LD projects (whether for shape, for semantics, or both) starts with a bit of reading on Schema.org’s [reference shelf](https://schema.org/docs/documents.html) and search function results, or a few other major ontologies/contexts like the [HeppNetz Good Relations ](http://www.heppnetz.de/projects/goodrelations/)vocabulary for e-Commerce or the [EPCIS ](https://www.gs1.org/epcis/epcis/1-1)standard for describing business processes and events. Once you have a skeleton that maps *most* of the relevant data for your use case in standardized terms, you’re ready to start extending!
</details>

<details><summary>
Where do your extensions live, tho? 
</summary><br>
Extensions can remain specific to a given project if your project hosts its own vocabulary extending standard one, or (with appropriate resources and timelines) you can propose your extensions “to origin” at [schema.org](https://schema.org/docs/extension.html) or elsewhere. When self-hosting, remember to configure your web server to serve LD files as MIME-type json+ld (you might also want to get fancy with [versioning redirects](https://github.com/w3c-ccg/vc-http-api/pull/158#issue-588951741) like /latest/ and /next/)
</details>

<details><summary>
Can a VC be signed by two or more parties? How do I produce and consume multi-signed VCs?
</summary><br>
Yes! The VC spec is actually fairly open on this issue, and Markus Sabadello gave a [great presentation](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---3-feb-2021---useu-time-0600-pt---update-on-did-core-and-enterprise-ethereum-alliance-d-burnett-and-did-interop-fundamentals-markus-sabadello-and-guests) at DIF Interop in January of 2021 laying out two major schools of prior art here-- how and when to produce each, and how to verify both.
</details>

<details><summary>
What is ZKP? What is the difference between ZKP and “Selective Disclosure”?
</summary><br>
Zero-Knowledge Proofs refers to a mathematical construct, which is at the heart of many cryptographic systems such as the control privacy-preserving mechanisms in such "blinded transaction" blockchains as ZCash. It refers to mathematical or data operations, not to high-level protocols such as credential exchange or proofing claims or real-world exchanges.

Selective Disclosure, on the other hand, refers to real-world exchanges or information exchanges.  In the VC context, presenting information contained in a verifiable credential selectively, in a way that still allows the credential as a whole to be cryptographically proofed and verified, usually relies on some form of ZKP cryptography.  There are different styles of ZKP and different styles of Selective Disclosure, so it helps to be precise about exactly which kind you are talking about, as they all have distinct properties and guarantees, scalability issues, etc. 

In the decentralized identity world, the most common selective disclosure mechanisms (each with their own distinct Verifiable Presentation mechanisms!) are:

- CL-ZKP (the CL stands for [Camenisch-Lysyanskaya](https://www.youtube.com/watch?v=K6s4ENTfcWw), the last names of the two designers), which powers Indy and Indy-based systems' VP capabilities; the bulk of this work has been driven by DIF member Evernym.
- BBS+ (See Mattr's [Introduction](https://mattr.global/using-privacy-preserving-zkp-credentials-on-the-mattr-platform/), [AMA](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---18-nov-2020---usapac-time-1400-pt), and test-suite PR in the VC-HTTP-API ([144](https://github.com/w3c-ccg/vc-http-api/pull/144#discussion_r590342533)) for background); many DIF members have also pioneered the work, including Trinsic and SecureKey. 
- Microsoft Research has been building up ZKP capabilities based on an unrelated third form of cryptographic tradition known as "[fuzzy vaults](https://medium.com/decentralized-identity/building-interoperable-zkp-credential-systems-70bc20a8a809)," but a VP implementation based on it is still forthcoming. 

</details>

<details><summary>
What is the relationship between DIDs and VCs?
</summary><br>
Technically, there is none! VCs work great with DIDs used as the identifiers for issuer and verifier, but they also work with many other kinds of identifiers (Solid addresses, centralized and local identifier schemes, blockchain/smart-contract addresses, etc). DIDs can be used for all kinds of verifications, which is why the "verification method" system of associating multiple keys of different types with each DID is so flexible; signing VCs is only one of many purposes.  That said, the designers of both always had the other front-of-mind, and the complementarity of design thinking is hard to deny or overlook.
</details>

## Layer 4: Apps, UX, and Wallets

<details><summary>
How can UX design be flexible but still privacy-preserving when allowing users to combine, link, or co-present VCs issued to different DIDs?
</summary><br>
There’s not a lot written about this or prior art!  If you know of any please open a PR against this answer using the github link at the top of this document. If you are working on such a project, please contact the [product managers](https://lists.identity.foundation/g/id-productmanagers) group and present the project for feedback!
</details>

<details><summary>
How can key management be made usable for "normal" end-users?
</summary><br>
DIF Executive Director Rouven Heck led a fascinating [two](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-10th-2021)-[part](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-24th-2021) discussion of this topic at Product Managers, which overviewed the problem space quite well and provided lots of further reading and links. 
</details>

