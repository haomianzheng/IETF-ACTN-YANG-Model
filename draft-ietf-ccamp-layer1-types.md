---
title: "Common YANG Data Types for Layer 1 Networks"
abbrev: "L1 Common YANG Types"
category: std

docname: draft-ietf-ccamp-layer1-types-latest
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
  latest: "https://haomianzheng.github.io/IETF-ACTN-YANG-Model/draft-ietf-ccamp-layer1-types.html"

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
    city: Milan
    country: Italy
    email: italo.busi@huawei.com

contributor:
  -
    name: Dieter Beller
    org: Nokia
    email: dieter.beller@nokia.com
  -
    name: Sergio Belotti
    org: Nokia
    email: sergio.belotti@nokia.com
  -
    name: Yanlei Zheng
    org: China Unicom
    email: zhengyanlei@chinaunicom.cn
  -
    name: Aihua Guo
    org: Futurewei
    email: aihuaguo@futurewei.com
  -
    name: Young Lee
    org: Samsung
    email: younglee.tx@gmail.com
  -
    name: Lei Wang
    org: China Mobile
    email: wangleiyj@chinamobile.com
  -
    name: Oscar Gonzalez de Dios
    ins: O. Gonzalez de Dios
    org: Telefonica
    email: oscar.gonzalezdedios@telefonica.com
  -
    name: Xufeng Liu
    org: Volta Networks
    email: xufeng.liu.ietf@gmail.com
  -
    name: Yunbin Xu
    org: CAICT
    email: xuyunbin@caict.ac.cn
  -
    name: Anurag Sharma
    org: Google
    email: ansha@google.com
  -
    name: Rajan Rao
    org: Infinera
    email: rrao@infinera.com
  -
    name: Victor Lopez
    org: Telefonica
    email: victor.lopez@nokia.com
  -
    name: Yunbo Li
    org: China Mobile
    email: liyunbo@chinamobile.com
  -
    name: Daniel King
    org: Old Dog Consulting
    email: daniel@olddog.co.uk

normative:
  ANSI_INCITS_230:
    title: Information Technology - Fibre Channel - Physical and Signaling Interface (FC-PH).
    author:
      org: American National Standards Institute
    date: January 1994
    seriesinfo: ANSI INCITS 230-1994 (R1999)
    target: https://webstore.ansi.org/standards/incits/ansiincits2301994r1999
  ANSI_T1.105:
    title: Synchronous Optical Network (SONET) Basic Description including Multiplex Structure, Rates, and Formats
    author:
      org: American National Standards Institute
    date: May 2001
    seriesinfo: ANSI T1.105-2001
    target: https://webstore.ansi.org/standards/atis/t11052001
  IEEE_754:
    title: IEEE Standard for Floating-Point Arithmetic
    author:
      org: Institute of Electrical and Electronics Engineers
    date: July 2019
    seriesinfo: IEEE 754-2019
    target: https://ieeexplore.ieee.org/document/8766229
  IEEE_802.3:
    title: IEEE Standard for Ethernet
    author:
      org: Institute of Electrical and Electronics Engineers
    date: June 2018
    seriesinfo: IEEE 802.3-2018
    target: https://ieeexplore.ieee.org/document/8457469
  ISO_IEC_9899_1999:
    title: Programming Languages - C
    author:
      org: International Organization for Standardization
    date: December 1999
    seriesinfo: ISO/IEC 9899:1999
    target: https://www.iso.org/standard/29237.
  ITU-T_G.7044:
    title: Hitless adjustment of ODUflex(GFP)
    author:
      org: International Telecommunication Union
    date: October 2011
    seriesinfo: ITU-T G.7044
    target: https://www.itu.int/rec/T-REC-G.7044
  ITU-T_G.707:
    title: Network node interface for the synchronous digital hierarchy (SDH)
    author:
      org: International Telecommunication Union
    date: January 2007
    seriesinfo: ITU-T G.707
    target: https://www.itu.int/rec/T-REC-G.707
  ITU-T_G.709:
    title: Interfaces for the optical transport network
    author:
      org: International Telecommunication Union
    date: June 2020
    seriesinfo: ITU-T G.709
    target: https://www.itu.int/rec/T-REC-G.709
  MEF_63:
    title: Subscriber Layer1 Service Attributes Technical Specification
    author:
      org: Metro Ethernet Forum
    date: August 2018
    seriesinfo: MEF 63
    target: https://www.mef.net/wp-content/uploads/2018/08/MEF-63.pdf

informative:
  ITU-T_G.Sup43:
    title: Transport of IEEE 10GBASE-R in optical transport networks (OTN)
    author:
      org: International Telecommunication Union
    date: November 2011
    seriesinfo: ITU-T G.Sup43
    target: https://www.itu.int/rec/T-REC-G.Sup43


--- abstract

This document defines a collection of common common data types,
identities, and groupings in the YANG data modeling language. These
derived common common data types, identities, and groupings are
intended to be imported by modules that model Layer 1 configuration
and state capabilities. The Layer 1 types are representative of
Layer 1 client signals applicable to transport networks, such as
Optical Transport Networks (OTN). The Optical Transport Network
(OTN) data structures are included in this document as Layer 1 types.


--- middle

# Introduction

This document specifies common data types, groupings, and identities
for use in YANG {{!RFC7950}} data models of Layer 1 networks. The
derived types and groupings apply to Traffic Engineered (TE) Layer 1
networks.

The Layer 1 (L1) Optical Transport Network (OTN) is specified in
{{?RFC7062}}. The corresponding routing and signaling protocols are
specified in {{?RFC7138}} and {{!RFC7139}}. The types and groupings
defined in this document are consistent with those documents, and can
be imported into other Layer 1 data models, including but not limited
to, {{?I-D.ietf-ccamp-otn-topo-yang}},
{{?I-D.ietf-ccamp-otn-tunnel-model}},
{{?I-D.ietf-ccamp-client-signal-yang}} and {{?I-D.ietf-ccamp-l1csm-yang}}.

The document is consistent with other specifications, including
{{MEF_63}} for Layer 1 service attributes, {{ITU-T_G.709}} and
{{ITU-T_G.Sup43}} for OTN data plane definitions.

The YANG data model in this document only defines groupings, typedef,
and identities. It does not define any configuration or state data,
as specified in the Network Management Datastore Architecture defined
in {{?RFC8342}}.

# Terminology and Notations

{::boilerplate bcp14-tagged}

Specific terms used within this document are as follows:

OTN:
: Optical Transport Network.

ODU:
: Optical Data Unit. An ODU has the frame structure and
overhead, as defined in Figure 12-1 of {{ITU-T_G.709}}. ODUs can be
formed in two ways: a) by encapsulating a single non-OTN client,
such as SONET/SDH (Synchronous Optical Network / Synchronous
Digital Hierarchy) or Ethernet, or b) by multiplexing lower-rate
ODUs. In general, the ODU layer represents the path layer in OTN.
The only exception is the ODUCn signal (defined below), which is
defined to be a section-layer signal. In the classification based
on bitrates of the ODU signals, ODUs are of two types: fixed rate
and flexible rate. Flexible-rate ODUs, called "ODUflex", have a
rate that is 239/238 times the bitrate of the client signal they
encapsulate.

ODUCn:
: Optical Data Unit-C. This signal has a bandwidth of
approximately 100 Gbit/s and is of a slightly higher bitrate than
the fixed rate ODU4 signal. This signal has the format defined in
Figure 12-1 of {{ITU-T_G.709}}. This signal represents the building
block for constructing a higher-rate signal called "ODUCn".

ODUk:
: Optical Data Unit-k, where k is one of {0, 1, 2, 2e, 3, 4}.
The term "ODUk" refers to an ODU whose bitrate is fully specified
by the index k. The bitrates of the ODUk signal for k = {0, 1, 2,
2e, 3, 4} are approximately 1.25 Gbit/s, 2.5 Gbit/s, 10 Gbit/s,
10.3 Gbit/s, 40 Gbit/s, and 100 Gbit/s, respectively.

LO ODU:
: Lower Order ODU. The LO ODUj (j can be 0, 1, 2, 2e, 3, 4,
or flex) represents the container transporting a client of the OTN
that is either directly mapped into an OTUk (k = j) or multiplexed
into a server HO ODUk (k > j) container.

HO ODU:
: Higher Order ODU. The HO ODUk (k can be 1, 2, 2e, 3, or 4)
represents the entity transporting a multiplex of LO ODUj
tributary signals in its OPUk area.

The reader may also refer to {{?RFC7062}} and {{?RFC9376}} for other key
terms used in this document. The terminology for describing YANG
data models can be found in {{!RFC7950}}.

# Prefix in Data Node Names

In this document, the names of data nodes and other data model
objects are prefixed using the standard prefix associated with the
corresponding YANG imported modules, as shown in {{tab-prefixes}}.

| Prefix      | YANG module             | Reference
| rt-types    | ietf-routing-types      | {{!RFC8294}}
| l1-types    | ietf-layer1-types       | \[RFCYYYY]
{: #tab-prefixes title="Prefixes and Corresponding YANG Modules"}

> RFC Editor Note:
Please replace XXXX with the number assigned to the RFC once this draft becomes an RFC.

# Layer 1 Types Overview {#DM}

## Relationship with other Modules

This document defines one YANG module for common Layer 1 types. The
aim is to specify common Layer 1 TE types (i.e., typedef, identity,
grouping) that can be imported by layer 1 specific technology, for
example, layer 1 OTN, in its technology-specific modules, such as
topology and tunnels. It is worth noting that the generic traffic-
engineering (TE) types module is specified as ietf-te-types in
{{!I-D.ietf-teas-rfc8776-update}}, and both YANG modules, ietf-te-types
and ietf-layer1-types, will need importing when the OTN is
configured. Generic attributes such as te-bandwidth and te-label,
which are specified as ietf-te-types in
{{!I-D.ietf-teas-rfc8776-update}}, need to be augmented with the OTN-specific
attributes, such as odu-type, which are specified as ietf-layer1-types in this document, when OTN is configured.

## Content in Layer 1 Type Module

The module ietf-layer1-types contains the following YANG reusable
types and groupings:

tributary-slot-granularity:
: This specifies the granularity levels for tributary slots utilized
by the server layer Optical Data Unit (ODU). Specifically, it
addresses how ODU links, including both Higher Order Optical Data
Unit-k (HO ODUk) and Optical Data Unit-Cn (ODUCn), accommodate
client layer ODUs within Label Switched Paths (LSPs). These
client layer ODUs could be Lower Order Optical Data Unit-j (LO
ODUj) or ODUk, respectively. The specified granularity levels for
these configurations are 1.25G, 2.5G, and 5G.

odu-type:
: This specifies the type of ODUk LSP, including the types specified
in {{ITU-T_G.709}} and {{!RFC7139}}.
: Since, as described in {{?RFC7963}}, {{ITU-T_G.Sup43}} does not
guarantee interoperability in the data plane for these containers,
the type of ODUk LSPs defined in {{ITU-T_G.Sup43}} and {{?RFC7963}} can
be defined in vendor-specific YANG modules using the odu-type
identity, defined in this document, as the base.

client-signal:
: This specifies the common Layer 1 client signal types, including
ETH {{IEEE_802.3}}, STM-n {{ITU-T_G.707}}, OC {{ANSI_T1.105}} and Fiber
Channel {{ANSI_INCITS_230}}. The input was based on the G-PID types
specified in {{!RFC7139}}.

otn-label-range-type:
: The label range type of OTN is represented in one of two ways,
tributary slots (TS) and tributary port number (TPN), as specified
in {{!RFC7139}}. Two representations are enumerated in the otn-
label-range-type.

otn-link-bandwidth:
: This grouping defines the link bandwidth information, usually as
the number of ODUs that can be supported by the link for each ODU
type: for example an OTN link with 100G bandwidth can support
either 1xODU4, 10xODU2 or 80xODU0.
: It is also used to represent the ODUflex resources available on a
link, as described in {{ODUflex}}.
: This grouping could be used in the OTN topology model for link
bandwidth representation. In general, all the bandwidth-related
sections, which are defined in a generic module, e.g., using the
groupings defined in {{!I-D.ietf-teas-rfc8776-update}}, need to be
augmented with this grouping when used to represent the bandwidth
of an OTN link.

otn-path-bandwidth:
: This grouping defines the path bandwidth information, usually as
the type of ODU (e.g., ODU0, ODU2, ODU4) being set up along the
path.
: In the case of ODUflex paths, more information about the bandwidth
of the ODUflex needs to be provided, as described in {{ODUflex}}.
: This grouping could be used in the OTN topology model for path
bandwidth representation as well as when setting up the OTN
tunnel. In general, all the bandwidth-related sections, which are
defined in a generic module, e.g., using the groupings defined in
{{!I-D.ietf-teas-rfc8776-update}}, need to be augmented with this
grouping when used to represent the bandwidth of an OTN tunnel or
path.

otn-label-range-info:
: This grouping is used to augment the label-restriction list,
defined in {{!I-D.ietf-teas-rfc8776-update}}, with OTN technology-
specific attributes, as defined in {{label}}.

otn-label-start-end:
: This grouping is used to augment the label-start and label-end
containers within the label-restriction list, defined in
{{!I-D.ietf-teas-rfc8776-update}}, with OTN technology-specific
attributes, as defined in {{label}}.

otn-label-step:
: This grouping is used to augment the label-step container within
the label-restriction list, defined in
{{!I-D.ietf-teas-rfc8776-update}}, with OTN technology-specific
attributes, as defined in {{label}}.

otn-label-hop:
: This grouping is used to augment the label-hop container, defined
in {{!I-D.ietf-teas-rfc8776-update}}, with OTN technology-specific
attributes, as defined in {{label}}.

optical-interface-func:
: The optical interface function is specified in {{MEF_63}}.
Identities that describe the functionality are specified to encode
bits for transmission and to decode bits upon reception.

## OTN Label and Label Range {#label}

As described in {{!RFC7139}}, the OTN label usually represents the
Tributary Port Number (TPN) and the related set of Tributary Slots
(TS) assigned to a client layer ODU LSP (LO ODUj or ODUk) on a given
server layer ODU (HO-ODU or ODUCn, respectively) Link (e.g., ODU2 LSP
over ODU3 Link). Some special OTN label values are also defined for
an ODUk LSP being set up over an OTUk Link.

The same OTN label MUST be assigned to the same ODUk LSP at the two
ends of an OTN Link.

As described in {{!RFC7139}}, TPN can be a number from 1 to 4095 and TS
are numbered from 1 to 4095, although the actual maximum values
depend on the type of server layer ODU. For example, a server layer
ODU4 provides 80 tributary slots (numbered from 1 to 80), and the TPN
values can be any number from 1 to 80.

The OTN Label Range specifies the available values for the Tributary
Port Number (TPN) and Tributary Slots (TS) for setting up ODUk Label
Switched Paths (LSPs) over an OTN Link, with priorities as defined in
{{!RFC4203}}. This range is established according to the guidelines in
{{!RFC7139}}.

The OTN Label Range is defined by the label-restriction list, defined
in {{!I-D.ietf-teas-rfc8776-update}}, which, for OTN, SHOULD be
augmented using the otn-label-range-info grouping.

Each entry in the label-restriction list represents either the range
of the available TPN values or the range of the available TS values:
the range-type attribute in the otn-label-range-info grouping defines
the type of range for each list entry.

Each entry of the label-restriction list, as defined in
{{!I-D.ietf-teas-rfc8776-update}}, defines a label-start, a label-end, a
label-step, and a range-bitmap. The label-start and label-end
definitions for OTN SHOULD be augmented using the otn-label-start-end
grouping. The label-step definition for OTN SHOULD be augmented
using the otn-label-step grouping. It is expected that the otn-
label-step will always be equal to its default value (i.e., 1), which
is defined in {{!I-D.ietf-teas-rfc8776-update}}.

As described in {{!RFC7139}}, in some cases, the TPN assignment rules
are flexible (e.g., ODU4 Link) while in other cases the TPN
assignment rules are fixed (e.g., ODU1 Link). In the former case,
both TPN and TS ranges are reported, while in the latter case, the
TPN range is not reported which indicates that the TPN SHALL be set
equal to the TS number assigned to the ODUk LSP.

As described in {{!RFC7139}}, in some cases, the TPN assignment rules
depend on the TS Granularity (e.g., ODU2 or ODU3 Links). Different
entries in the label-restriction list will report different TPN
ranges for each TS granularity supported by the link, as indicated by
the tsg attribute in the otn-label-range-info grouping.

As described in {{!RFC7139}}, in some cases the TPN ranges are different
for different types of ODUk LSPs. For example, on an ODU2 Link with
1.25G TS granularity, the TPN range is 1-4 for ODU1 but 1-8 for ODU0
and ODUflex. Therefore, different entries in the label-restriction
list will report different TPN ranges for a different set of ODUk
types, as indicated by the odu-type-list in the otn-label-range-info
grouping.

Appendix A provides some examples of how the TPN and TS label ranges
described in Table 3 and Table 4 of {{!RFC7139}} can be represented in
YANG using the groupings defined in this document.

## ODUflex {#ODUflex}

ODUflex is a type of ODU with a flexible bit rate which is configured
when setting up an ODUflex LSP.

{{ITU-T_G.709}} defines six types of ODUflex: ODUflex(CBR),
ODUflex(GFP), ODUflex(GFP,n,k), ODUflex(IMP), ODUflex(IMP,s), and
ODUflex(FlexE-aware).

The main difference between these types of ODUflex is the formula
used to calculate the nominal bit rate of the ODUflex, as described
in Table 7-2 of {{ITU-T_G.709}}. A YANG choice has been defined to
describe these cases:

~~~~ ascii-art
       +--rw (oduflex-type)?
          +--:(generic)
          |  +--rw nominal-bit-rate        union
          +--:(cbr)
          |  +--rw client-type             identityref
          +--:(gfp-n-k)
          |  +--rw gfp-n                   uint8
          |  +--rw gfp-k?                  l1-types:gfp-k
          +--:(flexe-client)
          |  +--rw flexe-client
          |          l1-types:flexe-client-rate
          +--:(flexe-aware)
          |  +--rw flexe-aware-n           uint16
          +--:(packet)
             +--rw opuflex-payload-rate    union
~~~~

The OPUflex payload rate can be expressed either in a floating point
notation or a scientific notation, as defined in {{IEEE_754}} and
{{ISO_IEC_9899_1999}}.

The 'generic' case has been added to allow the ODUflex nominal bit
rate to be defined independently of the type of ODUflex. This could
be useful for forward compatibility in the transit domain/nodes where
the set up of ODUflex LSPs does not depend on the ODUflex type.

In order to simplify interoperability the 'generic' case SHOULD be
used only when needed; the ODUflex type-specific case SHOULD be used
whenever possible.

The 'cbr' case is used for Constant Bit Rate (CBR) client signals.
The client-type indicates which CBR client signal is carried by the
ODUflex and, implicitly, the client signal bit rate, which is then
used to calculate the ODUflex(CBR) nominal bit rate as described in
Table 7-2 of {{ITU-T_G.709}}.

The 'gfp-n-k' case is used for GFP-F mapped client signals based on
ODUk.ts and 'n' 1.25G tributary slots. 'gfp-k' defines the nominal
bit-rate of the ODUk.ts which, together with the value of 'gfp-n', is
used to calculate the ODUflex(GFP,n,k) nominal bit rate as described
in Table 7-8 and Table L-7 of {{ITU-T_G.709}} . With a few exceptions,
shown in Table L-7 of {{ITU-T_G.709}}, the nominal bit-rate of the
ODUk.ts could be inferred from the value of 'n', as shown in
Table 7-8 of {{ITU-T_G.709}} and therefore the 'gfp-k' is optional.

The 'flexe-client' case is used for Idle Mapping Procedure (IMP)
mapped FlexE client signals, The 'flexe-client' represents the type
of FlexE client carried by the ODUflex which implicitly defines the
value of 's' used to calculate the ODUflex(s) nominal bit rate as
described in Table 7-2 of {{ITU-T_G.709}}. The '10G' and '40G'
enumeration values are used for 10G and 40G FlexE clients to
implicitly define the values of s=2 and s=8. For the 'n x 25G' FlexE
Clients the value of 'n' is used to define the value of s=5 x n.

The 'flexe-aware' case is used for FlexE-aware client signals. The
flexe-aware-n represents the value n (n = n1 + n2 + ... + np) which
is used to calculate the ODUflex(FlexE-aware) nominal bit rate as
described in Table 7-2 of {{ITU-T_G.709}}.

The 'packet' case is used for both the GFP-F mapped client signals
and the IMP mapped client signals. The opuflex-payload-rate is
either the GFP-F encapsulated-packet client nominal bit rate or the
64b/66b encoded-packet client nominal bit rate. The calculation of
ODUflex(GFP) nominal bit rate is defined in Section 12.2.5 of
{{ITU-T_G.709}}, and the calculation of ODUflex(IMP) nominal bit rate
is defined in Section 12.2.6 of {{ITU-T_G.709}}. The same formula is
used in both cases.

Sections 5.1 and 5.2 of {{!RFC7139}} defines two rules to compute the
number of tributary slots to be allocated to ODUflex(CBR) and
ODUflex(GFP) LSPs when carried over a HO-ODUk link. According to
Section 19.6 of {{ITU-T_G.709}}, the rules in Section 5.2 apply only to
ODUflex(GFP,n,k) while the rules defined in Section 5.1 apply to any
other ODUflex type, including, but not limited, to ODUflex(CBR).
Section 20.5 of {{ITU-T_G.709}} defines the rules for computing the
number of tributary slots to be allocated to ODUflex LSPs when
carried over an ODUCn link.

In order to compute the number of tributary slots required to set up
an ODUflex LSP, or ODUflex LSPs, the type of Optical channel Data
Tributary Unit (ODTU) is reported for the OTN Links or the OTN LTPs
(Link Termination Points).

Following the {{ITU-T_G.709}} definitions, the rules defined for
ODUflex(GFP,n,k) are used only when the 'gfp-n-k' case is used. In
all the other cases, including the (generic) case, the rules defined
for any other ODUflex type are used.

The number of available ODUs, defined for each ODUk type, including
ODUflex, does not provide sufficient information to infer the OTN
link bandwidth availability for ODUflex LSPs.

The OTN link bandwidth definitions for ODUflex LSPs also depend on
the number of tributary slots (TS) and on the type of ODTU used to
compute the number of TS required to set up an ODUflex LSP, according
to the rules defined in Section 19.6 and Section 20.5 of
{{ITU-T_G.709}}, as described above.

Similarly, bandwidth constraints for ODUflex LSPs of the OTN
connectivity matrix and of the OTN local link connectivity entries
depend also on the number of tributary slots (TS) and on the type of
ODTU used to compute the number of TS required to set up an ODUflex
LSP along the underlay path, according to the rules defined in
Section 19.6 and Section 20.5 of {{ITU-T_G.709}}, as described above.
For example, with reference to Figure 1 of {{!RFC7139}}, the
connectivity matrix entry or the local link connectivity entry
corresponding to the A-C underlay path, would report 2 Tributary
Slots (TS) with ODTU4.ts ODTU type.

### Resizable ODUflex {#Resize}

Resizable ODUflex is a special type of ODUflex that supports the
procedures defined in {{ITU-T_G.7044}} for hitless resizing of the
ODUflex nominal bit rate.

Two odu-type identities have been defined for ODUflex:

- The ODUflex identity, which is used with any type of non-resizable
ODUflex, as defined in Table 7-2 of {{ITU-T_G.709}}.

- The ODUflex-resizable identity, which is used only with resizable
ODUflex(GFP,n,k).

These two identities are used to identify whether an ODUflex(GFP,n,k)
LSP does or does not support the {{ITU-T_G.7044}} hitless resizing
procedures. They also identify whether an OTN link only supports the
set up of non-resizable ODUflex LSPs or also supports the set up of
resizable ODUflex(GFP,n,k) LSP but with different capabilities (e.g.,
a lower number of LSPs).

# YANG Tree for Layer1 Types {#tree}

~~~~ ascii-art
{::include-fold yang/trees/ietf-layer1-types.tree}
~~~~

# YANG Code for Layer1 Types {#code}

~~~~ yang
{::include yang/ietf-layer1-types.yang}
~~~~
{: sourcecode-markers="true" sourcecode-name="ietf-layer1-types@2024-02-22.yang"}

# Security Considerations {#Security}

The YANG module specified in this document defines a schema for data
that is designed to be accessed via network management protocols such
as NETCONF {{!RFC6241}} or RESTCONF {{!RFC8040}}. The lowest NETCONF layer
is the secure transport layer, and the mandatory-to-implement secure
transport is Secure Shell (SSH) {{!RFC6242}}. The lowest RESTCONF layer
is HTTPS, and the mandatory-to-implement secure transport is TLS
{{!RFC8446}}.

If using secure channels, such as SSH for NETCONF or TLS for
RESTCONF, an array of secure validation methods are availible. These
methods range from public key and password authentication to host
identity verification. It is strongly advised to not use options
that require no authentication. However, it is important to
acknowledge that not all authentication methods offer the same level
of security. For instance, password-based authentication is notably
susceptible to security threats such as phishing attacks and password
reuse.

The NETCONF access control model {{!RFC8341}} provides the means to
restrict access for particular NETCONF or RESTCONF users to a
preconfigured subset of all available NETCONF or RESTCONF protocol
operations and content.

The YANG module in this document defines layer 1 type definitions
(i.e., typedef, identity and grouping statements) in YANG data
modeling language to be imported and used by other layer 1
technology-specific modules. When imported and used, the resultant
schema will have data nodes that can be writable, or readable. The
access to such data nodes may be considered sensitive or vulnerable
in some network environments. Write operations (e.g., edit-config)
to these data nodes without proper protection can have a negative
effect on network operations.

The security considerations spelled out in the YANG 1.1 specification
{{!RFC7950}} apply for this document as well.

# IANA Considerations {#IANA}

It is proposed that IANA should assign new URIs from the "IETF XML
Registry" {{!RFC3688}} as follows:

~~~~
      URI: urn:ietf:params:xml:ns:yang:ietf-layer1-types
      Registrant Contact: The IESG
      XML: N/A; the requested URI is an XML namespace.
~~~~

This document registers following YANG modules in the YANG Module Names
registry {{!RFC7950}}.

~~~~
      name:         ietf-layer1-types
      namespace:    urn:ietf:params:xml:ns:yang:ietf-layer1-types
      prefix:       l1-types
      reference:    RFC XXXX
~~~~

> RFC Editor Note: Please replace XXXX with the number assigned to the
RFC once this draft becomes an RFC.


--- back

# Examples of OTN Label Ranges {#app1}

This appendix provides some examples of how the TPN and TS label
ranges described in Table 3 and Table 4 of {{!RFC7139}} can be
represented in YANG using the groupings defined in this document.

It also considers the OTUk links in addition to HO-ODUk links.

The JSON code examples provided in this appendix provides some
embedded comments following the conventions in Section 3.2 of
{{?I-D.ietf-ccamp-transport-nbi-app-statement}} and have been folded
using the tool in {{?RFC8792}}.

~~~~ json
{::include-fold yang/examples/odu-label-restrictions-examples.json}
~~~~

# Acknowledgments
{:numbered="false"}

The authors and the working group give their sincere thanks to Robert
Wilton for the YANG doctor review, to Tom Petch for his comments
during the model and document development, and to Deborah Brungard
for her support in addressing IESG review comments on the scope of
this document.
