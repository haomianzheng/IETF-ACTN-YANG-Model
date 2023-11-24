---
title: "OTN Tunnel YANG Model"
abbrev: "OTN Tunnel YANG Model"
category: std

docname: draft-ietf-ccamp-otn-tunnel-model-20
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
    name: TBD
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
{::include ../../../YANG/ccamp/otn-tunnel/ietf-otn-tunnel.tree}
~~~~
{: #fig-otn-tunnel-tree artwork-name="ietf-otn-tunnel.tree"}

# OTN Tunnel YANG Code

~~~~ yang
{::include ../../../YANG/ccamp/otn-tunnel/ietf-otn-tunnel.yang}
~~~~
{: #fig-otn-tunnel-yang sourcecode-markers="true" sourcecode-name="ietf-otn-tunnel@2023-10-12.yang"}

# Security Considerations

The data following the model defined in this document is exchanged
via, for example, the interface between an orchestrator and a
transport network controller.  The security concerns mentioned in
{{!I-D.ietf-ccamp-client-signal-yang}} also applies to this document.

The YANG module defined in this document can be accessed via the
RESTCONF protocol defined in {{!RFC8040}}, or maybe via the NETCONF
protocol {{!RFC6241}}.

# IANA Considerations

This document requests IANA to register the following URIs in the "ns" subregistry within the "IETF XML Registry" {{!RFC3688}}. Following the format in {{!RFC3688}}, the following registrations are requested.

~~~~
      URI: urn:ietf:params:xml:ns:yang:ietf-otn-tunnel
      Registrant Contact: The IESG
      XML: N/A; the requested URI is an XML namespace.
~~~~

This document requests IANA to register the following YANG modules in the "IANA Module Names" {{!RFC6020}}. Following the format in {{!RFC6020}}, the following registrations are requested:

~~~~
      name:         ietf-otn-tunnel
      namespace:    urn:ietf:params:xml:ns:yang:ietf-otn-tunnel
      prefix:       otn-tnl
      reference:    RFC XXXX
~~~~

RFC Editor Note: Please replace XXXX with the number assigned to the
RFC once this draft becomes an RFC.

--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.
