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

## Usage guide: How did I get here? Who are you?

This is a general-purpose collection of frequently-asked questions,
initiated/straw-manned by some regular contributors to the DIF Interoperability
Working Group, DIF Staff, and volunteers organized on DIF's member Slack. Each
question can be clicked on to expand and contract its answer. It is not now and
likely will never be an exhaustive reference, but rather a broadly-useful
resource to help people understand what they don't understand, find their
people, get involved in the best possible place, and level-set with their
interlocutors there.

Speaking of level-setting, each question is marked with 1, 2, or 3 stars based on
the level of familiarity they assume. Here is the key:

|Symbol|Meaning|
|---|---|
|⭐|Q&A requiring little technical background|
|⭐⭐|Q&A for the moderately tech-savvy software developer or industry insider|
|⭐⭐⭐|Q&A for the dedicated identity geek or guru|
|🌶|Controversial topic|

One strategy for learning is to read through in three separate passes, i.e.,
expand and read all the 1-star questions first, then reload the page and do the
same for all the 2-star questions, then the 3-stars. They are not sorted by
level because they progress down rabbit holes, and are intended to be readable
in various orders. If you don't understand the placement of chilis warning you
about triggering, controversial topics, don't worry-- understanding the
controversies is level 4.  When you not only understand why all those chili are
there, but furthermore feel torn and sympathetic to all parties in each
controversy, you're at level 5-- and should maybe think about chairing a working
group or joining one of the Steering Committees?

You may be wondering what the high-level categories on the sidebar mean: they break down the terrain of decentralized identity into broadly-defined "layers". This can be a little "inside baseball" at first, but with time, the utility and consequence of this layering should become apparent. It originated in the DIF Interoperability WG's months-long iterative discussion on interoperability and integration with prior art, which in turn built on Executive Director Rouven Heck's iteration on the ToIP 4-layer paradigm.

<details><summary>
See the simplified 4+1 layering diagram 
</summary>

![](assets/map.png)
Src: [Hakan Yildiz, Technische Universität Berlin](https://github.com/decentralized-identity/interoperability/blob/master/assets/interop-mapping-version-by-Hakan-Yildiz(TUB).pdf); [more detailed version](https://github.com/decentralized-identity/interoperability/raw/master/assets/interoperability-mapping-exercise-10-12-20.pdf)
</details>


This mini-site was made using [Spec-Up](/decentralized-identity/spec-up/), DIF's
in-house spec-authoring tool that consumes GitHub-flavored Markdown (with a few
additional bells and whistles) and publishes JS-enabled HTML to a github pages
branch. Please use issues to request minor changes or new sections, or PRs if
you are proposing both questions AND respective answers.

## Layer 0: Introductory Concepts

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What's a DID? What's a DID Document?
</summary><br>
In short, it's a username on the internet that you own. A connected DID document contains extra info that describes you.<br><br>

The most "decentralized" of the identifiers are so-called "decentralized
identifiers," or DIDs. These are each registered and resolved on autonomous
"namespaces" (see below), which are often closely coupled to specific
public-readable DLTs like blockchains that, by publishing addressing records
immutably, function as "verifiable data registries" for their specific kind of
identifiers. 

Each DID is prefixed with a reference to, and only guaranteed to useful,
meaningful, and reliable within, one DID namespace. Each "namespace" (addressing
system) is navigated with and governed by a "DID Method." 

</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What's a DID "Method"?
</summary><br>
In short, if you type your DID username in a browser, it's the method that's going to handle your request.<br><br>

Each DID is a publically-specified micro-protocol containing namespace rules,
CRUD and resolution mechanics, references to all dependencies such as
standardized cryptographic signatures schemes, and sometimes even models and
algorithms specific to one set of infrastructure such as a blockchain protocol
governed elsewhere. Each "DID method" has unique characteristics and
infrastructures, with particular strengths and weaknesses; even their security
guarantees and privacy engineering vary widely, so it can be dangerous to assume
they are all equal and interchangeable. Each is like a little internet unto
itself!

> Each "DID method" encodes and specifies a set of interdependent governance,
> publication, and discovery mechanisms for DIDs in a given DID namespace.

**Namespace** here means a universe of possible names, each of which is unique and
ideally as collision-free as possible, and in most cases completely opaque
and/or non-human-readable. 

</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; Who governs and maintains these "DID Methods"? How can I learn how a given method works?
</summary><br>
In short, there's a [list](https://w3c.github.io/did-spec-registries/#the-registration-process) of systems that are nicely specified how you can use them.


All methods are expected to be maintainers of systems and infrastructure that
are built on top of them. They are each specified by a published, registered,
and ideally well-maintained **specification**. This specification explains how to
validate a DID (namespace rules), where to query and what to expect back when
resolving a DID, etc. The
[registry](https://w3c.github.io/did-spec-registries/#the-registration-process)
of compliant specifications for DID Methods is maintained by a dedicated W3C
working group, currently the [DID-core WG](https://w3c.github.io/did-core/), and
at some point, this will be passed on to another WG when it dissolved, most
likely whichever maintenance group will maintain the DID specification itself.


</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; Are there sub-categories of DID "Method" that I should know about?
</summary><br>

Absolutely! A DID is any address that can be turned into a usable DID Document,
and there are many drastically different ways of doing this that can confuse
beginners by all being grouped under the broad category of DIDs.  For example,
most DID methods use blockchains or other publicly-readable verifiable data
registries directly (or indirectly, in the case of "layer 2" systems based on
DIF's [Sidetree Protocol](https://identity.foundation/sidetree/spec/) ) but
some, such as [`DID:Web`](https://w3c-ccg.github.io/did-method-web/), use other
systems of verification, such as TLS-secured DNS resolution. There are also
"deterministic" DID methods like [`DID:key`]() and `DID:pkh` that produce a DID
Document without any verifiable registry from a pre-existing public key for
interoperability purposes, and "off-chain" or "ephemeral" methods like
[DID:Peer](https://identity.foundation/peer-did-method-spec) that produce a
single-use, private DID Document corresponding to private keys generated at
runtime for private connections. DID:Peer DIDs are integral to DIDComm, which is
one key way to allow routing and messaging across these addressing systems en
masse rather than having to resolve them one by one and figure out routing and
messaging based on their various privacy, discovery, routing, and security
properties.

An emerging category of DID-like things is AIDs, or Autonomous Identifiers,
which do not depend on a verifiable data registry to be trustworthy, instead
maintaining and deliverying their own "self-certifying" DID Document. The most
famous of these are the identifiers in the [KERI event-log
system](https://github.com/decentralized-identity/keri), but others are on the
horizon, and the share many properties with the more self-certifying variants of
the Sidetree protocol.  AIDs can be considered a special category of DIDs, but
the exact "tunneling" mechanism for making an AID out of existing DIDs from
other namespaces and other equivalences and bridges are still in progress so
they are not quite 100% interoperable yet. Luckily for DIF, this work is
happening here!

</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What are Verifiable Credentials ("VCs"), exactly?
</summary><br>

Verifiable Credentials combine properties and superpowers from many different
mental models and forms of prior art; Linked Data, JSON Web Tokens, Ontologies,
ETL systems. They are like portable, free-floating data points, which are not
exactly documents or files or "records" in the usual sense. They are signed and
thus tamper-evident, and thus share much of the verifiability of blockchain data
or signed PDFs insofar as the signatures they contain can be properly verified
by reference to the identities included inside the document.  For the different
categories or "flavors" of VC, see Layer 3 below.

</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What is a wallet?
</summary><br>

Controlling, updating, and proving control of a DID (or, for that matter, a
cryptocurrency address, an NFT, or many other kinds of digital assets) requires
a private key, which isn't very secure or useful if copies of it are drifting
around the open web like flotsam. For this reason, private keys are managed by
specialized software generally called a "wallet" or an "authenticator", since
they have to do complex, high-security operations to avoid leaking private keys
while still producing unique signatures with those private keys every time proof
is needed that they possess them (in different context, these private-key
operations can be called "signing", "authentication", "interactive proof", etc).

In the identity context, however, a wallet can also store and present VCs, which
require proof of control of a private key to be considered verifiable at a given
point in time. For this reason, cryptocurrency wallets (that only manage control
keys for cryptocurrency accounts) are usually distinguished from identity
wallets (that control keys for receiving and verifiably presenting verifiable
credentials).  That said, there is no good reason one wallet couldn't do both,
and some day soon they probably will! See the Layer 4 section for more detail on
wallets in general and the Universal Wallet in particular.

</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What’s so `decentralized` and `self-sovereign` about these abstract-sounding
identity tools? 
</summary><br>

Each "DID Method" represents the governance and groundrules of a
variously-decentralized addressing system. In the most decentralized of these,
addresses can be generated and/or registered confidentially by any party, as on
public blockchains; in all, some amount of independence, confidentiality, and
privacy is guaranteed in the registration process. Regardless of how access to
registration of them is gated, DIDs are like email addresses or URLs, except
they return key material for encrypted communications and data operations. Thus,
they enable decentralized communications and identity operations that might
otherwise be hard to build from the ground up.

Verifiable Credentials have two superpowers-- **verifiability** (they are
digitally signed in a tamperproof way, like a signed PDF, which can be verified
independently of and privately from the signer) and **portability** (they are
designed to be interpretable outside of their original context, and contain
mechanisms for reconstructing and interpreting that context independently as
well).  

These two building blocks (decentralized addressing/identifiers and portable
data verifiable in a decentralized way) enable new ways of representing and
protecting human identity in the digital world, which is referred to as
"self-sovereign" in many circles. More generally, though, non-human identities
can also be decentralized using the same tools, which are also in scope of this
Foundation.

> Using DIDs (Decentralized Identifiers) and VCs (Verifiable Credentials) does
> not automatically lead to decentralized infrastructure and decentralization of
> authority.
</details>

## Layer 1: Identifiers and namespaces

<details><summary>
⭐⭐ &nbsp;&nbsp; What’s the difference between decentralized identity and IAM? 
</summary><br>

Identity and Access Management tends to be associated with centralized
hierarchies of delegation (i.e., the “Access Control List” approach, credentials
that “phone home” to their issuer at each use, etc.). Cqentralized and/or
“Federated” architectures are common in today’s IAM, but they are not inherent
to IAM: many IAM companies are rolling out products and systems for managing and
provisioning decentralized identities and/or verifiable credentials at
enterprise scale. If those identities and credentials are portable and
interoperable, that’s decentralized enough for this decentralized identity
foundation!

> IAM can be more or less decentralized, and decentralized tools can be used to
> centralized ends. Technological decentralization doesn't guarantee
> decentralization of business models or power structures in the real world! And
> it might not even be a good thing if they did. 🌶
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; DID methods: should I support just one or multiple?
</summary><br>

Most people presume only one DID method will be enough for a given product,
use-case, or ecosystem, but consuming credentials from other DID systems
requires at least a passive level of support (i.e., resolution), and being able
to issue VCs to holders of multiple kinds of identifiers (including but not
limited to other DID methods) requires considerable development work as well.
Options to support resolutions of several DID methods is either to build a
full-featured, native/direct mechanism for each method or to use a variant or
subset of the forkable, open-source, community-maintained [Universal
Resolver](https://medium.com/decentralized-identity/the-universal-resolver-infrastructure-395281d2b540)
project at DIF. There is a more nascent [Universal
Registrar](https://github.com/decentralized-identity/universal-registrar)
project for information about how to “outsource” CRUD on foreign DID methods to
a trusted agent.
</details>

<details><summary>
⭐⭐⭐How do I pick between DID methods?
</summary><br>

This is a very complex question, and one which DIF cannot give advice in a way
that is neutral and fair to all its members. There are, however, a number of
resources that might help.  One is the W3C DID working group’s [DID
Rubric](https://w3c.github.io/did-rubric/) project for ranking the apples and
the oranges against each other.

DIF Member Eric Welton presented at the January 2021 F2F a project called the
DID Method Dataset, which is a "Community Journalism" model. The idea there is
to set up google forms to mirror both the W3C DID Rubric as well as
"professional question sets" - the answers to these questions. one early
prototype looks like
[this](https://docs.google.com/forms/d/e/1FAIpQLSc0Dn9LrYBtqJ1t7eVHMzq2PsMGeJbYKfEYGuYEQXJeaFaGBQ/viewform).
Similar and cooperative/synergistic efforts are also underway at [Legendary
Requirements](http://legreq.com/). Also, researchers from [SBA
Research](https://www.sba-research.org/) in collaboration with DIF Member
[Danube Tech](https://danubetech.com/) have worked on evaluating 7 DID methods
using the W3C DID Rubric; a [draft
report](https://docs.google.com/document/d/1jP-76ul0FZ3H8dChqT2hMtlzvL6B3famQbseZQ0AGS8/)
is available.
</details>

<details><summary>
⭐⭐⭐So if I were to design my own DID Method, where to start? How to approach the design?
</summary><br>

The open-endedness and extensibility of DIDs is liberating, daunting, and
staggeringly complex. What can you put into a DID Doc? What are the tradeoffs?
How do people protect or compensate for the privacy and security risks of
putting more into the Doc? These are massive questions, way beyond an FAQ. A
hopefully smaller question is whether the overhead and interoperability costs of
creating a new method outweigh adapting an existing method: whether you land on
a yes or a no or somewhere in between, a thorough review of prior art is still
the next step, whether to reuse or reimplement.  Such a review can be
eye-opening and fortify the design process in a lot of unexpected ways. 
 
 If you decide to design a new DID Method, DIF’s longest-running working group,
[Identifiers and
Discovery](https://identity.foundation/working-groups/identifiers-discovery.html),
would be a good place to start. Skim the
[minutes](https://github.com/decentralized-identity/identifiers-discovery/blob/main/agenda.md)
of recent meetings for DID method design and specification topics, or just reach
out to propose an agenda item at a future
meeting.https://en.wikipedia.org/wiki/XACML
</details>

<details><summary>
⭐⭐⭐Certain use-cases are only possible given certain properties of a
method/did:doc design. How do I find out which DID methods I should be looking
at? 
</summary><br>

This is, again, too large a question for a one-paragraph answer. But
understanding the requirements of a given use-case or problem space takes time
and extensive research-- and neutrality. Try to read against the grain in
marketing materials and arrive at your own conclusions about what different
systems “optimize for”.

Here are some key coarse-grain categories and families of features on which DID
method differ significantly:
- Are VC’s completely “off-chain” or are hashes or pointers encoded in immutable
  storage of some kind?
- Are VC’s revocable? How?
- Does the DID layer support selective disclosure (including ZKP or specific
  forms of ZKP)?
- Does the DID layer include mechanisms for storing and referencing semantics
  (i.e. credential definitions)? Is it a required mechanism?
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; Why aren’t x509 and DIDs compatible? Why aren’t DIDs and eIDAS compatible?
</summary><br>

They are! VCs are neutral and un-opinionated by design as to what kinds of
identifier URIs are provided for issuer and holder identification. DID methods
could be designed to use x.509 structures to manage key material for DIDs, or
simply contain x.509 addresses in their DID:Documents.  For bibliography on
eIDAS and DIDs, see the [Vienna Identity
Meetup](https://www.thedinglegroup.com/blog/2021/3/11/eidas-and-self-sovereign-identity)
and [SSI Meetup](http://ssimeetup.org) recordings on the subject.

Whether or not a specific x.509 system is decentralized enough, or private
enough, is up for debate-- but there is no technological conflict, and plenty of
work has been commissioned by governments around the world to align their
existing identity/transaction auditing infrastructures with this new paradigm
for verifiable credentials. 
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; What’s the difference between a DOI or other “persistent identifier” and a DID?
</summary><br>

Digital Object Identifiers ([DOIs](https://www.doi.org/)) are the most famous
form of persistent identifier, and differ in two main aspects from decentralized
identifiers: on the one hand, they are very centralized, in that one global
registry of all DOIs is maintained and governed by a non-profit called the
International DOI Foundation or
[IDF](https://www.doi.org/doi_handbook/7_IDF.html). On the other, they are
static in both senses of the word: they are neither updatable/reusable nor
interactive, which are the two main superpowers of DIDs.

There are, however, many more persistent identifiers, some of them less
centralized and some of them more interactive or dynamic. Indeed, a whole
community working with such “PIDs” exist, primarily in the fields of library
science, academic publishing, and other fields where unique identifiers and
namespaces for opaque identifiers are of paramount importance. For more
information about that other world, see Markus Sabadello’s article on our blog,
“[DIDs are PIDs](https://blog.identity.foundation/dids-are-pids/)”.
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; What exactly is a SCID?
</summary><br>

Self-certifying identifiers are deterministically derived from public keys, such
that they can be widely published and control of the public key from which they
derive can be proven with its corresponding private key. They are
"self-"certifying in the same way that DIDs generally require reading a
blockchain or other verifiable data registry to certify-- the identifier itself,
being a hash or other deterministic derivation of the public key, validates the
public key. For this reason, some forms of SCID such as those used in KERI or
Sidetree can be called “microledgers,” as explained in this [DIF blog
post](https://blog.identity.foundation/keri--for-every-did--a-microledger/)
about KERI. 

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
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What are agent frameworks? How big, how broad, or even how small can they be?
🌶Do we need them? Should each system just string together the minimum viable
combination of modules that work together?
</summary><br>

One way of thinking of agent frameworks is that they encompass
confidential/privacy-preserving equivalents to many of the “invisible” layers of
the internet stack that we non-specialists rarely think about or even know by
name: Content Delivery Networks (CDNs), service workers, replication and
redundancy services, network routing. Agent frameworks allow lightweight
frontends like single-page apps or decentralized apps (dApps) to interact
directly and discretely with each other and verifiable data registries while
exposing less information and correlation risk than if they went through
conventional clouds and server infrastructures.

There are many use-cases where agents bring more complexity or performance
issues than they are worth; they are particularly well-suited to human-identity
use-cases, high-privacy use-cases, and large ecosystems that are homogenous in
terms of decentralized identity tooling and formats. 
</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; Do existing agent frameworks have some simple overview documentations I can
peruse to compare them? Getting close to interoperability? Or inspiration?
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
⭐⭐ &nbsp;&nbsp; How can I choose between frameworks? This feels like an even bigger commitment
than a choice of DID method.
</summary><br>

It might in fact be a bigger commitment! That said, many frameworks listed above
are deliberately modular and open-ended, allowing not just forking and
customization, but even recombination between them. Frameworks are not as
binding as they were a year ago, and will likely be even less so a year from
now: they are a growth hack and a means to greater decentralization, in the long
view.  Open source is all about trust, after all!

</details>

<details><summary>
⭐⭐⭐Is it smart to try to make one agent/framework to rule them all? 🌶
</summary><br>

No one is trying to make that! Agent frameworks have varying degrees of
interoperability planned on their published roadmaps, and many will likely
support DIDComm, Presentation Exchange, and other common protocols at *some*
level, for inter-framework VC exchange and other interoperability/cross-auditing
purposes. See discussion of this topic
[here](https://docs.google.com/document/d/1O3A0MSSKmVJVPUotFE2H7kGbB4WuBjw1ELHBcer2F3E/edit).
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; Are there any agents that is flexible outside their domain today?
</summary><br>

So far, verification of "foreign" VC formats (and "representations") from other
systems has been slow to be fully integrated into frameworks, but great progress
is being made-- DIF is optimistic that this answer will have to be completely
rewritten by 2022. DIF member Animo Solutions has built LD VC support into Aries
Cloud Agent Python (and hopefully the other Aries agents will soon follow suit).
Furthermore, DIF member [Bloom](https://bloom.co/) has been driving some [WACI
work](https://github.com/hellobloom/waci-demo) on top of the Presentation
Exchange specification to facilitate the initiation and negotiation of
exchanges, which is feeding into a new C&C work item, which might well pave the
way to full VC-HTTP-API support across frameworks.
</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What exactly is a “connection”? Is it a transport? Can I exchange VCs over one?
</summary><br>

“Connection” is very much an Aries-centric concept: it is an abstraction of a
relationship between two identifiers/data subjects, first described in an [Aries
RFC](https://github.com/hyperledger/aries-rfcs/blob/master/features/0160-connection-protocol/README.md).
A more generic version of the concept is included in the [Universal Wallet draft
specification](https://w3c-ccg.github.io/universal-wallet-interop-spec/#connection)
at W3C-CCG, for the sake of portability and equivalences. A little further
afield of the SSI world proper, in the ActivityPub community which develops
tooling for bottom-up/community-driven federated social media and
micropublication systems, there is also a related notion of “[pet
names](https://socialhub.activitypub.rocks/t/petnames-gui/1066)” that may be of
interest to connection & UX researchers: these are local aliases for
opaque/privacy-preserving identifiers, with certain best practices and privacy
models baked in.

Technically, one does not exchange VCs over a “connection,” even if the process
can be described colloquially using this construction. Instead, an Aries
connection is how exchange protocols are initiated and expressed to an end-user;
for the actual mechanics of transport protocols, see the relevant
[subprotocols](https://github.com/hyperledger/aries-rfcs/blob/master/features/0160-connection-protocol/README.md#0-invitation-to-connect)
and Aries RFCs.
</details>

<details><summary>
⭐⭐⭐ Key management: what are the pro's and con's to custodial approaches? What recovery options exist today? Are end-users ready for a private-key based future?
</summary><br>

Product Managers had a [stellar
session](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-10th-2021)
about this last week, which is being continued next week. Much like
"connections", there is very little starting point for a universal standard, and
most blockchains try to tackle this problem from one angle or another so
universalizing is very tricky but there are definitely ways to align without
boiling the ocean.
</details>

## Layer 3: VC Infrastructure

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; Are there different “types” or “formats” of VCs? Are they incompatible?
</summary><br>

There are 4 major “representations'', which are not exactly “formats” in the
sense that word documents or PDFs are a “file format,” but rather more like 4
encoding systems from 4 different operating systems or file systems. They have
slightly different relationships to external semantic anchoring, which makes
translating *losslessly* between them or “roundtripping” a very tricky, but not
impossible, technical problem. Most of today’s solutions opt to translate with a
little loss if it is acceptable to their usecases. DIF Interop WG has hosted a
lot of conversations on this topics, and Kaliya Young's recent [article about
exactly
this](https://www.lfph.io/wp-content/uploads/2021/02/Verifiable-Credentials-Flavors-Explained.pdf)
was crowd-edited on a [very special
episode](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---13-jan-2021---usapac-time-1400pt---communications-problem-explaining-the-vc-format-wars-to-decision-makers).
The article is definitely the best place to start further reading. 
</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; These things are revocable, right?
</summary><br>

Actually, most VC systems currently have limited revocation capabilities, as
they add significant scaling costs and complexity, to say nothing of varying
properties for privacy engineering. Different use cases justify different
approaches to revocation (including none at all).  Martin Riedel's overview of
approaches to revocation/status mechanisms at interop [in
February](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---10-feb-2021---usapac-time-1400pt---revocation-method-comparison)
was really helpful in introducing these approaches at a high level, and a series
of events in the months since have explored the topic further; see the Interop
WG notes for more
[details](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md).
</details>

<details><summary>
⭐⭐⭐ I’ve never used JSON-LD and I get confused by all this LD talk. Can you explain
it to me like I’m 5? What’s the difference between a JSON-LD “Context”
/Vocabulary, the traditional “Data Schemata” I use every day?
</summary><br>

Traditional data schemata are used to express (and thus validate against that
expression) the **syntax** of data objects-- the type, length, form,
presence/absence, etc of values in the key/value pairs that make up most data
structures. The primary function of JSON-LD contexts is to express the
**semantics** of the keys, not the values-- they facilitate the translation
between schemata or systems and the reconstruction of lost or foreign contexts
in which data can have meaning.
</details>

<details><summary>
⭐⭐⭐ That sounds hard, and/or I don’t think my boss/investors/CISO would like that.
Is JSON-LD the only way to express semantics? Do I have to use JSON-LD to use
VCs?🌶🌶
</summary><br>

There are other systems for expressing semantics for data, such as the young
IETF standard
[JSON-Schema](https://json-schema.org/learn/getting-started-step-by-step.html)
which does not require keys to be defined against public definitions and that
does not require/assume the immutable publication of contexts for signatures to
be long-lived. This may be simpler and easier for some use cases but may inhibit
interoperability with LD-based systems and the vocabularies of organizations
like the W3C and GS1. Like LD Schema, JSON Schema requires special linters and
validators, which can be found in the [JSON Schema
Section](https://extendsclass.com/json-schema-validator.html) at
extendsclass.com . DIF work items like the [Credential
Manifest](https://identity.foundation/credential-manifest/) use JSON Schema
extensively.

Also, the low-level VC libraries in the Aries ecosystem abstract out much of the
complexity specific to LD and semantic anchoring. See
[RFC47](https://github.com/hyperledger/aries-rfcs/tree/master/concepts/0047-json-ld-compatibility),
[RFC250](https://github.com/hyperledger/aries-rfcs/blob/master/concepts/0250-rich-schemas/README.md),
Implementer’s Call [Notes
12-17-20](https://wiki.hyperledger.org/display/IWG/2020-12-17+Identity+Implementers+WG+Call),
and the archives of the AriesGo framework [discussion
channels](https://wiki.hyperledger.org/display/ARIES/aries-framework-go), where
much low-level JSON-LD work has taken place; to expand Aries support for
JSON-LD, check the [Code With
Us](https://digital.gov.bc.ca/marketplace/opportunities/code-with-us/3f9f0e86-b8bf-47ee-9f3d-5b272f9ec845)
for open grants.
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; Where do “Credential Definitions” fit in?
</summary><br>

The core VC libraries of the Hyperledger Aries project work on a kind of hybrid
“credential definition” that includes both semantic and syntactic definitions of
what can go into a given VC called a [Rich
Schema](https://github.com/hyperledger/aries-rfcs/blob/master/concepts/0250-rich-schemas/README.md).
VCs are not only validated against these definitions, but the CL-ZKP algorithms
available in the same libraries also use the definitions to allow for verifiable
selective disclosure of subsets of credential data via “framing”-- this process
requires the definition as one of the inputs, however, so Indy-conformant
credential definitions must be used. These have historically been written to the
Indy blockchain, but other forms of immutable/highly-available storage are being
pioneered in the Aries ecosystem.
</details>

<details><summary>
⭐⭐⭐How do I interpret credentials that require validating them against JSON-LD
Contexts? Should I be scared?
</summary><br>

Fetching new contexts and revocation lists at runtime is generally frowned upon
and could raise serious privacy and security issues in a production environment;
for this reason, JSON-LD, like most graph-model data systems, makes extensive
use of caching, pre-loading, and periodically refreshing its dependencies to
build a “local graph.” One crucial building-block in such a secure pre-loading
system specific to the JSON-LD concept of a “document” is the “document loader”
described in many specifications and tutorials on how to build for JSON-LD
verification. DIF hosts a general-purpose reference
[implementation](https://github.com/decentralized-identity/jsonld-document-loader)
of such a tool, and its donator, Orie Steele of Transmute Industries, gave an
overview of [why and how to use it](https://youtu.be/-yUbMDft5O0) at DIF Interop
WG.
</details>

<details><summary>
⭐⭐⭐How do I make my own JSON-LD Context?
</summary><br>

Basically, the process of creating schemata (whether for syntax, for semantics,
or both) is best thought of as a *recombinatory* process-- mixing and matching
composable prior art and adding properties or methods to existing building
blocks is the name of the game, and the more you can recycle or use common
building blocks, the better. Developers often refer to this as “extending
classes,” i.e. adding properties and methods to a pre-existing object.

Most schema development for JSON-LD projects (whether for shape, for semantics,
or both) starts with a bit of reading on Schema.org’s [reference
shelf](https://schema.org/docs/documents.html) and search function results, or a
few other major ontologies/contexts like the [HeppNetz Good Relations
](http://www.heppnetz.de/projects/goodrelations/)vocabulary for e-Commerce or
the [EPCIS](https://www.gs1.org/epcis/epcis/1-1) standard for describing
business processes and events. Once you have a skeleton that maps *most* of the
relevant data for your use case in standardized terms, you’re ready to start
extending!

Another place to look is the vocabularies established in the W3C-CCG, some of
which, such as the traceability vocabulary, have their own unique generators for
creating and testing LD schemata from conventional "data shape" schemata in
JSON. An example of the stages of generation can be found
[here](https://github.com/w3c-ccg/traceability-vocab#place-as-an-example)and a
generation tutorial is forthcoming. 
</details>

<details><summary>
⭐⭐⭐Where do your extensions *live*, tho? 
</summary><br>

Extensions can remain specific to a given project if your project hosts its own
vocabulary extending standard one, or (with appropriate resources and timelines)
you can propose your extensions “to origin” at
[schema.org](https://schema.org/docs/extension.html) or elsewhere. When
self-hosting, remember to configure your web server to serve LD files as
MIME-type json+ld (you might also want to get fancy with [versioning
redirects](https://github.com/w3c-ccg/vc-http-api/pull/158#issue-588951741) like
/latest/ and /next/)
</details>

<details><summary>
⭐⭐⭐Can a VC be signed by two or more parties? How do I produce and consume multi-signed VCs?
</summary><br>

Yes! The VC spec is actually fairly open on this issue, and Markus Sabadello
gave a [great
presentation](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---3-feb-2021---useu-time-0600-pt---update-on-did-core-and-enterprise-ethereum-alliance-d-burnett-and-did-interop-fundamentals-markus-sabadello-and-guests)
at DIF Interop in January of 2021 laying out two major schools of prior art
here-- how and when to produce each, and how to verify both.
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; What is ZKP? What is the difference between ZKP and “Selective Disclosure”?
</summary><br>

Zero-Knowledge Proofs refers to a mathematical construct, which is at the heart
of many cryptographic systems such as the control privacy-preserving mechanisms
in such "blinded transaction" blockchains as ZCash. It refers to mathematical or
data operations, not to high-level protocols such as credential exchange or
proofing claims or real-world exchanges.

Selective Disclosure, on the other hand, refers to real-world exchanges or
information exchanges.  In the VC context, presenting information contained in a
verifiable credential selectively, in a way that still allows the credential as
a whole to be cryptographically proofed and verified, usually relies on some
form of ZKP cryptography.  There are different styles of ZKP and different
styles of Selective Disclosure, so it helps to be precise about exactly which
kind you are talking about, as they all have distinct properties and guarantees,
scalability issues, etc. 

In the decentralized identity world, the most common selective disclosure
mechanisms (each with their own distinct Verifiable Presentation mechanisms!)
are:

- CL-ZKP (the CL stands for
  [Camenisch-Lysyanskaya](https://www.youtube.com/watch?v=K6s4ENTfcWw), the last
  names of the two designers), which powers Indy and Indy-based systems' VP
  capabilities; the bulk of this work has been driven by DIF member Evernym.
- BBS+ (See Mattr's
  [Introduction](https://mattr.global/using-privacy-preserving-zkp-credentials-on-the-mattr-platform/),
  [AMA](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---18-nov-2020---usapac-time-1400-pt),
  and test-suite PR in the VC-HTTP-API
  ([144](https://github.com/w3c-ccg/vc-http-api/pull/144#discussion_r590342533))
  for background); many DIF members have also pioneered the work, including
  Trinsic and SecureKey. 
- Microsoft Research has been building up ZKP capabilities based on an unrelated third form of cryptographic tradition known as "[fuzzy vaults](https://medium.com/decentralized-identity/building-interoperable-zkp-credential-systems-70bc20a8a809)," but a VP implementation based on it is still forthcoming. 

</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What is the relationship between DIDs and VCs?
</summary><br>

Technically, there is none! VCs work great with DIDs used as the identifiers for
issuer and verifier, but they also work with many other kinds of identifiers
(Solid addresses, centralized and local identifier schemes,
blockchain/smart-contract addresses, etc). DIDs can be used for all kinds of
verifications, which is why the "verification method" system of associating
multiple keys of different types with each DID is so flexible; signing VCs is
only one of many purposes.  That said, the designers of both always had the
other front-of-mind, and the complementarity of design thinking is hard to deny
or overlook.
</details>

## Layer 4: Apps, UX, and Wallets

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What shape can this take? What kinds of software and hardware will be able to use DIDs and VC?
</summary><br>

The sky is the limit-- all kinds of form factors and software contexts are in
various stages of prototyping an standardization!  In fact, many people use the
word "wallet" to refer to all kinds software, including libraries and widgets
working invisibly inside other software. There are browser-based wallets (that
store keys in the browser, whether temporarily or permanently), cloud-based
wallets (that rely on "cloud HSMs" and other cloud-native secure keystores and
have a conventional account structure per user), mobile apps (that may use
biometrics, on-device cryptography, etc).  There are combinations and
synchronization/replication systems spanning 2 or 3 of those.  There are even
on-premise systems for issuance and verification, which might produce and
consume VCs without a conventional individual/edge wallet ever coming into play.
There are many many nails that this hammer is good for!
</details>

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; Do I need a fancy new, modern smartphone to control my own identity and credentials securely and privately?
</summary><br>

This is a matter of some debate, and like privacy and other psychological and/or
legal norms, "self-sovereignty", "direct control" of data, and "data rights" are
highly specific to their underlying social, legal, political,  economic, and
even medical realities.  There is plenty of work ongoing in our community on
[Guardianship](https://sovrin.org/a-deeper-understanding-of-implementing-guardianship/)
as a techno-social construct (and legal corollary to assumptions about the
agency of the "user" in software thinking), to give just one example, and the
use of biometrics or mnemonics to prove, maintain, and exert control over a DID
will likely need to be advanced and standardized before decentralized identity
architectures can be brought to the huge fraction of the world's population with
low chances of owning a cryptographically enabled personal phone or computer.  
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; Do concepts from cryptocurrency wallets like "cold storage", "air gapping", and "custodial wallet" apply to identity wallets?
</summary><br>

Yes and no-- in some use cases, the distinctions can be quite meaningful because
they signal different architectures, security guarantees, relations of power
between stakeholders, etc etc.  In particular, SSI use cases about direct,
interactive control of credentials by individual humans lend themselves quite
well to these analogies, and web-based wallets (with the actual private key
controlled by a trusted service provider, a hardware security module, a cold
storage device, etc) can be understood as less directly human-controlled.  In
other use cases, though, the analogy can be confusing or distracting, so don't
expect them to be useful everywhere!
</details>


<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; How do DIDs and VCs get used without a live
 internet connection for querying a live blockchain?
</summary><br>

Depending on what information needs to be live for a given use-case, and how
live/fresh it needs to be, verification can be more or less "offline".  For
instance, if a verifier has all the information it needs about a known and
finite set of issuers, it can verify the authenticity of a VC offline-- and
depending on what information the holder of that credential can present along
with it, they can also verify that it was indeed issued to them.  Checking the
status of mutable-status (i.e., revocable) credentials offline is another tricky
matter, but here as everywhere, it depends on the requirements of the usecase--
if revocation lists can be updated once a day, the 23 hours between updates
verification can happen live and offline!
</details>


<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; What's the difference between a Wallet and a Mobile Agent?🌶
</summary><br>

Actually, this answer cannot be answered definitively-- the terms are, in some
sense, still shifting and drifting over time as our nascent "market" changes
shape and needs; they might never truly settle, because both "wallet" and
"agent" are complex and multivalent terms already in the history of software,
which mean very different things in nearby contexts.  For instance, in browser
terminology, an "agent" is any daemon or widget that reliably represents or
serves a distant party (usually human) in a fiduciary or remote-control
capacity; in legal terms, an agent is anything that acts on another's behalf;
etc etc.  A whole survey-based research project of DIF's Glossary Group tried to
suss out who used the term how in our community and descriptively map the
schools of thought (see the [final
report](https://identity.foundation/assets/glossary-group-report--may-2020.pdf)
for a skimmable overview).  It's not a bad thing that no cross-community
concensus ever arose!
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; How many wallet should there be in the future? How many will there be in, say, 2 or 10 or 20 years?🌶🌶
</summary><br>

I marked this question with two chilis because "browsers" were the battleground
of Web 1.0 and "apps" were the battleground of Web 2.0, leaving many to
speculate that wallets and/or blockchains will be the battlegrounds of Web 3.0.
Drummond Reed of Evernym and the ToIP Foundation even gave a talk on the [Coming
Browser
Wars](https://uto.asu.edu/features/move-over-browsers-future-internet-digital-wallets);
it stands to reason that whoever owns and governs the major wallets (and thus
the end-user's UX, which seeps into and influences the whole culture and
ideology of the digital world) will be well-positioned in our decentralized
future! While DIF's focus is mostly on paving the highways and freeways rather
than on designing the cars, UX has its place at DIF (the Product Managers
group), and as any UX designer can tell you, you can't leave UX thinking for
last!

All that said, DIF is a member organization and cannot speculate on the shape of
competition between its members. Wallets play such an integral role in the
business models and market dynamics of our members' work that we can only signal
the consequence of wallet design and encourage its member to collaborate and
co-develop wallets and common wallet libraries and components openly.

</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; How can UX design be flexible but still privacy-preserving when allowing users to combine, link, or co-present VCs issued to different DIDs?
</summary><br>

There’s not a lot written about this or prior art!  If you know of any please
open a PR against this answer using the github link at the top of this document.
If you are working on such a project, please contact the [product
managers](https://lists.identity.foundation/g/id-productmanagers) group and
present the project for feedback!
</details>

<details><summary>
⭐⭐ &nbsp;&nbsp; How can UX design be flexible but still privacy-preserving when allowing users to combine, link, or co-present VCs issued to different DIDs?
</summary><br>

There’s not a lot written about this or prior art!  If you know of any please
open a PR against this answer using the github link at the top of this document.
If you are working on such a project, please contact the [product
managers](https://lists.identity.foundation/g/id-productmanagers) group and
present the project for feedback!
</details>

<details><summary>
⭐⭐⭐ How can key management be made usable for "normal" end-users?
</summary><br>

DIF Executive Director Rouven Heck led a fascinating
[two](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-10th-2021)-[part](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-24th-2021)
discussion of this topic at the Product Managers group, which overviewed the
problem space quite well and provided lots of further reading and links. 
</details>

<details><summary>
⭐⭐⭐ How can key management be made usable for "normal" end-users?
</summary><br>

DIF Executive Director Rouven Heck led a fascinating
[two](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-10th-2021)-[part](https://github.com/decentralized-identity/product-managers/blob/main/agenda.md#february-24th-2021)
discussion of this topic at Product Managers, which overviewed the problem space
quite well and provided lots of further reading and links. 
</details>

## Layer 5: Trust Frameworks and Ecosystems across Industries and Jurisdictions

<details><summary>
 &nbsp;&nbsp; ⭐ &nbsp;&nbsp; So, is this stuff street-legal yet? If so, where? If not, what's it going to take?
</summary><br>

Legalizing any load-bearing, high-value technology is slow and complex work that
takes a lot of hands-- first, exact definitions and specifications are needed,
as well as standardizations, longitudinal assesments, academic studies, impact
reports, that kind of thing.  Even after all that is squared away and packaged
up to adequately prepare regulators to do their work, they in turn take their
own time to harmonize many different specialists and stakeholders, before they
can present somethign to politicians, who have their own games to play and
interests to align.  All the market forces in the world, perfectly aligned, can
only speed these processes up so much.

All that said, encryption has been around a long time, and personal data, and
direct control mechanisms, and privacy laws.  All of these exist in regulatory
frameworks and relatively stable, regulated marketplaces for software that
structure all of this at national or global scale. When you combine these
regulatory frameworks with certification schemes and the kind of fair-play
pressures and norms that Better Business Bureaus and guilds enforce, you've got
a **Trust Framework**, which in layman's terms tells you how much to trust each
link in a chain of data, contracts, and service/fiduciary relationships. How
much liability can a bank outsource to the software providers that make its
mobile app? Which digital signatures hold up in court? What's an acceptible
margin of error when identifying people, or vouching for the soundness of their
paperwork? These are all norms set by a Trust Framework, which might govern a
nation-state or an industry within one or a global software market.
</details>


<details><summary>
 &nbsp;&nbsp; ⭐⭐ &nbsp;&nbsp; Those Trust Framework things sound cool, where can I find out more?
</summary><br>

Trust Frameworks are complex things, and no single organization can be expected
to track them all or exert pressure on all of them. DIF has historically done
little work directly on trust frameworks, but DIF works with many organizations
on trust framework and regulatory issues, inside and outside of its parent
organization, the Linux Foundation.  For further reading, see:

* The Open Identity Exchange ([OIX](https://openidentityexchange.org/about)) has
  a [Trust Framework Working
  Group](https://openidentityexchange.org/workgroups?action=view&Workgroup=455)
  that has released a [very thorough and comprehensive
  guide](https://openidentityexchange.org/guide-trust-frameworks-interoperability)
  to trust frameworks for identity software, and is incrementally expanding and
  revising it to include decentralized architectures alongside today's
  mainstream federated ones. See [this
  recording](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---28-apr-eu-time---how-trust-frameworks-compare-and-develop-oix)
  of OIX's Nick Mothershaw speaking at the Interoperability WG about the
  revision process and getting input from our community on how to bring the good
  word to the regulators and trustwork framers of the world. 
* The DIF Interop WG also held an open discussion on the subject of some trust
  frameworks and certification schemes pertinent to our industry on [31 Mar
  2021](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md#agenda---31-mar-2021---trust-framework-talk)
  
* A sister organization in the Linux Foundation called the Trust Over IP
  foundation does a lot of work on trust frameworks and specifying privacy,
  confidentiality, and audit/verification capabilities into trust frameworks
  instead of just liabilities.  They also have an early-stage specification for
  [Machine-Readable Trust
  Frameworks](https://wiki.trustoverip.org/display/HOME/ToIP+Governance+Metamodel)
  that is being formulated on a conceptual level in their [Governance Stack
  Working
  Group](https://wiki.trustoverip.org/display/HOME/Governance+Stack+Working+Group);
  the technical specifications for an early prototype of the concept are
  currently proposed as a [conceptual
  RFC](https://github.com/hyperledger/aries-rfcs/blob/master/concepts/0430-machine-readable-governance-frameworks/README.md)
  in the Aries community.
* Trust Frameworks are often discussed, assessed, and even critiqued in the
  [MyData community](https://mydata.org/), particularly in Europe, where the
  bulk of their activities are based).
* Another key technical organization that often intervenes and opines on Trust
  Frameworks and regulatory matters is the [Kantara
  Initiative](https://kantarainitiative.org/), primarily active and influential
  in the English-speaking world. They have even authored meta-frameworks that
  offer building blocks for more active frameworks in specific jurisdictions,
  such as their [Identity Assurance
  Framework](https://kantarainitiative.org/idassurance/); they also incubated,
  standardized, and govern an Authorization framework called [User Managed
  Access](https://kantarainitiative.org/confluence/display/uma/Home), which laid
  important technical and social groundwork for the technologies and ideas of
  decentralized identity.

</details>

## Layer X: Architectural Considerations, Interoperability, and Integrations

<details><summary>
 &nbsp;&nbsp; ⭐⭐ &nbsp;&nbsp; Don't we already have a standard? What's so hard about interoperating? 🌶
</summary><br>

If it were easy, the [Interop
WG](https://github.com/decentralized-identity/interoperability#interoperability-project)
wouldn't need to meet
[weekly](https://github.com/decentralized-identity/interoperability/blob/master/agenda.md)
to educate, document, strategize, and evangelize for interoperability planning,
testing, certifications, and collaborations!  The ["Deliverables"
section](https://github.com/decentralized-identity/interoperability#minor-deliverables)
of the WG's homepage is a good overview of how complicated and hard it is to
herd the cats of our community and broker common goals and definitions.  For an
explanation of the current state of those negotiations, see our recent [blog
post](https://blog.identity.foundation/setting-interoperability-targets/) on the
subject.

In particular, see our [interoperability
map](https://github.com/decentralized-identity/decentralized-identity.github.io/blob/master/assets/crosscommunity-architecture-survey-oct-2020.pdf),
which includes lots of information about architectural considerations in the
"transversal" column, and integration/retro-fitting concerns for bridging to
today's data systems.

</details>