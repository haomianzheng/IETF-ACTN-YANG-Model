---
title: >
  A YANG Data Model for Optical Transport Network (OTN) Tunnels and Label Switched Paths
abbrev: OTN Tunnel Model
category: std

docname: draft-ietf-ccamp-otn-tunnel-model-latest
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
  github: "haomianzheng/IETF-ACTN-YANG-Model"

author:
  -
    name: Haomian Zheng
    org: Huawei Technologies
    street: H1, Huawei Xiliu Beipo Village, Songshan Lake
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
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    name: Victor Lopez
    org: Nokia
    email: victor.lopez@nokia.com
  -
    name: Yunbin Xu
    org: CAICT
    email: xuyunbin@caict.ac.cn

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
    name: Rajan Rao
    org: Infinera
    email: rrao@infinera.com
  -
    name: Yunbo Li
    org: China Mobile
    email: liyunbo@chinamobile.com
  -
    name: Dieter Beller
    org: Nokia
    email: dieter.beller@nokia.com
  -
    name: To-Be-Added
    org: To-Be-Added
    email: To-Be-Added
  -
    name: Xian Zhang
    org: Huawei Technologies
    email: Huawei Technologies
  -
    name: Lei Wang
    org: China Mobile
    email: wangleiyj@chinamobile.com
  -
    name: Oscar Gonzalez de Dios
    ins: O. Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com

normative:
  ITU-T_G.709:
    title: Interfaces for the optical transport network
    author:
      org: ITU-T Recommendation G.709
    date: March 2020
    seriesinfo: ITU-T G.709

informative:

--- abstract

This document describes the YANG data model for tunnels in OTN TE
networks.  The model can be used to do the configuration in order to
establish the tunnel in OTN network.  This work is independent with
the control plane protocols.

--- middle

# Introduction

OTN transport networks, specified in {{ITU-T_G.709}}, can carry various
types of client signals.  In many cases, the client signal is carried
over an OTN tunnel across connected domains in a multi-domain
network.

This document provides YANG model for creating OTN tunnel.  The model
augments the generic TE Tunnel model specified in
{{!I-D.ietf-teas-yang-te}}.

The YANG module ietf-otn-tunnel defined in this document conforms to
the Network Management Datastore Architecture (NMDA) defined in
{{!RFC8342}}.

## Terminology and Notations

Refer to {{!I-D.ietf-ccamp-otn-topo-yang}} for the OTN specific terms
terms used in this document.

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

## Tree Diagram

A simplified graphical representation of the data model is used in
{{yang-tree}} of this this document.  The meaning of the symbols in these
diagrams is defined in {{?RFC8340}}.

## Prefix in Data Node Names

In this document, names of data nodes and other data model objects
are prefixed using the standard prefix associated with the
corresponding YANG imported modules, as shown in the following table.

| Prefix      | YANG module             | Reference
| l1-types    | ietf-layer1-types       | \[RFC YYYY]
| otn-tnl     | ietf-otn-tunnel         | RFC XXXX
| te          | ietf-te                 | \[RFC ZZZZ]
{: #tab-prefixes title="Prefixes and corresponding YANG modules"}

RFC Editor Note: Please replace XXXX with the number assigned to the
RFC once this draft becomes an RFC.  Please replace YYYY with the RFC
numbers assigned to {{!I-D.ietf-ccamp-layer1-types}}.  Please replace
ZZZZ with the RFC numbers assigned to {{!I-D.ietf-teas-yang-te}}.

# OTN Tunnel Model Description

## Overview of OTN Tunnel Model

This document aims to describe the data model for OTN tunnel.  The
OTN tunnel model is using TE tunnel {{!I-D.ietf-teas-yang-te}} as a
basic model and augments it with OTN-specific parameters, including
the bandwidth information and label information.  {{fig-overview}} shows the
augmentation relationship.

~~~~ ascii-art
                           +----------------+
              TE generic   |     ietf-te    |
                           +----------------+
                                    ^
                                    |
                                    | Augments
                                    |
                           +--------+--------+
              OTN          | ietf-otn-tunnel |
                           +-----------------+
~~~~
{: #fig-overview title="Relationship between OTN and TE tunnel models"}

It is also worth noting that the OTN tunnel provisioning is usually
based on the OTN topology.  Therefore the OTN tunnel model is usually
used together with OTN topology model specified in
{{!I-D.ietf-ccamp-otn-topo-yang}}.  The OTN tunnel model also imports a
few type modules, including ietf-layer1-types, ietf-te-types and
ietf-inet-types.  The OTN-specific attributes in {{!RFC7139}}, including
the Tributary Slot (TS) and Tributary Port Number (TPN), can be used
to represent the bandwidth and label information.  These attributes
have been specified in {{!I-D.ietf-ccamp-layer1-types}} and used in this
document for augmentation of the generic TE tunnel model.

More scenarios and model applications can be found in
{{?I-D.ietf-ccamp-transport-nbi-app-statement}} and
{{?I-D.ietf-teas-actn-yang}}.

## Bandwidth Augmentation

The model augments all the occurrences of the te-bandwidth container
with the OTN technology specific attributes using the otn-link-
bandwidth and otn-path-bandwidth groupings defined in
{{!I-D.ietf-ccamp-layer1-types}}.

## Label Augmentation

The model augments all the occurrences of the label-restriction list
with OTN technology specific attributes using the otn-label-range-
info grouping defined in {{!I-D.ietf-ccamp-layer1-types}}.

Moreover, the model augments all the occurrences of the te-label
container with the OTN technology specific attributes using the otn-
label-start-end, otn-label-hop and otn-label-step groupings defined
in {{!I-D.ietf-ccamp-layer1-types}}.

{: #yang-tree}

# OTN Tunnel YANG Tree

~~~~ ascii-art
{::include-fold ../../yang/otn-tunnel/ietf-otn-tunnel.tree}
~~~~
{: #fig-otn-tunnel-tree artwork-name="ietf-otn-tunnel.tree"}

# OTN Tunnel YANG Code

~~~~ yang
{::include ../../yang/otn-tunnel/ietf-otn-tunnel.yang}
~~~~
{: #fig-otn-tunnel-yang sourcecode-markers="true" sourcecode-name="ietf-otn-tunnel@2024-03-21.yang"}

# IANA Considerations

IANA is requested to register the following URI in the "ns" subregistry within the "IETF XML Registry" {{!RFC3688}}:

~~~~
      URI: urn:ietf:params:xml:ns:yang:ietf-otn-tunnel
      Registrant Contact: The IESG
      XML: N/A; the requested URI is an XML namespace.
~~~~

IANA is requested to register the following YANG module in the "YANG Module Names" subregistry {{!RFC6020}} within the "YANG Parameters" registry.

~~~~
      name:         ietf-otn-tunnel
      namespace:    urn:ietf:params:xml:ns:yang:ietf-otn-tunnel
      prefix:       otn-tnl
      reference:    RFC XXXX
~~~~

> RFC Editor Note: Please replace XXXX with the number assigned to the RFC once this draft becomes an RFC.

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

- "otnt:otn-bandwidth"

> This subtree specifies the configurations of OTN technology-specific information under any occurrence of the tet:te-bandwidth container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:te-bandwidth/te:technology/otnt:otn/otnt:otn-bandwidth"). By configuring the OTN bandwidth attributes, an attacker may create an unauthorized OTN traffic path. By removing or modifying it, a malicious attacker may cause OTN traffic to be disabled or misrouted.

- "otnt:otn-label-range"

> This subtree specifies the configurations of OTN technology-specific label range information under any occurrence of the tet:label-restriction container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:path-in-segment/te:label-restrictions/te:label-restriction/otnt:otn-label-range"). By configuring the OTN label range attributes, an attacker may create an unauthorized OTN traffic path. By removing or modifying, a malicious attacker may cause OTN traffic to be disabled or misrouted.

- "otnt:otn-label"

> This subtree specifies the configurations of OTN technology-specific label information under any occurrence of the tet:te-label container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:explicit-route-objects/te:route-object-include-exclude/te:type/te:label/te:label-hop/te:te-label/te:technology/otnt:otn/otnt:otn-label"). By configuring, removing or modifying the OTN label attributes, a malicious attacker may cause OTN traffic to be disabled or misrouted.

Some of the readable data nodes in this YANG module may be considered
sensitive or vulnerable in some network environments.
It is thus important to control read access (e.g., via get, get-config, or
notification) to these data nodes.
Specifically, the following subtrees and data nodes have particular sensitivities/vulnerabilities:

- "otnt:otn-bandwidth"

> This subtree specifies the configurations of OTN technology-specific information under any occurrence of the tet:te-bandwidth container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:te-bandwidth/te:technology/otnt:otn/otnt:otn-bandwidth"). Unauthorized access to this data node can disclose the OTN bandwidth information of OTN tunnels and LSPs.

- "otnt:otn-label-range"

> This subtree specifies the configurations of OTN technology-specific label range information under any occurrence of the tet:label-restriction container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:path-in-segment/te:label-restrictions/te:label-restriction/otnt:otn-label-range"). Unauthorized access to this data node can disclose the state information of OTN tunnels and LSPs.

- "otnt:otn-label"

> This subtree specifies the configurations of OTN technology-specific label information under any occurrence of the tet:te-label container, as defined in {{!I-D.ietf-teas-yang-te}} (e.g., "/te:te/te:tunnels/te:tunnel/te:primary-paths/te:primary-path/te:explicit-route-objects/te:route-object-include-exclude/te:type/te:label/te:label-hop/te:te-label/te:technology/otnt:otn/otnt:otn-label"). Unauthorized access to this data node can disclose the state information of OTN tunnels and LSPs.

This YANG module does not define RPC operations.

This YANG module uses groupings from other YANG modules that
define nodes that may be considered sensitive or vulnerable
in network environments. Refer to the Security Considerations
of {{!I-D.ietf-ccamp-layer1-types}} for information as to which nodes may
be considered sensitive or vulnerable in network environments.

Finally, the YANG module described in this document augments the "ietf-te" YANG module {{!I-D.ietf-teas-yang-te}} by adding data nodes. The security considerations for the subtrees described in those RFCs apply equally to the new data nodes that this module adds.

--- back

# Acknowledgments
{:numbered="false"}

We would like to thank Yu Chaode for his comments and discussions.