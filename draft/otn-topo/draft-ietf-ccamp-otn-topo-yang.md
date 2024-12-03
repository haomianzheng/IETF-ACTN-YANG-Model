---
title: "A YANG Data Model for Optical Transport Network Topology"
abbrev: "OTN Topology YANG Model"
category: std

docname: draft-ietf-ccamp-otn-topo-yang-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Routing"
workgroup: "CCAMP Working Group"
venue:
  group: "Common Control and Measurement Plane"
  type: "Working Group"
  mail: "ccamp@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/ccamp/"
  github: "haomianzheng/ccamp-client-pm-yang"
  latest: "https://haomianzheng.github.io/ccamp-client-pm-yang/draft-zheng-ccamp-client-pm-yang.html"

author:
  -
    name: Haomian Zheng
    org: Huawei Technologies
    street: H1, Huawei Industrial Base, Songshan Lake
    city: Dongguan
    region: Guangdong
    code: 523808
    country: China
    email: zhenghaomian@huawei.com
  -
    name: Italo Busi
    org: Huawei Technologies
    email: italo.busi@huawei.com
  -
    name: Xufeng Liu
    org: Alef Edge
    email: xufeng.liu.ietf@gmail.com
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    name: Oscar Gonzalez de Dios
    ins: O. Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com

contributor:
  -
    name: Aihua Guo
    org: Futurewei
    email: aihuaguo.ietf@gmail.com
  -
    name: Anurag Sharma
    org: Google
    email: ansha@google.com
  -
    name: Yunbin Xu
    org: CAICT
    email: xuyunbin@caict.ac.cn
  -
    name: Lei Wang
    org: China Mobile
    email: wangleiyj@chinamobile.com
  -
    name: Baoquan Rao
    org: Huawei Technologies
    email: raobaoquan@huawei.com
  -
    name: Xian Zhang
    org: Huawei Technologies
    email: Huawei Technologies
  -
    name: Huub van Helvoort
    ins: H. van Helvoort
    org: Hai Gaoming BV
    email: huubatwork@gmail.com
  -
    name: Victor Lopez
    org: Nokia
    email: victor.lopez@nokia.com
  -
    name: Yunbo Li
    org: China Mobile
    email: liyunbo@chinamobile.com
  -
    name: Dieter Beller
    org: Nokia
    email: dieter.beller@nokia.com
  -
    name: TBD

normative:
  ITU-T_G.709:
    title: Interfaces for the optical transport network
    author:
      org: ITU-T Recommendation G.709
    date: March 2020
    seriesinfo: ITU-T G.709

informative:

--- abstract

This document defines a YANG data model for representing, retrieving,
and manipulating Optical Transport Network (OTN) topologies.  It is
independent of control plane protocols and captures topological and
resource-related information pertaining to OTN.

--- middle

# Introduction

A transport network is a server-layer network designed to provide
connectivity services for a client-layer network to carry the client
traffic transparently across the server-layer network resources.  A
transport network typically utilizes several different transport
technologies such as the Optical Transport Networks (OTN) or packet
transport such as provided by the MPLS-Transport Profile (MPLS-TP).

This document defines a data model of an OTN topology, using YANG version 1.1 
{{!RFC7950}}.  The model can be used by an application communicating
with a transport controller.  Furthermore, it can be used by an
application for the following purposes (but not limited to):

- To obtain a whole view of the network topology information of its
interest;

- To receive notifications with regard to the information change of
the OTN topology;

- To enforce the establishment and update to the network topology
with the characteristics specified in the data model;

The YANG model defined in this document is independent of control
plane protocols and captures topology-related information pertaining
to OTN electrical layer, as the scope specified by {{?RFC7062}} .
Furthermore, it is not a stand-alone model, but augments from the TE
topology YANG model defined in {{!RFC8795}}, and importing from the
generic Layer 1 types defined in {{!I-D.ietf-ccamp-layer1-types}}.
Following TE topology YANG model, the YANG model defined in this
document is interface independent.  The model is included in
{{?I-D.ietf-teas-actn-yang}}, which indicates the typical usage of IETF
YANG models in ACTN architecture specified by {{?RFC8453}}.  More
specifically, the usage of this model between controllers is
described in {{?I-D.ietf-ccamp-transport-nbi-app-statement}}.

This model supports both client-configured and system-controlled OTN
topologies, as described {{!RFC8345}}.
These OTN topologies can be used as overlay or underlay topologies, using the mechanisms defined in {{!RFC8345}} and {{!RFC8795}}.

The reader of this document is assumed to be familiar with the OTN
technology, as specified in {{ITU-T_G.709}} and with the TE topology
YANG data model, as defined in {{!RFC8795}}.

{{?RFC7062}} also provides a framework to allow the development of
protocol extensions to support GMPLS and Path Computation Element
(PCE) control of OTN.

{{Section 6 of !RFC8795}} provides guidelines for writing technology-
specific TE topology augmentations.

The YANG data model in this document conforms to the Network
Management Datastore Architecture defined in {{!RFC8342}}.

## Terminology and Notations

Some of the key terms used in this document are listed as follows.

TS:
: Tributary Slot.

TSG:
: Tributary Slot Granularity.

TPN:
: Tributary Port Number.

Refer to {{?RFC7062}} for the key terms used in this document.

The following terms are defined in {{!RFC7950}} and are not redefined
here:

-  client

-  server

-  augment

-  data model

-  data node

The following terms are defined in {{!RFC6241}} and are not redefined
here:

-  configuration data

-  state data

The terminology for describing YANG data models is found in
{{!RFC7950}}.

## Requirements Language

{::boilerplate bcp14}

## Tree Diagram

A simplified graphical representation of the data model is used in
{{yang-tree}} of this this document.  The meaning of the symbols in these
diagrams is defined in {{?RFC8340}}.

## Prefix in Data Node Names

In this document, the names of data nodes and other data model
objects are prefixed using the standard prefix associated with the
corresponding YANG imported modules, as shown in {{tab-prefixes}}.

| Prefix      | YANG module             | Reference
| l1-types    | ietf-layer1-types       | \[RFCYYYY]
| otnt        | ietf-otn-topology       | RFC XXXX  |
| nw          | ietf-network            | {{!RFC8345}} |
| nt          | ietf-network-topology   | {{!RFC8345}} |
| tet         | ietf-te-topology        | {{!RFC8795}} |
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

> RFC Editor Note:
Please replace XXXX with the number assigned to the
RFC once this draft becomes an RFC.
Please replace YYYY with the RFC
numbers assigned to {{!I-D.ietf-ccamp-layer1-types}}.

# YANG Data Model for OTN Topology

## OTN Topology Data Model Overview

This document aims to describe the data model for OTN topology.  As a
classic Traffic-engineering (TE) technology, OTN provides TDM
switching in transport network {{ITU-T_G.709}}.  Therefore, the YANG
module presented in this document augments from a more generic
Traffic Engineered (TE) network topology data model, i.e., the ietf-
te-topology, as specified in {{!RFC8795}}.  In {{Section 6 of !RFC8795}},
the guideline for augmenting TE topology model was provided, and in
this draft, we augment the TE topology model to describe the topology
in OTN.  Common types, identities and groupings defined in
{{!I-D.ietf-ccamp-layer1-types}} is reused in this document.  {{!RFC8345}}
describes a network topology model and provides the fundamental model
for {{!RFC8795}}.  However, this work is not directly augmenting
{{!RFC8345}}.  {{fig-overview}} shows the augmentation relationship.

~~~~ ascii-art
                        +------------------+
           TE generic   | ietf-te-topology |
                        +------------------+
                                  ^
                                  |
                                  | Augments
                                  |
                        +---------+---------+
           OTN          | ietf-otn-topology |
                        +-------------------+
~~~~
{: #fig-overview title="Relationship between OTN and TE topology models"}

The entities and TE attributes, such as node, termination points and
links, are still applicable for describing an OTN topology and the
model presented in this document only specifies technology-specific
attributes/information.  The OTN-specific attributes in {{!RFC7139}},
including the TPN, TS and TSG, can be used to represent the bandwidth
and label information.  These attributes have been specified in
{{!I-D.ietf-ccamp-layer1-types}}, and used in this document for
augmentation of the generic TE topology model.

## Attributes Augmentation {#sec-attributes}

There are a few characteristics augmenting the generic TE topology.

Following the guidelines described in {{!RFC8795}}, an otn-topology
network-type is specified as the indicator of OTN in the topology.

~~~~ ascii-art
      augment /nw:networks/nw:network/nw:network-types/tet:te-topology:
        +--rw otn-topology!
~~~~

Three OTN technology-specific parameters that augment the generic TE
link attributes are specified.

~~~~ ascii-art
      augment /nw:networks/nw:network/nt:link/tet:te
                /tet:te-link-attributes:
        +--rw otn-link
          +--rw odtu-flex-type?   l1-types:odtu-flex-type
          +--rw tsg?              identityref
          +--rw distance?         uint32
~~~~

In OTN the resources is measured by the tributary slots (TS), as
specified in {{!RFC7139}}.  The tributary slot granularity (TSG)
attribute defines the granularity, such as 1.25G, 2.5G and 5G, used
by the TSs of a given OTN link.  The distance attribute describes the
geographical distance between a pair of OTN link termination points.
This is usually measured by the length of the fibre.

The OTN topology model also includes information about the access
links that support the transparent client signals, defined in
{{!I-D.ietf-ccamp-layer1-types}}.  These links can also be multi-
function access links that can support one or more transparent client
signals and OTN.

A client-svc presence container is specified to augment the generic
TE link termination point to describe if the point is capable of
carrying a client signal and what kind of signal can be carried as
follows.  The same presence container is also specified for the TE
link.

~~~~ ascii-art
      augment /nw:networks/nw:network/nw:node/nt:termination-point
                /tet:te:
        +--rw client-svc!
            +--rw supported-client-signal*   identityref
~~~~

The list of supported-client-signal is used to provide the
capabilities of the client signal specified in
{{!I-D.ietf-ccamp-layer1-types}}.

## Bandwidth Augmentation {#sec-bandwidth}

Following the guidelines in {{!RFC8795}}, the model augments all the
occurrences of the te-bandwidth container with the OTN technology-
specific attributes using the otn-link-bandwidth and otn-path-
bandwidth groupings defined in {{!I-D.ietf-ccamp-layer1-types}}.

The odtu-flex-type attribute of a given OTN Link (or Link Termination Point - LTP), shown in {{sec-attributes}}, is used, together with the OTN technology-specific attributes defined in the otn-link-bandwidth and otn-path-bandwidth groupings, to compute the number of Tributary Slots (TS) required by the ODUflex LSPs set up on that OTN Link (or LTP).

In order to compute the number of Tributary Slots (TS) required by the ODUflex LSPs set up on an underlay path (e.g., the underlay path of a connectivity matrix entry), the odtu-flex-type attribute is added to the OTN technology-specific attributes defined in the otn-link-bandwidth and otn-path-bandwidth groupings.

## Label Augmentation

The model augments all the occurrences of the label-restriction list
with OTN technology specific attributes using the otn-label-range-
info grouping defined in {{!I-D.ietf-ccamp-layer1-types}}.

Moreover, following the guidelines in {{!RFC8795}}, the model augments
all the occurrences of the te-label container with the OTN technology
specific attributes using the otn-label-start-end, otn-label-hop and
otn-label-step groupings defined in {{!I-D.ietf-ccamp-layer1-types}}.

# The YANG Model {#yang-code}

This YANG module references {{!RFC8345}}, {{!RFC8795}},
{{!I-D.ietf-ccamp-layer1-types}} and {{ITU-T_G.709}}.

~~~~ yang
{::include ../../../YANG/ccamp/otn-topology/ietf-otn-topology.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-otn-topology@2024-06-21.yang"}

# IANA Considerations

It is proposed to IANA to assign new URIs from the "IETF XML
Registry" {{!RFC3688}} as follows:

~~~~
      URI: urn:ietf:params:xml:ns:yang:ietf-otn-topology
      Registrant Contact: The IESG
      XML: N/A; the requested URI is an XML namespace.
~~~~

This document registers a YANG module in the YANG Module Names
registry {{!RFC7950}}.

~~~~
      name:         ietf-otn-topology
      namespace:    urn:ietf:params:xml:ns:yang:ietf-otn-topology
      prefix:       otnt
      reference:    RFC XXXX
~~~~

> RFC Editor Note: Please replace XXXX with the number assigned to the
RFC once this draft becomes an RFC.

# Security Considerations

This section is modeled after the template described in Section 3.7
of {{?I-D.ietf-netmod-rfc8407bis}}.

The "ietf-te-types" and the "ietf-te-packet-types" YANG modules define data models that are
designed to be accessed via YANG-based management protocols, such as
NETCONF {{?RFC6241}} and RESTCONF {{?RFC8040}}. These protocols have to
use a secure transport layer (e.g., SSH {{?RFC4252}}, TLS {{?RFC8446}}, and
QUIC {{?RFC9000}}) and have to use mutual authentication.

The Network Configuration Access Control Model (NACM) {{!RFC8341}}
provides the means to restrict access for particular NETCONF or
RESTCONF users to a preconfigured subset of all available NETCONF or
RESTCONF protocol operations and content.

There are a number of data nodes defined in this YANG module that are writable/creatable/deletable (i.e., config true, which is the default).
These data nodes can be considered sensitive or vulnerable in some network environments.
Write operations (e.g., edit-config) to these data nodes without proper protection can have a negative effect on network operations.
Specifically, the following subtrees and data nodes have particular sensitivities/vulnerabilities:

- "/nw:networks/nw:network/nw:network-types/tet:te-topology/otnt:otn-topology"

> This subtree specifies the OTN topology type. Modifying the configurations can render the OTN topology type invalid. By making such modifications, a malicious attacker may disable the OTN capabilities on the related networks and cause traffic to be disrupted or misrouted.

- "/nw:networks/nw:network/nw:node/tet:te/tet:te-node-attributes/otnt:otn-node"

> This subtree specifies the OTN node type. By configuring the OTN node type, an attacker may create an unauthorized OTN traffic path. By removing it, a malicious attacker may cause OTN traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding OTN nodes and OTN links in this OTN topology and the connected OTN topologies.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:otn-link/otnt:odtu-flex-type"

> This node is used, together with the other attributes in the otn-bandwidth container, to compute the OTN bandwidth information for an OTN link, as described in {{sec-bandwidth}}. By configuring, modifying or removing this data node, a malicious attacker may modify the OTN bandwidth. The consequences of modifying the OTN bandwidth are reported below for the otn-bandwidth container.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:otn-link/otnt:tsg"

> This node represents the TSG of the OTN link, as described in {{sec-attributes}}. By configuring, modifying or removing this data node, a malicious attacker may modify the resouces assigned to the OTN LSPs setup over that OTN link. The consequences of modifying the TSG would be to disrupt the traffic carried by the OTN LSPs setup over that OTN link.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:otn-link/otnt:distance"

> This node is describes the geographical distance between a pair of OTN link termination points. By configuring, modifying or removing the distance, an attacker may cause OTN traffic to be misrouted. Such traffic changes may also affect the traffic on the surrounding OTN nodes and OTN links in this OTN topology and the connected OTN topologies.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:client-svc"

> This subtree specifies the client traffic type supported by a link. By configuring it, an attacker may create an unauthorized client traffic path. By removing it, a malicious attacker may cause client traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding OTN nodes and OTN links in this OTN topology and the connected OTN topologies.

- "/nw:networks/nw:network/nw:node/nt:termination-point/tet:te/otnt:otn-link-tp/otnt:odtu-flex-type"

> This node is used, together with the other attributes in the otn-bandwidth container, to compute the OTN bandwidth information for an OTN link termination point, as described in {{sec-bandwidth}}. By configuring, modifying or removing this data node, a malicious attacker may modify the OTN bandwidth. The consequences of modifying the OTN bandwidth are reported below for the otn-bandwidth container.

- "/nw:networks/nw:network/nw:node/nt:termination-point/tet:te/otnt:client-svc"

> This subtree specifies the client traffic type supported by a link termination point. By configuring it, an attacker may create an unauthorized client traffic path. By removing it, a malicious attacker may cause client traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding OTN nodes and OTN links in this OTN topology and the connected topologies.

- "otnt:otn-bandwidth"

> This subtree specifies the configurations of OTN technology-specific information under any occurrence of the tet:te-bandwidth container, as defined in {{!RFC8795}} (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:max-resv-link-bandwidth/tet:te-bandwidth/otnt:otn-bandwidth"). By configuring the OTN bandwidth attributes, an attacker may create an unauthorized OTN traffic path. By removing or modifying it, a malicious attacker may cause OTN traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding OTN nodes and OTN links in this OTN topology and the connected OTN topologies.

- "otnt:otn-label-range"

> This subtree specifies the configurations of OTN technology-specific label range information under any occurrence of the tet:te-label-restriction container, as defined in {{!RFC8795}} (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction\otnt:otn-label-range"). By configuring the OTN label range attributes, an attacker may create an unauthorized OTN traffic path. By removing or modifying, a malicious attacker may cause OTN traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding OTN nodes and OTN links in this OTN topology and the connected OTN topologies.

- "otnt:otn-label"

> This subtree specifies the configurations of OTN technology-specific label information under any occurrence of the tet:te-label container, as defined in {{!RFC8795}} (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/tet:label-start/tet:te-label/tet:technology/otnt:otn-label"). By configuring, removing or modifying the OTN label attributes, a malicious attacker may cause OTN traffic to be disabled or misrouted. Such traffic changes may also affect the traffic on the surrounding OTN nodes and OTN links in this OTN topology and the connected OTN topologies.

Some of the readable data nodes in this YANG module may be considered
sensitive or vulnerable in some network environments.
It is thus important to control read access (e.g., via get, get-config, or
notification) to these data nodes.
Specifically, the following subtrees and data nodes have particular sensitivities/vulnerabilities:

- "/nw:networks/nw:network/nw:network-types/tet:te-topology/otnt:otn-topology"

> Unauthorized access to this subtree can disclose the OTN topology type.

- "/nw:networks/nw:network/nw:node/tet:te/tet:te-node-attributes/otnt:otn-node"

> Unauthorized access to this subtree can disclose the OTN nodes.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:otn-link/otnt:odtu-flex-type"

> This node is used, together with the other attributes in the otn-bandwidth container, to compute the OTN bandwidth information for an OTN link, as described in {{sec-bandwidth}}. Unauthorized access to this data node can disclose the OTN bandwidth information of OTN links.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:otn-link/otnt:tsg"

> Unauthorized access to this data node can disclose configuration information of OTN links.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:otn-link/otnt:distance"

> Unauthorized access to this data node can disclose state information of OTN links.

- "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/otnt:client-svc"

> Unauthorized access to this data node can disclose capabilities of OTN links.

- "/nw:networks/nw:network/nw:node/nt:termination-point/tet:te/otnt:otn-link-tp/otnt:odtu-flex-type"

> This node is used, together with the other attributes in the otn-bandwidth container, to compute the OTN bandwidth information for an OTN link termination point, as described in {{sec-bandwidth}}. Unauthorized access to this data node can disclose the OTN bandwidth information of OTN link termination points.

- "/nw:networks/nw:network/nw:node/nt:termination-point/tet:te/otnt:client-svc"

> Unauthorized access to this data node can disclose capabilities of OTN link termination points.

- "otnt:otn-bandwidth"

> This subtree specifies the configurations of OTN technology-specific information under any occurrence of the tet:te-bandwidth container, as defined in {{!RFC8795}} (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:max-resv-link-bandwidth/tet:te-bandwidth/otnt:otn-bandwidth"). Unauthorized access to this data node can disclose the OTN bandwidth information of OTN links and link termination points.

- "otnt:otn-label-range"

> This subtree specifies the configurations of OTN technology-specific label range information under any occurrence of the tet:te-label-restriction container, as defined in {{!RFC8795}} (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction\otnt:otn-label-range"). Unauthorized access to this data node can disclose the state information of OTN links and link termination points.

- "otnt:otn-label"

> This subtree specifies the configurations of OTN technology-specific label information under any occurrence of the tet:te-label container, as defined in {{!RFC8795}} (e.g., "/nw:networks/nw:network/nt:link/tet:te/tet:te-link-attributes/tet:label-restrictions/tet:label-restriction/tet:label-start/tet:te-label/tet:technology/otnt:otn-label"). Unauthorized access to this data node can disclose the state information of OTN links and link termination points.

This YANG module does not define RPC operations.

This YANG module uses groupings from other YANG modules that
define nodes that may be considered sensitive or vulnerable
in network environments. Refer to the Security Considerations
of {{!I-D.ietf-ccamp-layer1-types}} for information as to which nodes may
be considered sensitive or vulnerable in network environments.

Finally, the YANG module described in this document augments the "ietf-network" YANG module {{!RFC8345}} and the "ietf-te-topology" YANG module {{!RFC8795}} by adding data nodes. The security considerations for the subtrees described in those RFCs apply equally to the new data nodes that this module adds.

--- back

# YANG Tree {#yang-tree}

This section provides the YANG Tree of the OTN topology data model.

~~~~ ascii-art
{::include ../../../YANG/ccamp/otn-topology/ietf-otn-topology.tree}
~~~~

# JSON Examples

This appendix contains an example of an instance data tree in JSON
encoding {{?RFC7951}}.

The example instantiates the "ietf-otn-topology" model for the OTN
topology depicted in {{fig-example}} below.

The OTN topology consists of three nodes (D1, D2, and D3) with three
link termination (LTPs) each: two LTPs which terminates the links
that belongs to the OTN topology and one LTP which terminates inter-
domain links, as defined in {{!RFC8795}}.

The OTN links within the OTN network are 100G OTN links while the
links at the edge of the network are 10G links.  All these OTN links
support ODU4, ODU2 and ODU0 connections.  The link between nodes D1
and D2 also supports ODUflex.

The OTN links within the OTN network are bidirectional and
symmetrical: for this reasons, the link attributes (e.g., support for
OTN switching capability or transparent client signal and the OTN
maximum link bandwidth) are instantiated only on the link
representing the forward direction, while the link representing the
reverse direction are instantiated without any link attribute (other
than the name) to indicate that the OTN links are bidirectional and
symmetrical.

The link between nodes D1 and D2 is an example of a multi-function
link, as defined in {{sec-attributes}}, which can support both OTN and 100G
client signal (e.g., 100GE): the interface-switching-capability list
indicates support for OTN switching capability and the client-svc
presence container is instantiated.

For the LTPs which terminate OTN links, only the identifiers
information is instantiated.  All the other properties are defined in
the links they terminate.

For the LTPs at the edge network, additional properties are
instantiated to indicate whether the link can support OTN or
transparent client signals.  In particular:

- LTP 1 on Node D1 is an example of an LTP terminating a multi-
function access link, as defined in {{sec-attributes}}, which can support
both OTN and 10G client signals (e.g., 10GE and STM-64): the
interface-switching-capability list indicates support for OTN
switching capability and the client-svc presence container is
instantiated;

- LTP 2 on Node D2 is an example of an LTP which can support only
10G OTN (ODU2) signal: the interface-switching-capability list
indicates support for OTN switching capability and the client-svc
presence container is not instantiated;

- LTP 3 on Node D3 is an example of an LTP which can support only
10G (e.g., 10GE and STM-64) client signals: the interface-
switching-capability list does not indicate support for OTN
switching capability and the client-svc presence container is
instantiated.

~~~~ ascii-art
                   +------------+                   +------------+
                   |     D1     |                   |     D2     |
                  /-\          /-\                 /-\          /-\
                  | | 1        | |---------------->| | 1        | |
                  | |        2 | |<----------------| |        2 | |
                  \-/    3     \-/                 \-/    3     \-/
                   |   /----\   |                   |   /----\   |
                   +---|    |---+                   +---|    |---+
                       \----/                           \----/
                        A  |                             A  |
                        |  |                             |  |
                        |  |                             |  |
                        |  |       +------------+        |  |
                        |  |       |     D3     |        |  |
                        |  |      /-\          /-\       |  |
                        |  +----->| | 1        | |-------+  |
                        +---------| |        2 | |<---------+
                                  \-/    3     \-/
                                   |   /----\   |
                                   +---|    |---+
                                       \----/
~~~~
{: #fig-example title="Example of OTN topology"}

~~~~ ascii-art
{::include ../../../YANG/ccamp/otn-topology/otn-topology-example.json.folded}
~~~~

{:numbered="false"}

# Acknowledgments

We would like to thank Igor Bryskin, Zhe Liu, Zheyu Fan and Daniele
Ceccarelli for their comments and discussions.
