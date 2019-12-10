---
description: Simplify Documentation Guide
lang: en
title: Simplify Migration
viewport: 'width=device-width, initial-scale=1, shrink-to-fit=no'
---

::: {#myTopnav .topnav}
[Home](#home){.active} [Overview](#overview) [Get Started](#get_started)
[Core Concepts](#core_concepts) [API Reference](#api_reference)
[Support](#support) [Best Practices](#best_practices)
[](javascript:void(0);){.icon}
:::

::: {.tooltip_templates}
[ ![info](images/info.png) ]{#PCIP2PE}

**Peripheral Component Interconnect Point to Point Encryption**\
A secure method of sending card data

[ ![info](images/info.png) ]{#PCIDSS}

**Payment Card Industry Data Security Standard**\
A set of security standards for handling card data
:::

\
\
\
\
\

Simplify Ingenico Developer Guide 2.02.024-025 {#simplify-ingenico-developer-guide-2.02.024-025 .h1}
==============================================

Ingenico Configuration and Troubleshooting Guide 2.02.024-025 {#ingenico-configuration-and-troubleshooting-guide-2.02.024-025 .h1}
=============================================================

Table of Contents {#table-of-contents .h2}
-----------------

::: {.container style="align-self:center"}

::: {.main}
Code Format Demo {#code-format-demo .h2}
----------------

["The story so far:\
In the beginning the Universe was created.\
This has made a lot of people very angry\
and been widely regarded as a bad move."]{.tooltip
title="Adams, Douglas, 1952-2001. The Hitchhiker's Guide to the Galaxy. New York :Harmony Books, 1980"
style="font-family: Roboto, sans-serif; color:#58585a; font-size:16px;"}\

The following code is taken from the CSS file for this page.

\

![](svgs/file_copy_white.svg) Copy

              
                 
          :root {
            --table-vertical-spacing: 30px;
            --table-horizontal-spacing: 30px;
          }
          /*Demo specific CSS - Do not copy to production*/

          .tooltip_templates { display: none; }

          @media (min-width: 0px) {/*Smaller than mobile*/
            body {
                    width: 80%  ;
            }

            .sidebar {
                    width: 80%  ;
            }
          }

          @media (min-width: 375px) {/*Mobile to landscape mobile*/
            body {
                    width: 80%  ;
            }

            .sidebar {
                    width: 80%  ;
            }
          }
          @media (min-width: 576px) {/*Small devices (landscape phones, 576px and up)*/
            body {
                    width: 75%%;
            }
            .sidebar {
                    width: 75%  ;
            }
                }
          @media (min-width: 768px) {/*Medium devices (tablets, 768px and up)*/
            
            body {
                    width: 75%;
            }
            .sidebar {
                    width: 75%;
            }
          }

          @media (min-width: 992px) {/*Large devices (desktops, 992px and up)*/
              body {
                      width: 70%;
              }
              .sidebar {
                      width: 70%;
              }
          }
          @media (min-width: 1200px) {
              body {
                      width: 70%;
              }

              .sidebar {
                      width: 70%;
              }

          }


          a:link {
            text-decoration: none;
            color:#58585a;
          }

          a:visited {
            text-decoration: none;
            font-color:#6008BA;
          }
      

        .h1 {
          font-size:36px;
          font-family: 'Roboto', sans-serif;
          color:#0a1c76;
          line-height: 54px;
        }

        .h2 {
          font-size:32px;
          font-family: 'Roboto Light', sans-serif;
          color:#0a1c76;
          line-height: 48px;
        }

        .h3 {
          font-size:28px;
          font-family: 'Roboto', sans-serif;
          color:#2C7BBC;
          line-height: 42px;
          line-weight:300;
        }

        .h4 {
          font-size:24px;
          font-family: 'Roboto', sans-serif;
          color:#58585a;
          line-height: 34px;
        }

        .h5 {
          font-size:20px;
          font-family: 'Roboto', sans-serif;
          color:#58585a;
          line-height: 34px;
          font-weight: 700;
        }
     
              
              

\

Simplify Overview {#simplify-overview .h1}
=================

Simplify^®^ is a semi-integrated, payment application that resides on
the payment device and ensures card holders and merchants experience a
secure credit or debit payment transaction, using both magstripe and EMV
chip enabled cards. Simplify securely encrypts card data (tapped,
inserted, swiped or manually entered) at the Point of Interaction, and
sends the encrypted transaction data to Elavon\'s payment gateway
(Fusebox) where a token for the payment card data is created.

Through the Simplify application programming interface (API), customers
in the Retail, Healthcare, Hospitality and Service industries can easily
isolate sensitive cardholder data from their Point-of-Sale (POS) or
Property Management System (PMS), thereby eliminating or reducing the
scope of PCI compliance audits. The Simplify solution offers the
flexibility of a variety of PIN Transaction Security (PTS)-approved
devices, from tethered to wireless, along with communication and
connectivity modes ranging from RS232 through WiFi. This solution is
also available as a full P2PE solution.

::: {.row}
<div>

Integration Timeline {#integration-timeline .h2}
--------------------

+-----------------------+-----------------------+-----------------------+
| ![clipboard](/svgs/cl |                       | **Project Kickoff**\  |
| ipboard.svg){.circle} |                       |                       |
|                       |                       | -   Choose your       |
|                       |                       |     integration       |
|                       |                       |     method            |
|                       |                       | -   Define your scope |
|                       |                       | -   Read the          |
|                       |                       |     documentation     |
|                       |                       | -   Create test       |
|                       |                       |     account           |
+=======================+=======================+=======================+
| ![gear](/svgs/gear.sv |                       | **Development**\      |
| g){.circle}           |                       |                       |
|                       |                       | -   Write and test    |
|                       |                       |     code              |
+-----------------------+-----------------------+-----------------------+
| ![check](/svgs/check. |                       | **Integration         |
| svg){.circle}         |                       | Testing**\            |
|                       |                       |                       |
|                       |                       | -   Test all          |
|                       |                       |     transaction types |
|                       |                       |     in demo           |
|                       |                       |     environment       |
|                       |                       | -   Work with         |
|                       |                       |     Solution          |
|                       |                       |     Engineers on any  |
|                       |                       |     problems          |
|                       |                       | -   Complete          |
|                       |                       |     certification     |
|                       |                       |     test cases        |
+-----------------------+-----------------------+-----------------------+
| ![check](/svgs/headse |                       | **Post Implementation |
| t.svg){.circle}       |                       | Support**\            |
|                       |                       |                       |
|                       |                       | -   Support website   |
|                       |                       |     after launch.     |
+-----------------------+-----------------------+-----------------------+
| ![check](/svgs/clock. |                       | **Total Estimated     |
| svg){.circle}         |                       | Time**\               |
|                       |                       |                       |
|                       |                       | -   8-12 weeks        |
+-----------------------+-----------------------+-----------------------+

::: {.col .s4}
Learn the API {#learn-the-api .h2}
-------------

Learn the API using the following guides:

-   Simplify Ingenico Developer Guide 2.02.024-025 (you\'re reading it!)
-   Simplify Telium Developer Guide 2.02.021
-   Simplify VeriFone Developer Guide 2.19
-   Simplify VeriFone Developer Guide 2.18

Learn PIN Pad Procedures {#learn-pin-pad-procedures .h2}
------------------------

Learn PIN pad procedures using the following guides:

-   [Simplify Ingenico Download Configuration Troubleshooting Guide
    2.02.024-025.](#support)
-   \"\>Simplify Verifone Download Configuration Guide 2.19
:::

<div>

Communications {#communications .h2}
--------------

Communication Modes between PIN Pad and POS:

-   RS232 (Serial)
-   PPP over RS232
-   TCP/IP
    -   Bluetooth
    -   WiFi
    -   Ethernet
-   USB emulating RS232

For more information see **Message and Communications Protocols** in the
Simplify Developer Guide.

</div>

::: {.col .s12}
<div>

Supported Devices {#supported-devices .h2}
-----------------

</div>

::: {.body-text}
**Version 24 for Ingenico**\
We\'ve released version 24 for all Ingenico products. This version
supports Telium terminals only:

-   iPP320
-   iPP350
-   iSC250
-   iSC480
-   iSMP4
-   iWL2xx
-   Link 2500
-   Move 5000
-   Lane 3000
-   Lane 5000
-   Lane 7000
-   MX915
-   MX925
:::
:::

Additional Resources {#additional-resources .h2}
--------------------

Get more information and resources to optimize your experience with
Simplify.

</div>

::: {.body-text}
**Partner News** : Elavon\'s newsletter for Integration Partners.
:::

::: {.body-text}
**Payments Core 365** : A payments validation service available for
Elavon products.

### What\'s New for Ingenico Products? {#whats-new-for-ingenico-products .h3}

<div>

-   **TLS 1.2** We\'ve added an instructional guide for implementing TLS
    1.2.
-   **Test Cards** We\'ve added a new section covering how to work with
    test cards for your Simplify integrated Point-of-Sale devices.
-   **New for Ingenico in Version 25** Version 25 added new Ingenico
    support for:
    -   Tetra devices
    -   Bluetooth communications
-   **Version 24 for Ingenico** We\'ve released version 24 for all
    supported Ingenico products. This version supports the following
    features:
    -   Simplify now supports Wi-Fi
    -   Signature Request Message supports new tag (002) allowing more
        flexible signature screen layout.
    -   Initiate Ingestate Message allows POS to set IngEstate
        identifier (TMSID).
    -   Scrolling Receipt Message supports up to five lines of text plus
        a total line in a single request.
    -   Print Request Message from POS (NEW) supports Simplify printing
        on non-Pay\@Table systems.
    -   Fusebox supports processing Returns from Simplify as EMV
        transactions
    -   Simplify supports Contactless EMV.
    -   Stand-In response supports return of EMV tags (configurable).
    -   Simplify supports additional tags (011, 012, 071, 072).
    -   Get Check Info Response supports text field.
    -   Simplify supports Auto signature (no Signature Request message
        required).
    -   Simplify supports Quick Chip to speed EMV processing. (Includes
        optional Quick Chip message to enable tendering ahead of
        transaction total.)
    -   Simplify supports the display of Tip amounts for configured or
        POS-controlled Tip percentages.
    -   Added Wi-Fi Setup.
-   **Developer Guide Changes**

    We\'ve made several edits to our developer guide for Ingenico
    Version 24. The main changes are:

    -   **General Guidelines** - Guidelines have been added. Some
        guidelines have been placed at the start of [Message
        Details](#core_concepts).
    -   **[Message Details](#core_concepts)** - Reorganized sequence to
        group related messages. Moved some notes to a Guidelines section
        at the start of the chapter. Made other changes for clarity.
    -   **EMV** - Added list of EMV tags. Modified description of Return
        transaction using chip card to say EMV supported, consult Elavon
        for configuration.
    -   **Simplify - Generated Response Messages** - Defined processing
        required for response codes that produce Simplify-generated
        response messages.
    -   **Appendix F** - Renamed to Simplify-Controlled Fields. Made old
        Appendix F on field 11 a subsection, and rewrote for clarity.
        Added subsections on API fields 5001, 5070, 5071, 5104.

</div>

Simplify Introduction {#simplify-introduction .h1}
=====================

Simplify is Elavon's PIN Pad-based application designed to process
electronic payment transactions received from a Point of Sale (POS) or a
Property Management System (PMS).

This document is a developer guide for customers interfacing their POS /
PMS process to Simplify. It applies specifically to implementations that
run Simplify on Ingenico PIN Pads using Voltage or On-Guard encryption,
and send transactions to Elavon's Fusebox gateway.

The Developer Guide is distributed with the application and available to
the customer on the Elavon website. It is reviewed for every application
update and change to [PCI P2PE]{.tooltip tooltip-content="#PCIP2PE"
style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}
requirements (at least annually) and updated as required.

See [Usage](/#00079) for conventions used in this document.

See [Addendum](/#00081) for material added since the initial Developer
Portal release for this version of Simplify.

Supported Hardware {#00082 .h2}
------------------

Supported Telium Devices: - ipp320 - iPP350 - iSC250 - iCS480 - iSMP4 -
iWL2xx

New for Version 25: - Tetra Lane 3000 - Tetra Lane 5000 - Tetra Lane
7000 - Tetra Link 2500 - Tetra Move 5000

::: {#best_practices}
:::

\

General Guidelines {#00083 .h2}
------------------

POS development for Simplify should be based on the following set of
principles:

1.  [PCI DSS]{.tooltip tooltip-content="#PCIDSS"
    style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}
    Compliance: The customer is responsible for securely deleting the
    encrypted account data and making it unrecoverable after
    authorization using a method that supports [PCI DSS]{.tooltip
    tooltip-content="#PCIDSS"
    style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}
    secure delete standards (*[PCI DSS]{.tooltip
    tooltip-content="#PCIDSS"
    style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}
    3.0 Requirement 3.2*).

2.  The POS process should disregard any unexpected message from
    Simplify. This can be done by:

    a\) Discarding messages that do not correspond with the POS state.

    b\) Comparing the Transaction ID / Reference Number (field 7) in the
    request and response. If the response doesn't match the request, the
    message should be discarded.

3.  If multiple POS workstations can be associated with a single PIN
    Pad, Simplify assumes that the POS process ensures there is only one
    outstanding transaction per PIN Pad. (This situation can occur under
    TCP/IP.)

4.  Simplify can return encrypted account data to allow Stand-in
    processing by the POS. See [Stand-in Processing](#0003) for more
    information.

5.  For support purposes, Elavon strongly recommends that the POS logs
    all messages received from and sent to Simplify.

6.  API fields in messages sent to the POS will not necessarily appear
    in order by field number. E.g. the following sequence of fields is
    possible:

      API Field \#, Value              Description
      -------------------------------- --------------------
      0001,36                          Transaction Type
      5001,010003888                   Non-Financial Data
      0011,14123010000?V102.18B01803   User Data

7.  For API fields that are defined as variable length, the POS must be
    able to handle data of varying lengths.

8.  Elavon uses IngEstate for terminal maintenance and updates. Any
    issue with IngEstate connectivity will require shipping back the
    terminal for updates. Elavon recommends testing the connection to
    IngEstate during pilot.

9.  Elavon uses Inquiry and Voids to recover from communication issues
    on Financial Messages. Please pay close attention when implementing
    Inquiry and Void logic.

10. Fields 13 (date) and 14 (time) are required in all financial
    requests.

11. To protect against EMV cards being left in the Simplify device,
    Simplify will not accept any message from the POS until the card is
    removed. An error message will be returned indicating that the card
    is still inserted.

12. If no response is received for a financial request, or if you need
    to start over for any reason, the POS should send a Cancel before
    sending another financial request.

Message and Communications Protocols {#00084 .h2}
------------------------------------

A message using the Elavon Gateway API format consists of a list of
fields, each assigned a field number. The field number (which can be
0-filled to 4 characters or just the number up to 4 characters) is
followed by a comma which is followed by the field value. Each line is
terminated with a \<CR\>\<LF\>. Alternatively each line might be
terminated by a UNIX \<LF\>. The message is terminated with an \<EOT\>.

Control Characters are defined as follows:

\<CR\> = (0x0D) 1 byte, hex D

\<LF\> = (0x0A) 1 byte, hex A

\<EOT\> = (0x04) 1 byte, hex 4

::: {.notices .note}
::: {.body-text}
**Note:** Sample messages shown in this document do not show the control
characters.
:::
:::

The communications protocol between the POS process and Simplify is
TCP/IP, or RS-232 (Serial), or PPP with TCP/IP over RS-232.

TCP/IP

TCP/IP communications between the POS and Simplify can be by wired
ethernet, Wifi or Bluetooth transport to the base. The availability of
these communication methods is device-dependent.

In most systems, Simplify will act as the TCP/IP server. The POS process
will act as a TCP/IP client and initiate the connection to Simplify.

**Exception:** For Pay\@Table systems, the POS process will act as the
TCP/IP server. Simplify will act as a TCP/IP client and initiate the
connection to the POS.

Simplify-POS messaging can use plain TCP/IP or TCP/IP with TLS 1.2.
Depending on security configuration, a certificate may be needed if TLS
is used.

[Appendix B](#00069) describes the Simplify RS-232 communication
protocol.

Simplify RS-232 communication could optionally be over USB emulating
RS-232.

PPP under RS-232 (Serial)

Simplify supports PPP (Point to Point Protocol) communications over
RS-232. Using this protocol for the transport layer allows customers to
communicate via TCP/IP over a RS-232 physical link.

The Simplify PIN Pad will be the PPP client and communicate with a PPP
server on the customer network. Elavon will set the PIN Pad to receive
the following data from the PPP server: (1) A host IP address to use for
TCP/IP communications between the PIN Pad and Fusebox. (2) An IngEstate
server address to use for TCP/IP communications between the PIN Pad and
IngEstate.

There will be three TCP/IP sockets:

-   One socket is from the POS to Simplify. The POS will be the socket
    client and Simplify will be the socket server.

-   Another socket is from Simplify to Fusebox. FuseBox will be the
    socket server and Simplify will be the socket client. This socket is
    non-persistent (as usual) and is secured by TLS 1.2.

-   Another socket is from Simplify to the IngEstate server. IngEstate
    will be the socket server and Simplify will be the socket client.

Apart from interaction with the PPP server, Simplify TCP/IP
communications under PPP will follow the usual Simplify TCP/IP rules.

Versioning {#00085 .h2}
----------

The Simplify versioning scheme (from 2.02.021 on) includes a two-part
prefix (S-PP below) indicating: (1) whether Simplify is operating as
part of a [PCI P2PE]{.tooltip tooltip-content="#PCIP2PE"
style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}-validated
solution, and (2) the encryption type. The prefix for a validated
solution using On-Guard will be V-OG. Versions with any other prefix
will be non-validated.

The Simplify versioning implemented will be as follows:

  -----------------------------------------------------------------------------------------------------------------------------------------------
  Element                 Data Type               Description
  ----------------------- ----------------------- -----------------------------------------------------------------------------------------------
  S                       alphanumeric            Elavon enterprise implementation type ([PCI P2PE]{.tooltip tooltip-content="#PCIP2PE"
                                                  style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}-validated
                                                  solution indicator)V = validated\
                                                  Missing or any other value = non-validated

  PP                      alphanumeric            Encryption type used by application:\
                                                  OG = On-Guard\
                                                  G2 = Voltage

  X                       numeric                 Major Version\
                                                  Example: X was incremented to 2 when EMV support was added.

  YY                      numeric                 Minor Version. Changes that affect architecture or security.

  ABBCC                   numeric                 Build release\
                                                  A: 0-4: Only used for On-Guard implementations.\
                                                  5-9: Only used for Voltage implementations.\
                                                  BB: Feature changes that do not affect architecture or security.\
                                                  CC: Sequential build number for IngEstate control. No impact on functionality. For bug fixes or
                                                  adjustments.
  -----------------------------------------------------------------------------------------------------------------------------------------------

The Simplify version number will not affect the EMV level. A separate
internal EMV version will be used for purposes of EMV certification:

Any time there is a change in the EMV interface or functionality, the
EMV version will be updated.

The Simplify version number will be displayed during boot up and on an
Informational Screen that can be briefly displayed by pressing 0 when
the terminal is in the closed state. (To lengthen the display, press the
+ or -- key.) If the second part of the prefix of the version number is
OG (indicating On-Guard encryption), this will serve as an indicator
that SRED is activated in the terminal.

Current version numbers for Simplify and supporting software are as
follows:

Simplify Version 24

  Software Component            Version
  ----------------------------- -----------------
  Simplify OnGuard version      2.02.024xx-OG
  Simplify Voltage version      2.02.524xx-G2
  Simplify EMV Cert version     2.23
  Easy Path to C'Less version   5.14.0.02
  Easy Path to EMV version      22.14.2.01
  Telium SDK version            11.16.7.Patch G
  OnGuard version               1.6.0.00

Simplify Version 25

  Software Component                     Version
  -------------------------------------- ------------------
  Simplify OnGuard version               2.02.025xx-OG
  Simplify Voltage version               2.02.525xx-G2
  Simplify EMV Cert version              2.25
  Easy Path to C'Less version (Telium)   5.14.0.02
  Easy Path to EMV version (Telium)      22.14.2.01
  SDK version (Telium)                   11.16.07.Patch G
  Easy Path to C'Less version (Tetra)    7.6.7.00
  Easy Path to EMV version (Tetra)       30.12.3.01
  SDK version (Tetra)                    11.16.05.Patch M
  OnGuard version                        1.6.0.00

\

Message Details {#message-details .h1}
===============

This chapter provides details on message types sent between Simplify and
the POS. These messages follow the Elavon Gateway API as specified in
the **Fusebox Integration Guide**. The chapter covers both Financial
Messages and [Non-Financial Messages](#00021) (Tran Type 36). For
additional information on Financial Messages, see the Fusebox industry
guides. Message samples in this chapter do not include EMV fields;
please refer to the EMV chapter for more information.

Guidelines for Handling Financial Messages {#00006 .h2}
------------------------------------------

Messages built for Simplify and the handling of messages received from
Simplify should be based on the following set of principles:

1.  If account data is sent in Field 3 of the POS request, the Tender
    Type is required in Field 115 (Transaction Qualifier).

2.  If the POS wants Simplify to prompt for Manual Entry, send 'K' in
    Field 3.

3.  If the data in Field 2 (Amount) or any other amount field does not
    include a decimal point, the decimal point will be assumed. (E.g., a
    value of 2000 in this field will be read as 20.00.)

4.  If a transaction refers back to a previous transaction (e.g. Void,
    Prior Auth), the request for the later transaction follows the
    **Fusebox Integration Guide**, including the rules for POS data code
    (API field 47).

5.  Fields 13 (date) and 14 (time) are required in all financial
    requests.

6.  Elavon recommends not padding Field 7 (Transaction ID / Reference
    Number) with leading zeros. Elavon recommends presenting this field
    in the same manner in all messages.

7.  The messages in this document are basic samples. The POS should be
    able to handle any additional API fields in the response as defined
    in the **Fusebox Integration Guide** under "API Reference".

8.  If a [Void Request](#void_request) needs to be re-sent, it should be
    sent without modification until a Host Response is received.

9.  If a voice auth transaction is sent to Simplify without an account
    number or a token in field 3, Simplify will prompt for account data.
    The operator verifies that the account data for which voice auth was
    obtained matches that entered at the PIN Pad.

10. Elavon recommends sending API 5071 in all financial requests, using
    the value that reflects the actual transaction environment. See
    under [Simplify-Controlled Field Definitions](#00073).

11. The value in field 0007 (Transaction ID / Reference ID) is
    incremented by the POS for each new transaction.  

\

Sale Message (Tran Type 02) {#00007 .h2}
---------------------------

Simplify supports a Sale message from the POS process.

Request

The following table shows an example of a Sale Request message (from the
POS to Simplify).

  API Field \#, Value   Description
  --------------------- -------------------------------------------------------------------------------------------------------
  0001,02               Transaction Type
  0002,1.00             Transaction Amount
  0007,55               Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           Transaction Date (current date)-- MMDDYY
  0014,105007           Transaction Time (current time) -- HHMMSS
  0017,0.00             Cash Back Amount
  0109,Term02           Terminal ID (provided by Elavon)
  0110,205              Cashier ID
  0201,0.00             Tip Amount
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](#00073).
  8002,ONGUARD          Location Name (provided by Elavon)
  8006,TSTLA3           Chain Code (provided by Elavon)

### Response {#response .h3}

The table below is an example of a Sale Response message (from Simplify
to the POS).

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,02                             Transaction Type

  0002,1.00                           Transaction Amount

  0003,ID:4476082153699999            Account Token (returned by Fusebox)

  0004,0119                           Expiration Date (MMYY)

  0006,419039                         Authorization Code (returned by
                                      Fusebox)

  0007,55                             Transaction ID / Reference Number

  0009,001                            Fusebox -- Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction Date (current date) --
                                      MMDDYY

  0014,105007                         Transaction Time (current time) --
                                      HHMMSS

  0017,0.00                           Cash Back Amount

  0030,1                              Fusebox -- Online Indicator

  0032,022519                         Fusebox -- Authorization
                                      Transaction Date

  0033,135016                         Fusebox -- Authorization
                                      Transaction Time

  0035,5245                           Validation Code

  0036,018031513501628                Host Transaction Identifier

  0037,0                              Fusebox - Authorizer

  0043,117595                         System Trace Audit Number

  0047,M;1;1;1;0;1;2;5;4;1;3;C;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless; 5 =
                                      swiped)

  0054,90                             POS Entry Mode

  0062,154                            Service Code

  0109,TERM02                         Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,400                            Fusebox -- Processor ID

  0115,010                            Transaction Qualifier (010 =
                                      credit; 030 = debit)

  0125,315175016                      Retrieval Reference Number (may
                                      need to appear on receipt)

  0126,2                              Track Indicator (may need to appear
                                      on receipt)

  0129,0                              Fusebox -- Compliance Data

  0130,1.00                           Authorized Amount

  0140,USD                            Merchant Currency

  0201,0.00                           Tip Amount

  0651,00003@;010011759503151;\       Reversal data (for reversal, if
  750160000047170500000000000;\       needed)
  419039807417117595                  

  0738,106781MMCC539137 Y 0225        Recurring Compliance Data

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1002,CERTIFICATION-VISA/ELAVON      Cardholder Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,\*\*\*\*\*\*\*\*\*\*\*\*9999   Masked Account Number (for printing
                                      on receipt)

  1009,AA                             Host Response Code

  1010,COMPLETE                       Gateway Response Message

  1012,0039                           Gateway Batch Number

  1200,0000AA                         Issuer Network Information

  1339,00                             EMV Response Code

  1359,4                              EMV CVM Indicator

  4747,040311                         Third Party Interface POS Data Code

  5002,80649419                       Device Serial Number

  5004,OG                             Encryption Provider ID

  5010,EMVDC0838                      EMV kernel version

  5070,Merchant: Demo;Simplify:\      Simplify Information. See
  V-OG-2.02.02124;PARM: 2.21.1;\      [Simplify-Controlled Field
  TENDERDEF: 2.21.1;\                 Definitions](#00073).
  EMVPARM: EMVPARM-E4-1               

  5071,xxx...                         Defines whether card and cardholder
                                      are present. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  5104,xxx...                         Tip Settings. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  7007,1118074642168320               Transaction Link Identifier (unique
                                      identifier to link transactions)

  8002,ONGUARD                        Location Name (provided by Elavon)

  8006,TSTLA3                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

Auth Only Message (Tran Type 01) {#0002 .h2}
--------------------------------

Simplify supports an Auth Only message from the POS process.

### Request {#request .h3}

The following table shows an example of an Auth Only Request message
from the POS to Simplify.

\

  API Field \#, Value   Description
  --------------------- -------------------------------------------------------------------------------------------------------
  0001,01               Transaction Type
  0002,1.00             Transaction Amount
  0007,57               Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           Transaction Date (current date)-- MMDDYY
  0014,105120           Transaction Time (current time) -- HHMMSS
  0109,TERM02           Terminal ID (provided by Elavon)
  0110,205              Cashier ID
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](#00073).
  8002,ONGUARD          Location Name (provided by Elavon)
  8006,TSTLA3           Chain Code (provided by Elavon)

\
\

Prior Auth Sale Message (Tran Type 07) {#00008 .h2}
--------------------------------------

Simplify supports a Prior-Auth Sale (Completion) message from the POS
process.

The Prior-Auth Sale transaction type is designed to record a previously
authorized transaction for funding. It is also called a "post-authorized
sale" or a "completion" transaction, and works in conjunction with an
Auth Only transaction.

\

API Field \#
:::
:::
:::
:::

Description

\

0003

Account Data (token)

0004\

Expiration Date

0006

Authorization Code

0007

Transaction ID / Reference Number

### Request {#request-1 .h3}

An example of a Prior-Auth Sale Request message (from the POS to
Simplify) is:

\

API Field \#, Value

Description

0001,07

Transaction Type.

0002,8.00

Transaction Amount. Should be the final amount to be processed

0003,ID:1111748353147271

Account Data. Must match Auth Only response.

0004,1208

Expiration Date -- MMYY. Must match Auth Only response (if present).

0006,CVI014

Authorization Code. Must match Auth Only response.

0007,1025

Transaction ID / Reference Number. Must match Auth Only response

0011,xxx..

User Data. See [Simplify-Controlled Field Definitions](#00073).

0013,022519

Transaction Date (current date) -- MMDDYY

0014,143005

Transaction Time (current time) -- HHMMSS

0109,TERM1

Terminal ID (provided by Elavon)

0110,205

Cashier ID

0115,010

Transaction Qualifier (010 = credit; 030 = debit)

5071,xxx...

Defines whether card and cardholder are present. See
[Simplify-Controlled Field Definitions](#00073).

5104,xxx...

Tip Settings. See [Simplify-Controlled Field Definitions](#00073).

8002,RETL01

Location Name (provided by Elavon)

8006,TSTLAR

Chain Code (provided by Elavon)

\
\

### Response {#response-1 .h3}

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,07                             Transaction Type

  0002,8.00                           Transaction Amount

  0003,ID:1111748353147271            Account Token (returned by Fusebox)

  0004,1208                           Expiration Date -- MMYY

  0006,CVI014                         Authorization Code (returned by
                                      Fusebox)

  0007,1025                           Transaction ID / Reference Number

  0009,0025                           Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction Date (current date) --
                                      MMDDYY

  0014,115745                         Transaction Time (current time) --
                                      HHMMSS

  0030,1                              Online Indicator

  0033,115754                         Fusebox -- Authorization
                                      Transaction Time

  0035,0DF9                           Validation Code

  0036,111175957465103                Host Transaction Identifier

  0037,0                              Authorizer

  0043,223946                         System Trace Audit Number

  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless; 5 =
                                      swiped)

  0054,01                             POS Entry Mode

  0109,TERM1                          Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,189                            Processor ID

  0115,010                            Transaction Qualifier (010 =
                                      credit; 030 = debit)

  0125,0624155745                     Retrieval Reference Number (may
                                      need to appear on receipt)

  0126,2                              Track Indicator (may need to appear
                                      on receipt)

  0128,6.00                           Original Authorization Amount

  0129,1                              Compliance Data

  0130,8.00                           Total Authorized Amount

  0131,00                             CPS Total Incremental Auths sent

  0132,0                              Authorization Reversal Sent

  0140,USD                            Merchant Currency

  0651,00003@;\                       Reversal data (for reversal, if
  175016000004717050000000\           needed)
  0000419039807417117595              

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1003,0000                           Gateway Response Code

  1004,ACKNOWLEDGED                   Host Response Message

  1008,466206\*\*\*\*\*\*0005         Masked Account Number (for printing
                                      on receipt)

  1010,COMPLETE                       Gateway Response Message

  1012,1832                           Gateway Batch Number

  1200,0000AA                         Issuer Network Information

  1359,4                              EMV CVM Indicator

  5002,80378002                       Device Serial Number

  5004,OG                             Encryption Provider ID

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  5071,xxx...                         Defines whether card and cardholder
                                      are present. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  5104,xxx...                         Tip Settings. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  7007,1111175588200494               Transaction Link Identifier (unique
                                      identifier to link transactions)

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

\

Incremental Authorization Message (Tran Type 75) {#00009 .h2}
------------------------------------------------

Simplify supports an Incremental Authorization message from the POS
process if tokenization is implemented.

The following table shows a sample of fields in the Incremental
Authorization message that may need to match fields in the original
transaction. See the **Fusebox Integration Guide** and the **Lodging
Integration Guide** for more information on this Transaction Type.

\

  -----------------------------------------------------------------------
  API Field \#                        Description
  ----------------------------------- -----------------------------------
  0003                                Account Data (token)

  0004\                               Expiration Date

  0006                                Authorization Code

  0007                                Transaction ID / Reference Number
  -----------------------------------------------------------------------

### Request {#request-2 .h3}

An example of a Prior-Auth Sale Request message (from the POS to
Simplify) is:

\

  API Field \#, Value        Description
  -------------------------- -------------------------------------------------------------------------------------------------------
  0001,07                    Transaction Type.
  0002,8.00                  Transaction Amount. Should be the final amount to be processed
  0003,ID:1111748353147271   Account Data. Must match Auth Only response.
  0004,1208                  Expiration Date -- MMYY. Must match Auth Only response (if present).
  0006,CVI014                Authorization Code. Must match Auth Only response.
  0007,1025                  Transaction ID / Reference Number. Must match Auth Only response
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143005                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID (provided by Elavon)
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit)
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  5104,xxx...                Tip Settings. See [Simplify-Controlled Field Definitions](#00073).
  8002,RETL01                Location Name (provided by Elavon)
  8006,TSTLAR                Chain Code (provided by Elavon)

Full Authorization Reversal Message (Tran Type 61) {#00010 .h2}
--------------------------------------------------

Simplify supports a Full Authorization Reversal message from the POS if
tokenization is implemented.

The following table shows a sample of fields in the Full Authorization
Reversal message that may need to match fields in the original
transaction. See the **Fusebox Integration Guide** for more information
on this transaction type.

\

  -----------------------------------------------------------------------
  API Field \#                        Description
  ----------------------------------- -----------------------------------
  0003                                Account Data (token)

  0004\                               Expiration Date

  0006                                Authorization Code

  0007                                Transaction ID / Reference Number
  -----------------------------------------------------------------------

Request

An example of a Full Authorization Reversal message (from the POS to
Simplify) is:

\

  API Field \#, Value        Description
  -------------------------- -------------------------------------------------------------------------------------------------------
  0001,61                    Transaction Type
  0002,1.00                  Transaction Amount
  0003,ID:1111748353147271   Account Data. Must match Auth Only response.
  0004,1208                  Expiration Date -- MMYY. Must match Auth Only response (if present).
  0006,106845                Authorization Code. Must match Auth Only response.
  0007,140                   Transaction ID / Reference Number. Must match Auth Only response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143005                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID (provided by Elavon)
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit)
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  8002,RETL01                Location Name (provided by Elavon)
  8006,TSTLAR                Chain Code (provided by Elavon)

### Response {#response-2 .h3}

An example of a Full Authorization Reversal Response message (from
Simplify to the POS) is:

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,61                             Transaction Type

  0002,1.00                           Transaction Amount

  0003,ID:1120106195107475            Account Token (returned by Fusebox)

  0004,1215                           Expiration Date -- MMYY

  0006,CVI790                         Authorization Code (returned by
                                      Fusebox)

  0007,140                            Transaction ID / Reference Number

  0009,0104                           Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction Date (current date) --
                                      MMDDYY

  0014,143005                         Transaction Time (current time) --
                                      HHMMSS

  0030,1                              Online Indicator

  0032,022519                         Authorization Transaction Date

  0033,161934                         Authorization Transaction Time

  0035,E2F9                           Validation Code

  0036,112010967961779                Host Transaction Identifier

  0037,0                              Authorizer

  0043,118410                         System Trace Audit Number

  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless , 5 =
                                      swiped)

  0054,01                             POS Entry Mode

  0109,TERM1                          Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,189                            Processor ID

  0115,010                            Transaction Qualifier(010 = credit;
                                      030 = debit)

  0125,0110224915                     Retrieval Reference Number (may
                                      need to appear on receipt)

  0126,0                              Track Indicator (may need to appear
                                      on receipt)

  0128,16.00                          Original Authorization Amount

  0129,0                              Compliance Data

  0130,32.00                          Total Authorized Amount

  0131,01                             CPS Total Incremental Auths sent

  0132,0                              Authorization Reversal Sent

  0140,USD                            Merchant Currency

  0651,00003@;0100117595031\          Reversal data (for reversal, if
  5175016000004717050000000\          needed)
  0000419039807417117595              

  0738,106781MMCC539137 Y 0225        Recurring Compliance Data

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,400555\*\*\*\*\*\*4460         Masked Account Number (for printing
                                      on receipt)

  1009,AA                             Host Response Code

  1010,COMPLETE                       Gateway Response Message

  1012,1832                           Gateway Batch Number

  1200,0000AA                         Issuer Network Information

  1339,00                             EMV Response Code

  1359,4                              EMV CVM Indicator

  4747,020111                         Third Party Interface POS Data Code

  5002,80649419                       Device Serial Number

  5004,G2                             Encryption Provider ID

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  5071,xxx...                         Defines whether card and cardholder
                                      are present. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  7007,1112010821551364               Transaction Link Identifier. A
                                      unique identifier to link
                                      transactions

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

\

Partial Authorization Reversal Message (Tran Type 76) {#00011 .h2}
-----------------------------------------------------

Simplify supports a Partial Authorization Reversal message from the POS.

Important: Not all processors support this transaction type. It is
important to consult Elavon before implementing this transaction type.

  -----------------------------------------------------------------------
  API Field \#                        Description
  ----------------------------------- -----------------------------------
  0003                                Account Data (token)

  0004\                               Expiration Date

  0006                                Authorization Code

  0007                                Transaction ID / Reference Number
  -----------------------------------------------------------------------

### Request {#request-3 .h3}

An example of a Partial Authorization Reversal Request message (from the
POS to Simplify) is:

\

  API Field \#, Value        Description
  -------------------------- -------------------------------------------------------------------------------------------------------
  0001,76                    Transaction Type.
  0002,1.00                  Transaction Amount
  0003,ID:1120106195107475   Account Data. Must match Auth Only response.
  0004,1215                  Expiration Date -- MMYY. Must match Auth Only response (if present).
  0006,106844                Authorization Code. Must match Auth Only response.
  0007,140                   Transaction ID / Reference Number. Must match Auth Only response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143008                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID (provided by Elavon)
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit)
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  8002,RETL01                Location Name (provided by Elavon)
  8006,TSTLAR                Chain Code (provided by Elavon)

### Response {#response-3 .h3}

An example of a Partial Authorization Reversal Response message (from
Simplify to the POS) is:

\

  API Field \#, Value                Description
  ---------------------------------- -------------------------------------------------------------------------------------------------------
  0001,76                            Transaction Type
  0002,1.00                          Transaction Amount
  0003,ID:1120106195107475           Account Token (returned by Fusebox)
  0004,1215                          Expiration Date -- MMYY
  0006,CVI790                        Authorization Code (returned by Fusebox)
  0007,140                           Transaction ID / Reference Number
  0009,0104                          Host Batch number
  0011,xxx..                         User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                        Transaction Date (current date) -- MMDDYY
  0014,143005                        Transaction Time (current time) -- HHMMSS
  0030,1                             Online Indicator
  0032,022519                        Authorization Transaction Date
  0033,161934                        Authorization Transaction Time
  0035,E2F9                          Validation Code
  0036,112010967961779               Host Transaction Identifier
  0037,0                             Authorizer
  0043,118410                        System Trace Audit Number
  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4   POS Data Code
  0052,5                             Transponder / Proximity Indicator (0 = contact; 2 = contactless, 5 = swiped)
  0054,90                            POS Entry Mode
  0062,154                           Service Code
  0109,TERM1                         Terminal ID (provided by Elavon)
  0110,205                           Cashier ID
  0112,189                           Processor ID
  0115,010                           Transaction Qualifier (010 = credit; 030 = debit)
  0125,0110224915                    Retrieval Reference Number (may need to appear on receipt)
  0126,0                             Track Indicator (may need to appear on receipt)
  0128,16.00                         Original Authorization Amount
  0129,0                             Fusebox - Compliance Data
  0130,32.00                         Total Authorized Amount
  0131,01                            CPS Total Incremental Auths sent
  0132,0                             Authorization Reversal Sent
  0140,USD                           Merchant Currency
  0651,09901@                        Reversal data (for reversal, if needed)
  0738, MMTI539215 02255             Recurring Compliance Data
  1000,VI                            Card Type
  1001,VISA                          Card Name
  1003,0000                          Gateway Response Code
  1004,APPROVAL                      Host Response Message
  1005,0010600008014593613999        Merchant Number
  1008,400555\*\*\*\*\*\*4460        Masked Account Number (for printing on receipt)
  1009,AA                            Host Response Code
  1010,COMPLETE                      Gateway Response Message
  1012,1832                          Gateway Batch Number
  1200,0000AA                        Issuer Network Information
  1339,00                            EMV Response Code
  1359,4                             EMV CVM Indicator
  4747,040311                        Third Party Interface POS Data Code
  5002,80649419                      Device Serial Number
  5004,G2                            Encryption Provider ID
  5010,EMVDC0838                     EMV kernel version
  5070,xxx...                        Simplify Information. See [Simplify-Controlled Field Definitions](#00073).
  5071,xxx...                        Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  7007,1112010821551364              Transaction Link Identifier (unique identifier to link transactions)
  8002,RETL01                        Location Name (provided by Elavon)
  8006,TSTLAR                        Chain Code (provided by Elavon)

\

Return Message (Tran Type 09) {#00013 .h2}
-----------------------------

Simplify supports a Return message from the POS.

### Request {#request-4 .h3}

An example of a Return Request message (from the POS to Simplify) is:

\

  API Field \#, Value   Description
  --------------------- -------------------------------------------------------------------------------------------------------
  0001,09               Transaction Type.
  0002,125.98           Transaction Amount
  0007,1025             Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,143005           Transaction Time (current time) -- HHMMSS
  0109,TERM1            Terminal ID (provided by Elavon)
  0110,205              Cashier ID
  0115,010              Transaction Qualifier (010 = credit; 030 = debit)
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  8002,RETL01           Location Name (provided by Elavon)
  8006,TSTLAR           Chain Code (provided by Elavon)

### Response {#response-4 .h3}

An example of an Incremental Authorization Response message (from
Simplify to the POS) is:

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,01                             Tran Type. Note that the Tran Type
                                      in the response is a 01 (Auth Only
                                      response) -- not a 75.

  0002,19.00                          Transaction Amount

  0003,ID:1120064425266606            Account Token (returned by Fusebox)

  0004,1208                           Expiration Date -- MMYY

  0006,CVI130                         Authorization Code (returned by
                                      Fusebox)

  0007,1123                           Transaction ID / Reference Number

  0009,0102                           Host Batch Number

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction Date (current date) --
                                      MMDDYY

  0014,143005                         Transaction Time (current time) --
                                      HHMMSS

  0030,1                              Online Indicator

  0032,022519                         Authorization Transaction Date

  0033,161934                         Authorization Transaction Time

  0035,BF66                           Validation Code

  0036,112006976774166                Host Transaction Identifier

  0037,0                              Authorizer

  0043,211605                         System Trace Audit Number

  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless , 5 =
                                      swiped)

  0054,01                             POS Entry Mode

  0109,TERM1                          Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,189                            Processor ID

  0115,010                            Transaction Qualifier (010 =
                                      credit; 030 = debit)

  0125,0106211934                     Retrieval Reference Number (may
                                      need to appear on receipt)

  0126,2                              Track Indicator (may need to appear
                                      on receipt)

  0128,1.00                           Original Authorization Amount

  0129,1                              Compliance Data

  0130,19.00                          Total Authorized Amount

  0131,00                             CPS Total Incremental Auths sent

  0140,A                              Merchant Currency

  0651,00003@;\                       Reversal data (for reversal, if
  01001175950315\                     needed)
  17501600000471705000000000\         
  00419039807417117595                

  0738,106781MMCC539137 Y 0225        Recurring Compliance Data

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,400555\*\*\*\*\*\*4460         Masked Account Number (for printing
                                      on receipt)

  1009,AA                             Host Response Code

  1010,COMPLETE                       Gateway Response Message

  1012,1832                           Gateway Batch Number

  1200,0000AA                         Issuer Network Information

  1339,00                             EMV Response Code

  1359,4                              EMV CVM Indicator

  4747,020111                         Third Party Interface POS Data Code

  5002,80649419                       Device Serial Number

  5004,G2                             Encryption Provider ID

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  5071,xxx...                         Defines whether card and cardholder
                                      are present. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  5104,xxx...                         Tip Settings. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  7007,1112006767740668               Transaction Link Identifier (unique
                                      identifier to link transactions)

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

\

Void Return Message (Tran Type 17) {#00014 .h2}
----------------------------------

Simplify supports a Void Return message from the POS process if
tokenization is implemented. Customers might want to void a return
transaction after it has been completed. The POS does this by sending a
Void Return message to Simplify.

The following table shows a sample of fields in the Void Return message
that may need to match fields in the original transaction. See the
**Fusebox Integration Guide** for more information on this Transaction
Type.

\

  -----------------------------------------------------------------------
  API Field \#                        Description
  ----------------------------------- -----------------------------------
  0002                                Transaction Amount

  0003                                Account Data (token)

  0004\                               Expiration Date

  0007                                Transaction ID / Reference Number

  0109                                Terminal ID

  8002                                Location Name

  8006                                Chain Code
  -----------------------------------------------------------------------

\

### Request {#request-5 .h3}

An example of a Void Return Request message (from the POS to Simplify)
is:

\

  API Field \#, Value        Description
  -------------------------- -------------------------------------------------------------------------------------------------------
  0001,17                    Transaction Type.
  0002,125.98                Transaction Amount. Must match Return response.
  0003,ID:1120106195107475   Account Data. Must match Return response.
  0004,1208                  Expiration Date -- MMYY. Must match Return response (if present).
  0007,1025                  Transaction ID / Reference Number. Must match Return response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143515                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID. Must match Return response.
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit). Must match Return response.
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  8002,RETL01                Location Name. Must match Return response.
  8006,TSTLAR                Chain Code. Must match Return response.

\

### Response {#response-5 .h3}

An example of a Void Return Request message (from the POS to Simplify)
is:

  API Field \#, Value        Description
  -------------------------- -------------------------------------------------------------------------------------------------------
  0001,17                    Transaction Type.
  0002,125.98                Transaction Amount. Must match Return response.
  0003,ID:1120106195107475   Account Data. Must match Return response.
  0004,1208                  Expiration Date -- MMYY. Must match Return response (if present).
  0007,1025                  Transaction ID / Reference Number. Must match Return response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143515                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID. Must match Return response.
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit). Must match Return response.
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  8002,RETL01                Location Name. Must match Return response.
  8006,TSTLAR                Chain Code. Must match Return response.

\

Void Transaction Message (Tran Type 11) {#void-transaction-message-tran-type-11 .h2}
---------------------------------------

In some transactions, the customer may wish to void a Sale transaction
after it has already been completed. The POS can accomplish this by
sending a Void Transaction message to Simplify. A Void Transaction is
also used to financially recover from a timed-out financial request.

In some transactions, the customer may wish to void a Sale transaction
after it has already been completed. The POS can accomplish this by
sending a Void Transaction message to Simplify. A Void Transaction is
also used to financially recover from a timed-out financial request.

\

  -----------------------------------------------------------------------
  API Field \#                        Description
  ----------------------------------- -----------------------------------
  0002                                Transaction Amount

  0003                                Account Data (token)

  0004\                               Expiration Date

  0007                                Transaction ID / Reference Number

  0109                                Terminal ID

  8002                                Location Name

  8006                                Chain Code
  -----------------------------------------------------------------------

### Request {#void_request .h3}

An example of a [Void Request](#void_request) message (from the POS to
Simplify) is:

  API Field \#, Value        Description
  -------------------------- ------------------------------------------------------------------------------
  0001,11                    Transaction Type.
  0002,125.98                Transaction Amount. Must match Sale response.
  0003,ID:1102571965098318   Account Data. Must match Sale response.
  0004,1215                  Expiration Date -- MMYY. Must match Sale response (if present).
  0007,1025                  Transaction ID / Reference Number. Must match Sale response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143515                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID. Must match Sale response.
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit). Must match Sale response.
  8002,RETL01                Location Name. Must match Sale response.
  8006,TSTLAR                Chain Code. Must match Sale response.

\

### Response {#response-6 .h3}

An example of a Void Response message (from Simplify to the POS) is:

\

  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------
  0001,11                             Transaction Type.
  0002,125.98                         Transaction Amount
  0003,ID:1102571965098318            Account Token (returned by Fusebox)
  0006,CMC663                         Authorization Code (returned by Fusebox)
  0007,1025                           Transaction ID / Reference Number
  0009,0020                           Fusebox -- Host Batch number
  0011,xxx..                          User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                         Transaction Date (current date) -- MMDDYY
  0014,143515                         Transaction Time (current time) -- HHMMSS
  0030,1                              Fusebox -- Online Indicator
  0032,022519                         Fusebox -- Authorization Transaction Date
  0033,105319                         Fusebox -- Authorization Transaction Time
  0035,1008                           Validation Code
  0036,MCC0DFA9A                      Host Transaction Identifier
  0037,0                              Fusebox -- Authorizer
  0043,022284                         System Trace Audit Number
  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4    POS Data Code
  0052,5                              Transponder / Proximity Indicator (0 = contact; 2 = contactless, 5 = swiped)
  0054,90                             POS Entry Mode
  0109,TERM1                          Terminal ID. Must match Sale response.
  0110,205                            Cashier ID
  0112,400                            Fusebox -- Processor ID
  0115,010                            Transaction Qualifier (010 = credit; 030 = debit)
  0125,1008145319                     Retrieval Reference Number (may need to appear on receipt)
  0126,0                              Track Indicator (may need to appear on receipt)
  0128,1.00                           Original Authorization Amount
  0129,0                              Fusebox -- Compliance Data
  0130,1.00                           Authorized Amount
  0131,00                             CPS Total Incremental Auths sent
  0132,0                              Authorization Reversal Sent
  0140,USD                            Fusebox -- Merchant Currency
  0651,0000000                        Reversal data (for reversal, if needed)
  1000,MC                             Card Type
  1001,MASTERCARD                     Card Name
  1003,0000                           Gateway Response Code
  1004,ACKNOWLEDGED                   Host Response Message
  1005,0031940008024682711000         Merchant Number
  1008,\*\*\*\*\*\*\*\*\*\*\*\*1114   Masked Account Number (may need to appear on receipt)
  1009,AA                             Host Response Code
  1010,COMPLETE                       Gateway Response Message
  1012,0020                           Gateway Batch Number
  1200,0000AA                         Issuer Network Information
  1359,4                              EMV CVM Indicator
  5002,80378002                       Device Serial Number
  5004,G2                             Encryption Provider ID
  5010,EMVDC0838                      EMV kernel version
  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field Definitions](#00073).
  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  7007,1114281539351186               Transaction Link Identifier (unique identifier to link transactions)
  8002,RETL01                         Location Name. Must match Sale response.
  8006,TSTLAR                         Chain Code. Must match Sale response.

\

Gift Card Messages (Tran Types 01, 02, 07, 09, 11, 17, 24) {#00015 .h2}
----------------------------------------------------------

Simplify supports Gift Card messages from the POS process. As indicated
in the table, supported Gift Card messages are identified as follows:

-   All Gift Card messages send a value of 50 in Field 115 (Transaction
    Qualifier).

-   The type of Gift Card transaction is indicated by Field 1 (Tran
    Type) and Field 117 (Stored Value Function).

\

  Type of Transaction                    Field 1     Field 115        Field 117
  -------------------------------------- ----------- ---------------- -----------------------
                                         Tran Type   Tran Qualifier   Stored Value Function
  Auth Only                              01          50               n/a
  Redemption/Redemption with Cash Back   02          50               5
  Redemption with Cash Out/Cash Out      02          50               6
  Prior Auth / Voice Auth                07          50               7
  Card Activation                        09          50               1
  Card Issuance                          09          50               2
  Card Reload                            09          50               3
  Return                                 09          50               4
  Void Redemption                        11          50               5
  Void Activation                        17          50               1
  Void Issuance                          17          50               2
  Void Reload                            17          50               3
  Void Return                            17          50               4
  Balance Inquiry                        24          50               n/a

\

A sample Card Issuance request/response is shown below. Please refer to
the **Gift and Stored Value Card Integration Guide** for more
information on this Transaction Type.

### Request {#request-6 .h3}

An example of a **Card Issuance Request** message (from the POS to
Simplify) is:

\

  API Field \#, Value   Description
  --------------------- ----------------------------------------------------------------------------------------------------------------
  0001,09               Transaction Type of 9, in combination with Field 115 of 050 and Field 117 of 2, indicates a Gift Card Issuance
  0002,50.00            Dollar amount to be authorized
  0007,1025             Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,131535           Transaction Time (current time) -- HHMMSS
  0109,RETAIL           Terminal ID (provided by Elavon)
  0110,00000301         Cashier ID
  0115,050              Transaction Qualifier (050 = Gift / Stored Value)
  0117,2                Stored Value Function. A Value of 2 indicates a Card Issuance
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  8002,PLSNTN           Location Name (provided by Elavon)
  8006,TSTLAR           Chain Code (provided by Elavon)

\

### Response {#response-7 .h3}

An example of a **Card Issuance Response** message (from Simplify to the
POS) is:

\

  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------
  0001,09                             Transaction Type
  0002,000050.00                      Transaction Amount
  0003,ID:1120106195107475            Account Token (returned by Fusebox)
  0004,1218                           Expiration Date -- MMYY
  0006,001000                         Authorization Code (returned by Fusebox)
  0007,1025                           Transaction ID/Reference Number
  0011,xxx..                          User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                         Transaction Date (current date) -- MMDDYY
  0014,131535                         Transaction Time (current time) -- HHMMSS
  0043,500586                         System Trace Audit Number
  0052,5                              Transponder / Proximity Indicator (0 = contact; 2 = contactless , 5 = swiped)
  0054,01                             POS Entry Mode
  0109,RETAIL                         Terminal ID (provided by Elavon)
  0110,00000301                       Cashier ID
  0112,34                             Fusebox -- Processor ID
  0115,050                            Transaction Qualifier (010 = credit; 030 = debit)
  0117,2                              Stored Value Function
  0125,111293621357294                Retrieval Reference Number (may need to appear on receipt)
  0126,0                              Track Indicator (may need to appear on receipt)
  0140,USD                            Merchant Currency
  1000,SV                             Card Type
  1001,SVS                            Card Name
  1003,0000                           Gateway Response Code
  1004,01 -- APPROVAL                 Host Response Message
  1005,061286                         Merchant Number
  1008,600649\*\*\*\*\*\*\*\*\*1083   Masked Account Number (for printing on receipt)
  1009,01                             Host Response Code
  1010,COMPLETE                       Gateway Response Message
  1012,1784                           Gateway Batch Number
  5002,169018710                      Device Serial Number
  5004,G2                             Encryption Provider ID
  5010,EMVDC0838                      EMV Kernel Version
  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field Definitions](#00073).
  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  7007,1111293621357294               Transaction Link Identifier. A unique identifier to link transactions
  8002,PLSNTN                         Location Name (provided by Elavon)
  8006,TEST                           Chain Code (provided by Elavon)

\

Inquiry Message (Tran Type 22) {#00016 .h2}
------------------------------

In normal cases, Simplify will respond to a POS/PMS request in a timely
manner. If this does not occur, the POS/PMS will need to send an
**Inquiry** message to Simplify requesting information from Fusebox
about the transaction. An **Inquiry** message should contain all
elements of the original transaction.

-   Inquiry processing is required for the following situations:

    -   No response to a financial request.

    -   Field 1010 in the financial response contains one of the
        following:\
        \*SLR STAND-IN.\
        \*SLR COMMUNICATIONS ERROR.

-   After sending an **Inquiry** message, Elavon highly recommends that
    the POS/PMS wait for a response and continue processing based on the
    response. *The **Inquiry** message should be resent until it
    receives one of the following*:

    -   Fusebox approval for the original transaction

    -   Fusebox decline for the original transaction

    -   Fusebox no record response (Field 1010 = NO RECORDS FOUND).

<!-- -->

<!-- -->

-   The possible outcomes at the POS/PMS after sending an **Inquiry**
    message are as follows:

    -   The POS/PMS receives a normal transaction response. (Transaction
        Type = original). This response indicates that the **Inquiry**
        message and the original transaction were both processed online
        by Fusebox. The POS/PMS should treat this response as a normal
        response to the original transaction.

    -   The POS/PMS receives a no record response. (Transaction Type =22
        and Field 1010 contains NO RECORDS FOUND). This response
        indicates that the original request was NOT processed by
        Fusebox. The POS/PMS can proceed in accordance with corporate
        policy. E.g. a [Void Request](#void_request) can be sent for the
        transaction.

    -   If the **Inquiry** message times out at the host, the POS/PMS
        will receive a host down response (Transaction Type = 22 and
        Field 1010 contains \*SLR COMMUNICATIONS ERROR. or \*SLR SWITCH
        TIMEOUT.) The POS/PMS must then re-send the **Inquiry** message
        until it receives a host response

    -   If the POS/PMS times out before receiving an **Inquiry
        Response**, it must re-send the **Inquiry** message until it
        receives a host response.

-   The **Inquiry** message can be re-sent by Simplify or through a back
    channel. All rules for Inquiry processing apply regardless of how
    the **Inquiry** message is re-sent.

-   The **Inquiry** message can be sent any time before the Gateway
    Batch Close.

The following table shows a sample of fields in the **Inquiry** message
that may need to match fields in the original transaction. See the
**Fusebox Integration Guide** under "Transaction Types" \> "Transaction
Inquiry (22)" for more information on this Transaction Type.

\

  API Field \#   Description
  -------------- -----------------------------------
  0002           Transaction Amount
  0007           Transaction ID / Reference Number
  0109           Terminal ID
  8002           Location Name
  8006           Chain Code

\

### Request {#request-7 .h3}

An example of an **Inquiry Request** message (from the POS to Simplify)
is as follows:

  API Field \#, Value   Description
  --------------------- ----------------------------------------------------------------------
  0001,22               Tran Type.
  0002,5.00             Transaction Amount. Must match the financial request.
  0007,1025             Transaction ID / Reference Number. Must match the financial request.
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,131559           Transaction Time (current time) -- HHMMSS
  0017,0.00             Cash Back Amount
  0109,TERM1            Terminal ID. Must match the financial request.
  1008,ID:              Set to ID: to request that an account token be returned by Fusebox.
  8002,RETL01           Location Name. Must match the financial request.
  8006,TSTLAR           Chain Code. Must match the financial request.

### Response {#response-8 .h3}

An example of an **Inquiry Response** message (from Simplify to the POS)
is as follows:

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,02                             Original Transaction Type (entire
                                      response = original host response)

  0002,5.00                           Transaction Amount

  0003,ID:4546705467010002            Account Token (returned by Fusebox)

  0004,1221                           Expiration Date - MMYY

  0006,CVI758                         Authorization Code (returned by
                                      Fusebox)

  0007,1025                           Transaction ID / Reference Number

  0009,001                            Fusebox -- Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction Date (current date) --
                                      MMDDYY

  0014,151729                         Transaction Time (current time) --
                                      HHMMSS

  0017,0.00                           Cash Back Amount

  0030,1                              Fusebox -- Online Indicator

  0032,022519                         Fusebox -- Authorization
                                      Transaction Date

  0033,181733                         Fusebox -- Authorization
                                      Transaction Time

  0035,D07D                           Validation Code

  0036,114120980253909                Host Transaction Identifier

  0037,2                              Fusebox -- Authorizer

  0043,214872                         System Trace Audit Number

  0047,M;1;1;1;0;1;2;5;4;1;3;C;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless; 5 =
                                      swiped)

  0054,90                             POS Entry Mode

  0062,110                            Service Code

  0109,TERM1                          Terminal ID

  0110,205                            Cashier ID

  0112,400                            Fusebox -- Processor ID

  0115,010                            Transaction Qualifier (010 =
                                      Credit; 030 = debit)

  0125,430181733                      Retrieval Reference Number (may
                                      need to appear on receipt)

  0126,2                              Track Indicator (may need to appear
                                      on receipt

  0129,1                              Fusebox -- Compliance Data

  0130,5.00                           Authorized Amount

  0140,USD                            Fusebox -- Merchant Currency

  0201,0.00                           Tip Amount

  0651,00003@;01001175950315\         Reversal data
  17501600000471705000000000\         
  00419039807417117595                

  0738,106781MMCC539137 Y 0225        Recurring Compliance Data

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,\*\*\*\*\*\*\*\*\*\*\*\*0002   Masked Account Number (may need to
                                      appear on receipt)

  1009,AA                             Host Response Code

  1010,COMPLETE                       Gateway Response Message

  1012,0039                           Gateway Batch Number

  1200,0000AA                         Issuer Network Information

  1339,00                             EMV Response Code

  1359,4                              EMV CVM Indicator

  4747,050311                         Third Party Interface POS Data Code

  5002,80378002                       Device Serial Number

  5004,G2                             Encryption Provider ID

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  7007,1114281539351186               Transaction Link Identifier (unique
                                      identifier to link transactions)

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

\

DCC Inquiry Message (Tran Type 46) {#00017 .h2}
----------------------------------

The DCC Inquiry Message is a non-financial message used to support DCC
processing. If Simplify receives a DCC Inquiry Request from the POS, it
will pass through the message to Fusebox. For more information on DCC,
see [Dynamic Currency Conversion (DCC)](#0007).

\

Token Request Message (Tran Type 37) {#00018 .h2}
------------------------------------

Simplify supports a **Token Request** message from the POS process.

The **Token Request** message is a non-financial message, used to obtain
the Fusebox-assigned token for an account number.

### Request {#request-8 .h3}

An example of a **Token Request** message (from the POS to Simplify) is:

\

  API Field \#, Value   Description
  --------------------- --------------------------------------------------------------------------------
  0001,37               Transaction Type.
  0002,0.00             Transaction Amount. The amount should be 0.00 for a Token Request
  0007,1045             Transaction ID / Reference Number
  0109,TERM1            Terminal ID (provided by Elavon)
  0110,205              Cashier ID
  0115,010              Transaction Qualifier (010 = credit; 030 = debit)
  1008,ID:              Set to the value 'ID:' to request that an account Token be returned by Fusebox
  8002,RETL01           Location Name (provided by Elavon)
  8006,TSTLAR           Chain Code (provided by Elavon)

\

### Response {#response-9 .h3}

An example of a **Token Request** message (from the POS to Simplify) is:

\

  API Field \#, Value           Description
  ----------------------------- ------------------------------------------------------------------------------
  0001,37                       Transaction Type
  0002,0.00                     Transaction Amount
  0003,ID:1111748353147271      Account Token (returned by Fusebox)
  0004,1208                     Expiration Date -- MMYY
  0007,1045                     Transaction ID / Reference Number
  0052,5                        Transponder / Proximity Indicator (0 = contact; 2 = contactless, 5 = swiped)
  0109,TERM1                    Terminal ID (provided by Elavon)
  0110,205                      Cashier ID
  0115,010                      Transaction Qualifier (010 = credit; 030 = debit)
  0126,2                        Track Indicator
  1000,VI                       Card Type
  1001,VISA                     Card Name
  1003,0000                     Gateway Response Code
  1004,ACKNOWLEDGED             Host Response Message
  1008,400555\*\*\*\*\*\*4460   Masked Account Number
  1010,COMPLETE                 Gateway Response Message
  5002,80378002                 Device Serial Number
  7007,11111799604661403        Transaction Link Identifier. A unique identifier to link transactions
  8002,RETL01                   Location Name (provided by Elavon)
  8006,TSTLAR                   Chain Code (provided by Elavon)

\

Cancel Message (Tran Type 80) {#00018a .h2}
-----------------------------

Simplify supports a **Cancel** message from the POS process. When
Simplify receives a **Cancel Request**, it will attempt to cancel the
transaction (return to the Closed state) and send a **Cancel Response**
to the POS.

The **Cancel** message is available to allow the POS process to clear
the PIN Pad. This message should be used if the POS process and the PIN
Pad are out of sync.

### Request {#request-9 .h3}

An example of a **Cancel Request** is as follows:

API Field \#, Value

Description

0001,80

Transaction Type

0007,7765

Transaction ID / Reference Number

0013,092818

Transaction Date (current date) -- MMDDYY

0014,143005

Transaction Time (current time) -- HHMMSS

\

### Response {#response-10 .h3}

#### Transaction Cancelled {#transaction-cancelled .h4}

An example of a **Cancel Response** for a successful Cancel is as
follows:

API Field \#, Value

Description

0001,80

Transaction Type

0007,7765

Transaction ID / Reference Number

0011,xxx..

User Data. See [Simplify-Controlled Field Definitions](#00073) for the
use of this field

0013,092818

Transaction Date (current date) -- MMDDYY

0014,143005

Transaction Time (current time) -- HHMMSS

\

#### Transaction Not Cancelled {#transaction-not-cancelled .h4}

An example of a **Cancel Response** for an unsuccessful Cancel
(transaction already being processed) is as follows:

API Field \#, Value

Description

0001,80

Transaction Type

0007,7765

Transaction ID / Reference Number

0011,xxx..

User Data. See [Simplify-Controlled Field Definitions](#00073) for the
use of this field

0013,092818

Transaction Date (current date) -- MMDDYY

0014,143005

Transaction Time (current time) -- HHMMSS

1003,0030

Gateway Response Code

1004,0030

Host Response Message

1009,0030

Host Response Code

1010,\*SLR Busy.

Gateway Response Message

5002,284431938

Device Serial Number

\

### Health Message (Tran Type 73) {#health-message-tran-type-73 .h2}

Simplify supports **Health** messages from the POS process.

A **Health** message is sent by the POS process to verify that Simplify
is up and running on the PIN Pad. If Simplify receives a **Health**
message, it echoes back the same message it receives.

If the POS process does not receive a response to the **Health**
message, the POS process disconnects the TCP/IP socket and initiates the
TCP/IP socket connection again.

\

  API Field \#, Value   Description
  --------------------- --------------------------------------------
  0001,73               Transaction Type
  0007,7765             Transaction ID / Reference Number
  0013,022519           Transaction Date (current date) --- MMDDYY
  0014,143005           Transaction Time (current time) -- HHMMSS

\

Batch Close Message (Tran Type 13) {#00019 .h2}
----------------------------------

Simplify supports a **Batch Close** message from the POS process. This
message requests that a current batch be closed. The scope of the batch
close is determined as follows:

-   If the Terminal ID is sent in Field 109 of the **Batch Close
    Request**, the batch close will only apply to transactions run on
    the PIN pad specified by this Terminal ID.

-   If the Location Name is sent in Field 8002, the batch close will
    apply to transactions run in the entire location specified by this
    Location Name (typically: one store).

-   If the Chain Code is sent in Field 8006, the batch close will apply
    to transactions run for the entire chain specified by this Chain
    Code.

In the following example, the Terminal ID is sent in Field 109, so the
batch close will only apply to transactions run on the specified PIN
pad.

For more details on this tran type, see the **Fusebox Integration
Guide**.

### Request {#request-10 .h3}

An example of a **Batch Close Request** message (from the POS process to
the Simplify application) is:

\

  API Field \#, Value   Description
  --------------------- -----------------------------------------------------------------
  0001,13               Transaction Type
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0109,RETERM1          Terminal ID (provided by Elavon)

\

### Response {#response-11 .h3}

An example of a **Batch Close Response** message (from the Simplify
application to the POS process) is:

\

  API Field \#, Value     Description
  ----------------------- ------------------------------------------------------------------------
  0001,13                 Transaction Type
  0011,xxx..              User Data. See [Simplify-Controlled Field Definitions](#00073).
  0109,RETERM1            Terminal ID (provided by Elavon)
  0140,USD                Merchant Currency Trigraph
  1003,0000               Gateway Response Code
  1004,ACKNOWLEDGED       Host Response Message
  1010,COMPLETE           Gateway Response Message
  1012,0248               Gateway Batch Number
  1013,26.00              Local Batch Net Amount
  1014,2                  Local Batch Transaction Count
  1016,26.00              Host Batch Net Amount
  1017,2                  Host Batch Transaction Count
  1018,26.00              Funded Batch Amount
  1019,2                  Funded Batch Transaction Count
  7007,1115126747425133   Transaction Link Identifier. A unique identifier to link transactions.

\

Batch Inquiry Message (Tran Type 14) {#00020 .h2}
------------------------------------

Simplify supports a **Batch Inquiry** message from the POS process. This
message is used to obtain information about a current batch.

The scope of this inquiry is determined in the same manner as for a
**Batch Close** message:

-   If the Terminal ID is sent in Field 109 of the **Batch Inquiry
    Request**, the inquiry will only apply to transactions run on the
    PIN pad specified by this Terminal ID.

-   If the Location Name is sent in Field 8002, the inquiry will apply
    to transactions run in the entire location specified by this
    Location Name (typically: one store).

-   If the Chain Code is sent in Field 8006, the inquiry will apply to
    transactions run for the entire chain specified by this Chain Code.

In the following example, the Location Name is sent in Field 8002, so
the inquiry will only apply to transactions run in the specified
location.

For more details on this tran type, see the **Fusebox Integration
Guide**.

### Request {#request-11 .h3}

An example of a **Batch Inquiry Request** message (from the POS to the
Simplify application) is:

\

  API Field \#, Value   Description
  --------------------- -----------------------------------------------------------------
  0001,14               Transaction Type
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  8002,SIMTESTVOLT      Location Name (provided by Elavon)

\

### Response {#response-12 .h3}

An example of a **Batch Inquiry Response** message (from the Simplify
application to the POS) is:

\

  API Field \#, Value     Description
  ----------------------- -----------------------------------------------------------------------
  0001,14                 Transaction Type
  0011,xxx..              User Data. See [Simplify-Controlled Field Definitions](#00073).
  0140,USD                Merchant Currency Trigraph
  1003,0022               Gateway Response Code
  1004,EMPTY BATCH        Host Response Message
  1010,EMPTY BATCH        Gateway Response Message
  1012,0248               Gateway Batch Number
  7007,1115126747595135   Transaction Link Identifier. A unique identifier to link transactions
  8002,SIMTESTVOLT        Location Name (provided by Elavon)

\

Non-Financial Messages (Tran Type 36) {#00021 .h2}
-------------------------------------

Transaction Type 36 is used for non-financial purposes. The specific
purpose of a Tran Type 36 message is indicated by the value in the first
two bytes of Field 11, which define the Message Type. Field 5001 may be
used to further define the request and/or return data in the response.

Transaction Type 36 is used for non-financial purposes. The specific
purpose of a Tran Type 36 message is indicated by the value in the first
two bytes of Field 11, which define the Message Type. Field 5001 may be
used to further define the request and/or return data in the response.

### Non-Financial Message Format {#non-financial-message-format .h3}

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type 36. Non-Financial
                                      message

  0011,xxx..                          User Data.\
                                      The first two bytes of Field 11
                                      define the **Message Type** , as
                                      described below.\
                                      Usage of other bytes varies based
                                      on Message Type; see
                                      [Simplify-Controlled Field
                                      Definitions](#00073) Definitions.

  5001,xxx..                          Non-Financial Data.\
                                      The format of this field depends on
                                      the value of message type.\
                                      See the sections on specific
                                      messages for details.
  -----------------------------------------------------------------------

\

### Message Types {#message-types .h3}

Currently defined **Message Types** (Field 11) are as follows:

  -----------------------------------------------------------------------
  Message Type            Use                     Direction
  ----------------------- ----------------------- -----------------------
  01                      Signature Request       from POS to Simplify

  02                      Signature Response      from Simplify to POS

  03                      Demo Message (NOT USED) (not used)

  06                      Version Number Inquiry  Request from POS to
                          Message                 Simplify.\
                                                  Response from Simplify
                                                  to POS

  07                      Initiate IngEstate      Request from POS to
                          Message                 Simplify.\
                                                  Response from Simplify
                                                  to POS

  10                      Scrolling Receipt       From POS to Simplify
                          Message                 

  11                      Scrolling Receipt Stop  from POS to Simplify
                          Message                 

  12                      Exit Reversal Mode      from POS to Simplify
                          Message                 

  13                      Reserved for Bridge\    Request from Bridge to
                          (SAF Done Message. Not  Simplify\
                          used by POS)            Response from Simplify
                                                  to Bridge

  14                      Informational Prompt    Request from POS to
                          Message                 Simplify.\
                                                  Response from Simplify
                                                  to POS

  40                      Quick Chip Message      Request from POS to
                                                  Simplify\
                                                  Response from Simplify
                                                  to POS

  45                      Print Request Message   Request from POS to
                                                  Simplify\
                                                  Response from Simplify
                                                  to POS

  51                      Status Message          from POS to Simplify
  -----------------------------------------------------------------------

\

Signature Message (Tran Types 36-01, 36-02) {#00022 .h2}
-------------------------------------------

Simplify supports a signature process on touchscreen PIN Pads. When this
process is triggered, Simplify will prompt for a signature and send the
signature data (or customer Cancel) to the POS in a **Signature
Response** (36-02) message. There are two ways to trigger signature
processing:

-   Request message -- The POS can send Simplify a **Signature Request**
    (36-01) message.

-   [Auto Signature](#00064) -- For approved **Sale**, **Auth Only** and
    **Return** transactions, signature process can occur automatically
    (no **Signature Request** required). For details, see [Auto
    Signature](#00064).

The template used for the Signature screen is controlled by a Screen ID
subfield in field 11 of the **Signature Request**. Additional screen
details are defined by field 5001 of the request. The value of Screen ID
will determine the screen elements that can be controlled by field 5001,
as follows:

-   If Screen ID is 001, field 5001 can be used to define up to four
    lines of fixed text, with up to 40 characters per line.

-   If Screen ID is 002, field 5001 can be used to define up to three
    screen areas, from top to bottom: as follows:

    -   Button area -- Define height (as percentage of screen). Buttons
        are fixed size and vertically centered in the button area.

    -   Text area -- Define height (as percentage of screen). Define
        font size. Define rows of texts. Maximum number of rows depends
        on height of text area and font size.

    -   Signature area -- Height is remaining percentage of screen.

If signature data is captured by Simplify, it will be sent to the POS in
field 5000 of the Signature Response. The format of this data is
three-byte ASCII.

The detailed format of field 5001 and sample Signature Request and
Response messages are shown below:

### Field 5001 Format {#field-5001-format .h3}

\

+-----------------------------------+-----------------------------------+
| Message                           | Description                       |
+===================================+===================================+
| (Generic format)                  | The format of this field is       |
|                                   | TTTLLLVVV...VV (can be repeated   |
|                                   | up to four times in Request),     |
|                                   | where:\                           |
|                                   | TTT is a Tag\                     |
|                                   | LLL is the length of the data.\   |
|                                   | VVV..VV is the data               |
+-----------------------------------+-----------------------------------+
| Request (optional)                | Provides the POS with some        |
|                                   | control over the signature        |
|                                   | screen.\                          |
|                                   | Available tags depend on the      |
|                                   | Screen ID sent in field 11 bytes  |
|                                   | 6-8.\                             |
|                                   | \                                 |
|                                   | For Screen ID = 001:\             |
|                                   | TTT - Supported tags are:\        |
|                                   | 001 -- Text line 1 (Maximum       |
|                                   | length of 40)\                    |
|                                   | 002 -- Text line 2 (Maximum       |
|                                   | length of 40)\                    |
|                                   | 003 -- Text line 3 (Maximum       |
|                                   | length of 40)\                    |
|                                   | 004 -- Text line 4 (Maximum       |
|                                   | length of 40)\                    |
|                                   | VVV..VV defines the text to be    |
|                                   | displayed.\                       |
|                                   | \                                 |
|                                   | For Screen ID = 002\              |
|                                   | TTT - Supported tags are:\        |
|                                   | 001 -- Defines screen layout,     |
|                                   | font size and user text\          |
|                                   | VVV..VV defines screen and text   |
|                                   | formatting, followed by the text  |
|                                   | to be displayed (see sample       |
|                                   | below)\                           |
|                                   |                                   |
|                                   | ::: {.notices .note}              |
|                                   | <div>                             |
|                                   |                                   |
|                                   | **Note:** If a PIN Pad model      |
|                                   | supports fewer text lines than    |
|                                   | defined by this field, the excess |
|                                   | lines will be ignored.            |
|                                   |                                   |
|                                   | </div>                            |
|                                   | :::                               |
+-----------------------------------+-----------------------------------+
| Response\                         |                                   |
| (not used)                        |                                   |
+-----------------------------------+-----------------------------------+

\

### Request (Screen ID = 001) {#request-screen-id-001 .h3}

An example of a **Signature Request** message (from the POS process to
the Simplify application) for Screen ID = 001 is:

\

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type. A value of 36   |
|                                   | indicates a Non- Financial        |
|                                   | transaction                       |
+-----------------------------------+-----------------------------------+
| 0011,xxx..                        | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,001019\                      | See format described above.\      |
| Work order \# 112233002018\       |                                   |
| Estimate = \$259.00               |                                   |
+-----------------------------------+-----------------------------------+

\

### Request (Screen ID = 002) {#request-screen-id-002 .h3}

An example of a **Signature Request** message (from the POS process to
the Simplify application) for Screen ID = 002 is:

\

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type. A value of 36   |
|                                   | indicates a Non- Financial        |
|                                   | transaction                       |
+-----------------------------------+-----------------------------------+
| 0011,xxx..                        | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,00109220FS50FS5FS\           | See format described above.\      |
| Message 1; Message 2; Message 3;  |                                   |
| Message 4; Message 5; Message 6   |                                   |
+-----------------------------------+-----------------------------------+

### Response {#response-13 .h3}

An example of a **Signature Response** message (from the Simplify
application to the POS process) is:

  API Field \#, Value                      Description
  ---------------------------------------- ------------------------------------------------------------------------------
  0001,36                                  Transaction Type. A value of 36 indicates a Non- Financial transaction
  0011,xxx..                               User Data. See [Simplify-Controlled Field Definitions](#00073).
  0052,5                                   Transponder / Proximity Indicator (0 = contact; 2 = contactless, 5 = swiped)
  5000,xxxxxxxxxxxxxxxxxxxxxxxx.......xx   Signature data

Version Number Inquiry Message (Tran Type 36-06) {#00023 .h2}
------------------------------------------------

Simplify supports a **Version Number Inquiry** message from the POS
process.

The POS can send this message to Simplify when it wants to check the
Simplify application (program) version number, parameter version number,
and/or build number.

The **Version Number Inquiry Request** does not contain field 5001. The
only fields are field 1 (Tran Type = 36) and field 11.

### Field 5001 Format {#field-5001-format-1 .h3}

  -----------------------------------------------------------------------
  Message                             Description
  ----------------------------------- -----------------------------------
  (Generic format)                    The format of this field is
                                      TTTLLLVVV...VV, where:\
                                      TTT is a Tag\
                                      LLL is the length of the data.\
                                      VVV..VV is the data

  Request                             Not used

  Response                            Simplify program, parameter and
                                      build version numbers active in the
                                      PIN Pad.\
                                      TTT - Currently defined tags are:\
                                      006 -- Simplify
                                      program/parameter/build version
                                      values.\
                                      LLL = 040\
                                      VVV..VV\
                                      Positions 1-20 - Simplify program
                                      and parameter version numbers\
                                      Positions 21-40 - Simplify build
                                      number
  -----------------------------------------------------------------------

### Sample Response Message {#sample-response-message .h3}

An example of a **Version Number Inquiry Response** message (from
Simplify to the POS) is:

\

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type. A value of 36   |
|                                   | indicates a Non-Financial         |
|                                   | transaction                       |
+-----------------------------------+-----------------------------------+
| 0011,xxx..                        | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,006040 Ver: 2.23 - 2.23.1    | Version number data               |
| Build: 52302                      |                                   |
+-----------------------------------+-----------------------------------+
| 5002,80378002                     | PIN Pad serial number             |
+-----------------------------------+-----------------------------------+

\

Initiate IngEstate Message (Tran Type 36-07) {#00024 .h2}
--------------------------------------------

IngEstate is Ingenico\'s PIN Pad management system implemented by
Elavon.

Simplify supports an **Initiate IngEstate** message from the POS
process. This message can be used to determine whether an updated
package is available for downloading. Packages are used to download an
updated Simplify application, parameter files, form files, etc.

This message can also be used to update the TMS Identifier, by sending
it in field 5001 of the request (optional). See sample Request below for
details.

The **Initiate** **IngEstate** **Response** message includes the PIN Pad
serial number as well as a Status flag indicating whether the PIN Pad
was able to successfully communicate with IngEstate.

The Initiate IngEstate Message should only be sent when necessary and
based on coordination with Elavon.

### Field 5001 Format {#field-5001-format-2 .h3}

\

  -----------------------------------------------------------------------
  Message                             Description
  ----------------------------------- -----------------------------------
  (Generic format)                    The format of this field is
                                      TTTLLLVVV...VV, where:\
                                      TTT is a Tag\
                                      LLL is the length of the data.\
                                      VVV..VV is the data

  Request (optional)                  TTT - Currently defined tags:\
                                      881 = New TMSID

  Response                            TTT - Currently defined tags are:\
                                      007 -- Download information\
                                      LLL *must* be 052\
                                      VVV..VV\
                                      Bytes 1-50 = Padded PIN Pad Serial
                                      Number (*must* be 50 bytes)\
                                      Bytes 51-52 = Status Flag\
                                      00 -- Request successfully
                                      communicated to IngEstate\
                                      01 -- Simplify is busy with
                                      customer interaction\
                                      02 -- Parameter missing from
                                      parameter file
  -----------------------------------------------------------------------

\

### Request {#request-12 .h3}

An example of a possible **Initiate IngEstate Request** message (from
the POS process to Simplify) is:

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type. A value of 36
                                      indicates a Non-Financial
                                      transaction

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,88100899990000                 881=Tag for TMSID\
                                      008=Length of Data\
                                      99990000=new TMSID
  -----------------------------------------------------------------------

\

### Response {#response-14 .h3}

An example of a possible **Initiate IngEstate Response** message (from
Simplify to the POS process) is:

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type. A value of 36
                                      indicates a Non-Financial
                                      transaction

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,0070528007044000               007 = Tag for File download
                                      information\
                                      052 = Length of data (must be 52)\
                                      80070440 (plus blanks) = padded PIN
                                      Pad Serial \# (must be exactly 50
                                      bytes)\
                                      00 = Status Flag (00 = Simplify
                                      successfully communicated with
                                      IngEstate)
  -----------------------------------------------------------------------

\

### IngEstate Update Flow {#ingestate-update-flow .h3}

::: {.mermaid}
graph TD A\[\"fa:fa-store Point of Sale\"\]
A\--\>\|36-07\|B\[fa:fa-cash-register Simplify\] B\--\>C\[fa:fa-cloud
IngEstate Server\] C \--\> D{Response} D \--\> \|00 - Successful\|
G(Checks for updates) D \--\> \|01 - Error\| H(PINpad busy) D \--\> \|02
- Error\| F(Comm error) G \--\> \|If up to date\| I(Simplify reboots) G
\--\> \|If not up to date\| J(Downloads update from server and reboots)
:::

\

Scrolling Receipt Request Message (Tran Type 36-10) {#00025 .h2}
---------------------------------------------------

Simplify supports a **Scrolling Receipt Request** message from the POS
process. If Simplify receives this message, it responds by displaying
the data sent in the request (no Response message). There are currently
two types of supported data: item data and a running order total.

After a **Scrolling Receipt Request** message is sent, the only message
types that can be processed next are additional **Scrolling Receipt
Request** messages or a **Scrolling Receipt Stop** message.

If additional **Scrolling** **Receipt** **Request** messages are sent,
the additional item data will be appended to the existing item data
display and the running total will be updated with the most recent
total. If the item data will not all fit on the screen, the oldest item
data will not be displayed. Up to five lines of item data can be sent in
a single **Scrolling** **Receipt** **Request** message.

The display of scrolling receipt data is terminated by sending a
**Scrolling Receipt Stop** message (36-11). When the PIN Pad receives
this message, it will display the Idle screen. The PIN Pad will then be
available to process messages as usual.

### Field 5001 Format {#field-5001-format-3 .h3}

\

  -----------------------------------------------------------------------
  Message                             Description
  ----------------------------------- -----------------------------------
  (Generic format)                    The format of this field is
                                      TTTLLLVVV...VV , where:\
                                      TTT is a Tag\
                                      LLL is the length of the data.\
                                      VVV..VV is the data

  Request                             This field can be included in the
                                      Scrolling Receipt Request message.
                                      It allows the POS system to send up
                                      to 6 lines of text to be displayed
                                      on the screen (in addition to the
                                      canned text on the screen).\
                                      TTT - Currently defined tags are:\
                                      001 -- The data describing the item
                                      just scanned.\
                                      (Can be repeated up to 5 times per
                                      message.)\
                                      002 -- The running total of the
                                      price of all items, to be displayed
                                      on the bottom of the screen.\
                                      If tags other than 001 and 002 are
                                      sent, they will be ignored.\
                                      VVV..VV -- This field should
                                      contain data formatted for the
                                      desired display output. The maximum
                                      length will depend on the platform.

  (No Response message)               
  -----------------------------------------------------------------------

\

### Request {#request-13 .h3}

An example of a possible **Scrolling Receipt Request** message (from the
POS process to Simplify) is:

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type. A value of 36
                                      indicates a Non-Financial
                                      transaction

  0011,xxx..                          User Data See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,001025\                        001 = Tag for Item Data\
  2LB PKG STRAWBERRIES\               025 = Length of Item Data\
  2.98002013\                         2LB PKG STRAWBERRIES 2.98 = Item
  SubTotal 2.98                       Data\
                                      002 = Tag for Running Total Data\
                                      013 = Length of Running Total Data\
                                      SubTotal 2.98 = Running Total Data
  -----------------------------------------------------------------------

\

Scrolling Receipt Stop Message (Tran Type 36-11) {#00026 .h2}
------------------------------------------------

Simplify supports a **Scrolling Receipt Stop** message from the POS
process.

When Simplify receives a **Scrolling** **Receipt** **Stop** message, it
responds by stopping the display of Scrolling Receipt data and
displaying the Idle screen. The PIN Pad will then be available to
process messages as usual. There is no response message to the POS.

This message does not contain field 5001. The only fields are field 1
(Tran Type = 36) and field 11. See [Simplify-Controlled Field
Definitions](#00073) for the use of field 11.

\

Exit Reversal Mode Message (Tran Type 36-12) {#00027 .h2}
--------------------------------------------

Reversal mode is used to force a host reversal if this is required
during EMV processing. In this processing mode, Simplify resends the
request until a host response is received, while all new transactions on
the PIN Pad are processed offline.

Simplify supports an **Exit Reversal Mode** **Message**. When Simplify
receives this message, it will send a **Void** **Transaction**
**Response** (11) message to the POS, including the data required to
request the reversal, and return to normal processing mode. For more
information, see **Chip Declines and Simplify Reversal Mode**.

**Important**: Forcing Simplify to exit reversal mode is an exception
procedure that should only be used when necessary. If Simplify is forced
out of reversal mode, the merchant will be responsible for ensuring that
the transaction is reversed by the host, using the data in the **Void**
**Transaction** **Response**. Elavon strongly recommends allowing
Simplify to reverse all host-approved transactions that are declined by
the chip.

Informational Prompting Message (Tran Type 36-14) {#00028 .h2}
-------------------------------------------------

Simplify supports "Informational Prompts", which allow the merchant to
display screens and receive customer feedback in the response. See
[Informational Prompting](#0006).

Quick Chip Message (Tran Type 36-40) {#00029 .h2}
------------------------------------

A Quick Chip message can be sent from the POS to Simplify to allow the
customer to insert, swipe or tap a card during item entry. This allows
the customer to complete all payment steps before the total is known.
See [Quick Chip Tendering](#00065) for more information.

Normal tendering steps must follow the Quick Chip process.

Print Message Request (Tran Type 36-45) {#00030 .h2}
---------------------------------------

The Print Request message allows devices with integrated printers
running the standard (non-Pay\@Table) Simplify application to print
receipts. Simplify will accept a **Print Request** message when the PIN
Pad is in the Closed/Idle state. For all other states, the Simplify
response will indicate that Simplify is busy (field 5110 = 2). The
maximum message size is 4K bytes, including all formatting and function
characters.

The **Print Request** message is currently supported on Move 5000 and
iWL258 PIN Pads.

Print data is sent in fields 5107 (merchant receipt) and 5108 (customer
receipt).

#### 5107 Merchant reciept print data and commands {#merchant-reciept-print-data-and-commands .h4}

Print data must be formatted as follows:

\<FORMAT command\> \<print data\> \#

A FORMAT command takes the form \~\~FORMATabcde\#, where:\
**a** = Font (1=Monospace, 2=Ingenico proportional default)\
**b** = Scale(1-7=xxSmall, Small, Medium, Large, xLarge, xxLarge)\
**c** = Style - Normal, Bold(1-2)(Bold supported only with Monospace\
**d** = Alignment - Left-justified, Center-justified,
Right-justified(1-3)\
**e** = Reverse - Normal, Inverted (1-2)(Black foreground, white
background/ white foreground, black background)

Formatting defined by a FORMAT command will be used until a new FORMAT
comman is sent or the print job completes.

Use /n to start a new line within \<print data\>.

Use \#\# within \<print data\>to print a blank line and then start a new
line.

Use \#\# at the end of \<print data\>to print a blank line after the
data.

ACTION commands can be included in this field. These commands take the
form \~\~\<ACTION\>\#. Available action commands are as follows:

**\~\~BEEP\#** - Calls beep command

**\~\~EJECT\#** - Sends four line feeds for tear-off

**\~\~DISPLAYccc\#** - Sends the specified text (ccc\...) to the PIN Pad
display (replaces default display for current PIN Pad state). Use /n to
start a new line

**\~\~PAUSEnn\#** - Pauses printing for nn seconds. If no nn pause until
Enter is pressed.

**\~\~SIGNATURE\#** - Prints Signature line.

Using two pound signs (\#\#) before \<print data\> or at the end of an
ACTION command will print a blank line before printing the data or
performing the action:

\~\~FORMATabcde\#\#\<print data\>\#

\~\~\<ACTION\>\#\#

\

#### 5108 Customer receipt print data and commands {#customer-receipt-print-data-and-commands .h4}

Same format as API 5107

\

### Request (to demonstrate available formatting) {#request-to-demonstrate-available-formatting .h3}

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type. A value of 36
                                      indicates a Non-Financial
                                      transaction

  0011,xxx..                          User Data See [Simplify-Controlled
                                      Field Definitions](#00073).

  5108,\[see value below\]            Customer receipt print data and
                                      commands\
                                      (see format table above)

  5111, Printing Receipt              Message displayed on PIN Pad during
                                      printing.
  -----------------------------------------------------------------------

\

Status Message (Tran Type 36-51) {#00031 .h2}
--------------------------------

Simplify supports a **Status** **Message** to the POS. This message is
sent to the POS to provide it with status information on the current
transaction.

The **Status** message is informational only and does not follow the
general rules for recovery after a timeout. See [Appendix D: Recovery
after Timeout Flow](#00071) for details.

This message does not contain field 5001. The only fields are field 1
(Tran Type = 36) and field 11. See [Simplify-Controlled Field
Definitions](#00073) for the use of field 11.

\

Stand-In Processing {#0003 .h1}
===================

Simplify can be configured to support Stand-in processing for timed-out
(offline) transactions. A transaction is considered to have timed out
when: (1) the Fusebox response indicates that the Fusebox request to the
authorizer timed out, or (2) Simplify times out before receiving a
Fusebox response. (The Simplify timeout interval for a request to
Fusebox is defined individually for each request from the POS in the
first 3 bytes of Field 11.)

If Stand-in is enabled, a Stand-in Response will be sent for timed-out
transactions, allowing these transactions to be approved offline by the
POS and resubmitted through Simplify (or directly to Fusebox) for host
approval.

**Important:** Note for purposes of [PCI DSS]{.tooltip
tooltip-content="#PCIDSS"
style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}
compliance that a contains encrypted customer data. The merchant is
responsible for making this data unrecoverable after completion of the
authorization process (*PCI DSS 3.0 Requirement 3.2*).

For EMV transactions, Simplify can be configured to return EMV tags in
the Stand-In Response. The POS can include these tags in the resubmitted
transaction. Submitting EMV Stand-In transactions without EMV tags can
cause declines from some issuers. See **Fusebox EMV Integration Guide**
for more information.

Stand-In support is configured independently for each tender type and
applies to the following transaction types:

-   Sale

-   Auth

-   Refund

If Simplify times out waiting for a **Host Response** to one of these
three financial transaction types, the outcome at the POS process will
depend on whether Stand-in is enabled, as follows:

**Stand-in Enabled**

If Stand-in is enabled, the POS process will receive a **Stand-in
Response** (Field 1010 contains "\*SLR STAND-IN.").

Simplify will return encrypted transaction data for Stand-In
transactions. This will allow the transaction to be resubmitted for host
approval. *The* *POS is responsible* for approving or declining all
Stand-In transactions.

**Stand-in Not Enabled**

The POS process will receive a **Host Down Response** (Field 1010
contains "\*SLR COMMUNICATIONS ERROR." or \*SLR SWITCH TIMEOUT.), if
Stand-in is *not* enabled.

Inquiry processing must be performed at this time as described under
[Inquiry Message](#00016).

Note: Inquiry processing is not affected by whether or not Stand-in is
enabled.

\

Stand-In and Online Response Differences {#00032 .h2}
----------------------------------------

The main differences between a **Stand-in Response** and an **Online
Response** occur in the following fields:

  Field \#   Field Name                 Usage
  ---------- -------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  3          Account Data               Online: Token for the account number (from the Fusebox response)Stand-in: If a token is used for authorization, the token is returned. Otherwise, this field contains the encrypted version of the account number.
  4          Expiration Date            Stand-in: If the card was keyed, contains encrypted Expiration Date.
  6          Authorization Code         Online: Approval code returned by Fusebox.Stand-in: "SN:" followed by the Serial Number of the PIN Pad.
  1003       Gateway Response Code      Stand-in: "0000"
  1010       Gateway Response Message   Stand-in: "\*SLR STAND-IN."
  1379       EMV Receipt Field List     Online: From Fusebox, for use on declines (see Fusebox Integration Guide). Stand-in: From Simplify (same format as online).

**Note:** A value of \\\*SLR STAND-IN. in field 1010 *does not mean that
Simplify has performed stand-in.*

Sample Stand-In Response {#00033 .h2}
------------------------

A sample of the **Stand-In Response** for an offline transaction is as
follows:

(Stand-in enabled; EMV enabled but configured not to return EMV tags on
Stand-In)

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,02                             Transaction Type

  0002,1.00                           Transaction Amount

  0003,;&&&&&&\                       Encrypted Track Data\
  &&&&&&&&&&\                         (See under [Usage](/#00079) for
  = &&&&&&&&&&&\                      details.)
  &&&&&&&&&?                          

  0006,SN:80649419                    Serial Number (needed to Decrypt)

  0007,53                             Reference Number

  0011,xxx...                         User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction Date

  0014,104720                         Transaction Time

  0017,0.00                           Cash Back Amount

  0047,C;1;1;1;0;1;\                  POS Data Code
  5;5;4;3;3;C;0;4                     

  0052,0                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless , 5 =
                                      swiped)

  0054,05                             POS Entry Mode

  0109,TERM02                         Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0115,010                            Transaction Qualifier (010 =
                                      credit; 030 = debit)

  0126,2                              Track Indicator (may need to appear
                                      on receipt)

  0201,0.00                           Tip Amount

  1000,VI                             Card Type

  1002,UAT USA/Test Card 03           Cardholder Name

  1003,0000                           Response Code

  1008,476173\*\*\*\*\*\*0119         Masked Account Number

  1010,\*SLR STAND-IN.                Response Message.

  1314,A0000000031010                 Dedicated File Name

  1315,0096                           ICC Application Version Number

  1379,1326\|\                        Offline EMV Receipt Field List
  Application Label: ;1300\|AAC:\     
  ;1307\|TVR: ;1325\|AID: ;           

  1382,F000F0A001                     Additional Terminal Capabilities

  5002,80649419                       Serial Number needed to Decrypt

  5004,OG                             Encryption Provider ID

  5006,FFFF4D4D4D0\                   Encryption Transmission Block
  000C0046C050006                     

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  8002,ONGUARD                        Location Name (provided by Elavon)

  8006,TSTLA3                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

\

Recommended Rules for Handling Stand-In Responses {#00034 .h2}
-------------------------------------------------

The recommended rules for handling **Stand-in Responses** are as
follows:

\

1.  All responses with "\*SLR STAND-IN." need to be recorded by the POS
    (**Stand-In List**). This includes all transactions that were either
    locally approved or locally declined.

2.  Go through the **Stand In-List**.

    a\. If the POS processed the transaction as approved:

        i.  Send an inquiry

            1.  If inquiry response is **APPROVED**   
                (Transaction Type = original)

                a.  Done

            2.  If inquiry response is **NO RECORD    
                FOUND** (Transaction Type = 22)

                a.  Submit the Stand-in Transaction 
                    for processing.

    b\. If the POS processed the transaction as declined:

        i. Send an inquiry

            1.  If inquiry response is **APPROVED**   
                (Transaction Type = original)

                a.  Send a void

            2.  If inquiry response is **NO RECORDS 
                FOUND** (Transaction Type = 22)

                a.  Done

\

Store and Forward Transactions {#00035 .h2}
------------------------------

For a Store and Forward (deferred authorization) transaction resubmitted
through Simplify, the following fields must be sent (in addition to the
regular fields):

  API Field \#, Value   Description
  --------------------- --------------------------------------------------------------------------
  0003                  Encrypted account data
  0004                  Expiry date (if available from the Stand-In Response)
  0115                  Transaction Qualifier (provided by POS or returned in Stand-in Response)
  0116                  Offline Flag (Must be set to 2 if there is no Voice Auth)
  1008                  Should contain ID: if the merchant uses a token
  5002                  Device Serial Number (from Stand-in Response)
  5004                  Encryption Provider ID (from Stand-in Response)
  5005                  Encryption Transmission Block (from Stand-in Response)

\

EMV {#0004 .h1}
===

EMV (for **E**uropay-**M**asterCard-**V**isa) is a global standard
supporting the use of chip cards (ICC cards, "smart cards") for card
present debit and credit transactions.

Simplify supports EMV processing, both contact and contactless, for the
following Tran Types:

-   **Auth Only** (01)

-   **Sale** (02)

-   **Return** (09)

Based on settings, each supported Transaction Type can be processed as
either EMV or swiped. Please contact your Elavon representative for
configuration setting.

When the POS sends a request to Simplify, it must populate the fields
required to process the transaction. For in depth information on message
requirements for EMV, refer to the **Fusebox EMV Integration Guide**.

Simplify will attempt to process a transaction as EMV when the chip
reader successfully communicates with the chip to obtain card data, and
EMV processing is enabled for the card type and transaction type.

EMV processing is largely transparent to the POS, with the exception of
receipt printing. Additional **Status Message** codes are used for EMV
processing; see under [Simplify-Controlled Field Definitions](#00073).

Contactless EMV is supported using rules similar to those used for
contact EMV. Contactless EMV is enabled separately from contact; please
contact your Elavon representative if you would like to enable
contactless EMV. Simplify can also be configured to process contactless
transactions using MSD emulation.

EMV Receipt Printing {#00036 .h2}
--------------------

EMV rules require the printing of additional data on the receipt for
contact and contactless EMV transactions. The fields that must be
printed will vary by TPP (Acquirer) and transaction outcome.

The response message from Simplify for an EMV transaction will provide
the POS with two ways to print required EMV data:

-   The Fusebox response includes fields specifically designed to
    provide receipt data. Simplify adds chip data to these EMV receipt
    fields before sending the POS a response.

-   For more control over printing, the print string can be built by the
    POS from individual data fields in the response, where each field
    contains data for one EMV tag.

See "Sample EMV Sale Message" for examples of EMV receipt fields. See
"EMV Tags" for a list of commonly used tags. For more information, see
the **Fusebox EMV Integration Guide** under "EMV Receipt Details".

EMV Tags {#00037 .h2}
--------

EMV tags are typically present in the response to the POS in the
following fields. (This is a generic list; specific transactions may
omit some of these tags or include others not shown below.)

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0054,05                             POS Entry Mode (EMV Tag 9F39)

  0163,en                             Cardholder Language Preference (EMV
                                      Tag 5F2D)

  1300,6340AF8FFA1D0121               Application Cryptogram (EMV Tag
                                      9F26)

  1301,E8D8ACF3A49D94373030           Issuer Authentication Data (EMV Tag
                                      91)

  1302,221231                         Application Expiration Date (EMV
                                      Tag 5F24)

  1303,5E0300                         Cardholder Verification Method
                                      (CVM) Results (EMV Tag 9F34)

  1305,06010A03602000                 Issuer Application Data (EMV Tag
                                      9F10)

  1306,E0F8C8                         Terminal Capabilities (EMV Tag
                                      9F33)

  1307,8080008000                     Terminal Verification Results (TVR)
                                      (EMV Tag 95)

  1312,124                            Terminal Country Code (EMV Tag
                                      9F1A)

  1313,01                             Application PAN Sequence Number
                                      (EMV Tag 5F34)

  1314,A0000000031010                 Dedicated File Name (EMV Tag 84)

  1315,0096                           ICC Application Version Number (EMV
                                      Tag 9F08)

  1317,008C                           Terminal Application Version Number
                                      (EMV Tag 9F09)

  1318,00000107                       Transaction Sequence Counter (EMV
                                      Tag 9F41)

  1319,1C00                           Application Interchange Profile
                                      (EMV Tag 82)

  1320,0145                           Application Transaction Counter
                                      (ATC) (EMV Tag 9F36)

  1321,40                             Cryptogram Information Data (EMV
                                      Tag 9F27)

  1322,22                             Terminal Type (EMV Tag 9F35)

  1323,F131728B                       Unpredictable Number (EMV Tag 9F37)

  1325,A0000000031010                 ICC Application Identifier (AID)
                                      (EMV Tag 4F)

  1326,Visa Credit                    ICC Application Preferred Name (EMV
                                      Tag 9F12)

  1327,VISA CREDIT                    Terminal Application Label (EMV Tag
                                      50)

  1328,A0000000031010                 Terminal Application Identifier
                                      (AID) (EMV Tag 9F06)

  1332,FF00                           Application Usage Control (EMV Tag
                                      9F07)

  1334,7800                           Transaction Status Information (EMV
                                      Tag 9B)

  1339,00                             EMV Response Code (EMV Tag 8A)

  1350,92                             CA Public Key Index (EMV Tag 8F)

  1354,03                             ICC Public Key Exponent (EMV Tag
                                      9F47)

  1357,124                            ICC Transaction Currency (EMV Tag
                                      5F2A)

  1358,00                             Cryptogram Tran Type (EMV Tag 9C)

  1361,840                            Issuer Currency Code (EMV Tag 5F56)

  1376,000000000000000\               CVM List (EMV Tag 8E)
  0420142045E031F00                   

  1382,F000F0A001                     Additional Terminal Capabilities
                                      (EMV Tag 9F40)
  -----------------------------------------------------------------------

\

Other EMV-Related Response Fields {#00038 .h2}
---------------------------------

In addition to print fields, other fields have also been added to the
Simplify response to support EMV processing. As show in the following
table, some of these added fields provide the POS with information
regarding e.g. data entry mode, terminal capabilities and chip
condition. Please refer to Fusebox integration documentation for more
information.

  -----------------------------------------------------------------------
  API Field               Field Name              Description
  ----------------------- ----------------------- -----------------------
  0047                    POS Data Code           Defines properties of
                                                  the POS device, PIN Pad
                                                  capabilities or the
                                                  cardholder interaction

  0052                    Transponder / Proximity Value based on a
                          Indicator               combination of PIN Pad
                                                  contactless capability,
                                                  card data entry mode
                                                  and type of contactless
                                                  supported (if any)

  0054                    POS Entry Mode          Identifies how the card
                                                  data was entered

  0055                    PIN Capabilities        Identifies whether the
                                                  PIN Pad is capable of
                                                  accepting PIN entry

  0057                    ICC Chip Condition Code Identifies the
                                                  condition of the ICC
                                                  Chip / Account data
                                                  source

  1359                    EMV CVM Verification    Field to indicate to
                          Indicator               the POS the cardholder
                                                  verification methods.
                                                  Valid values are:\
                                                  0 - Failed CVM\
                                                  1 - Signature required\
                                                  2 - PIN required\
                                                  3 - PIN and signature
                                                  required\
                                                  4 -- Not determined.
                                                  POS should request
                                                  signature.
  -----------------------------------------------------------------------

These fields will be sent to the POS for any transaction (EMV or not) in
which a chip (ICC) is present. For more information, see the **Fusebox
EMV Integration Guide** under "Host Request" \> "EMV Elavon Gateway API
Request Changes".

\

Offline Situations {#00039 .h2}
------------------

Simplify supports Stand-In processing for offline situations based on
configured settings; see [Stand-in Processing](#0003) for more
information. When a transaction is processed offline, a
Simplify-generated response message is returned to the POS in field 1010
of the Stand-In Response; see [Simplify-Generated Messages](#0009).

Traditionally EMV tags are not returned in a Stand-In response. Starting
with version 2.02.023, Simplify can be set to return EMV tags to the POS
in Stand-In. This allows the POS to process Store and Forward (deferred
authorization) transactions as EMV.

Other changes to offline processing for EMV: ( 1) If EMV print data is
returned on an offline response, the POS must print the data. (2)
Simplify does not validate the expiration date for offline EMV
transactions.

\

ICC Declines and Simplify Reversal Mode {#00040 .h2}
---------------------------------------

If the ICC chip declines a host-approved transaction, or the customer
removes their card from the chip reader before a host-approved
transaction is completed, the host approval will need to be reversed.

If one of these scenarios occurs, the message in field 1010 will begin
with \*ICC (see [Simplify-Generated Messages](#0009)) and field 26 will
specify the reason for the reversal. 2 = Chip requested decline: 3 =
Premature EMV card removal.

If a host approval needs to be reversed, Simplify will send an EMV
decline of the original transaction to the POS and go into reversal mode
to force a host reversal. In reversal mode, Simplify sends the reversal
(Tran Type 11) to the host, and resends it if necessary, until a
response is received. While this is taking place, any other transactions
sent to the PIN Pad will be processed offline. After Simplify receives
an approval of the reversal, it will return to normal processing mode.

Alternatively, the POS can force Simplify out of reversal mode by
sending an **Exit Reversal Mode** (36-12) message. Simplify will respond
by sending a **Void** **Transaction** **Response** (11) message to the
POS, including the data required to request the reversal. The PIN Pad
will then return to normal processing mode. (If this message is sent and
Simplify is not in reversal mode, it will just echo back the same
message it receives.) See below for format and sample message exchange.

(Simplify can also be forced to exit reversal mode from within the
Elavon Main Menu on the PIN Pad; see the [Simplify Configuration,
Download and Troubleshooting Guide](#support) under "Exiting Reversal
Mode" for details.)

\

**Important**:

\

The following tables provide:

-   A sample of an ICC Chip Decline response.

-   The format of the **Exit Reversal Mode** message.

-   A sample of the **Exit Reversal Mode** / **Void Transaction
    Response** message exchange.

### Sample ICC Chip Decline Response {#sample-icc-chip-decline-response .h3}

Below is a sample response for a **Sale** transaction that was declined
by the ICC:

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,02                             

  0002,3.00                           

  0003,ID:5555396468550434            

  0004,1218                           

  0006,006276                         

  0007,221                            

  0009,001                            

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         

  0014,143339                         

  0017,0                              

  0026,2                              Reason for chip decline (2=Chip
                                      requested decline; 3=Premature EMV
                                      card removal)

  0030,1                              

  0032,022519                         

  0033,173346                         

  0034,M                              

  0035,0707                           

  0036,MCC0110ZU                      

  0037,0                              

  0043,015755                         

  0047,C;1;1;1;0;1;5;0;5;3;3;1;0;4    POS Data Code

  0052,0                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless; 5 =
                                      swiped)

  0054,05                             POS Entry Mode (EMV Tag 9F39)

  0055,1                              PIN Capabilities

  0057,0                              ICC Chip Condition Code

  0061,00                             

  0062,201                            

  0063,00                             

  0109,RETERM1                        

  0110,205                            

  0112,400                            

  0115,010                            

  0125,707213346                      

  0126,2                              

  0129,0                              

  0130,300                            

  0140,USD                            

  0163,en                             Cardholder Language Preference (EMV
                                      Tag 5F2D)

  0651,0000000                        

  1000,MC                             

  1001,MASTERCARD                     

  1002,Test Card 10                   

  1003,264                            

  1005,0010600008014593613999         

  1008,\*\*\*\*\*\*\*\*\*\*\*\*0434   

  1010,\*ICC EMV DECLINED.            

  1012,0774                           

  1200,0000AA                         

  1300,DF60405EFAA61BE6               Application Cryptogram (EMV Tag
                                      9F26)

  1301,D9816C720D4ECD560012           Issuer Authentication Data (EMV Tag
                                      91)

  1302,181231                         Application Expiration Date (EMV
                                      Tag 5F24)

  1303,1F0002                         Cardholder Verification Method
                                      (CVM) Results (EMV Tag 9F34)

  1305,021020100F220\                 Issuer Application Data (EMV Tag
  4000000000\                         9F10)
  00000000000FF                       

  1306,E0F8C8                         Terminal Capabilities (EMV Tag
                                      9F33)

  1307,4200008000                     Terminal Verification Result (TVR)
                                      (EMV Tag 95)

  1312,124                            Terminal Country Code (EMV Tag
                                      9F1A)

  1313,00                             Application PAN Sequence Number
                                      (EMV Tag 5F34)

  1314,A0000000041010                 Dedicated File Name (EMV Tag 84)

  1317,0002                           Terminal Application Version Number
                                      (EMV Tag 9F09)

  1318,00000192                       Transaction Sequence Counter (EMV
                                      Tag 9F41)

  1319,5800                           Application Interchange Profile
                                      (EMV Tag 82)

  1320,0014                           Application Transaction Counter
                                      (ATC) (EMV Tag 9F36)

  1321,00                             Cryptogram Information Data (EMV
                                      Tag 9F27)

  1322,22                             Terminal Type (EMV Tag 9F35)

  1323,E66C0DB5                       Unpredictable Number (EMV Tag 9F37)

  1325,A0000000041010                 ICC Application Identifier (AID)
                                      (EMV Tag 4F)

  1326,MasterCard                     ICC Application Preferred Name (EMV
                                      Tag 9F12)

  1327,MasterCard                     Terminal Application Label (EMV Tag
                                      50)

  1328,A0000000041010                 Terminal Application Identifier
                                      (AID) (EMV Tag 9F06)

  1332,FF00                           Application Usage Control (EMV Tag
                                      9F07)

  1333,06152016                       Last Host EMV Key Download

  1334,E800                           Transaction Status Information (EMV
                                      Tag 9B)

  1339,00                             EMV Response Code (EMV Tag 8A)

  1350,F1                             CA Public Key Index (EMV Tag 8F)

  1357,124                            ICC Transaction Currency (EMV Tag
                                      5F2A)

  1358,00                             Cryptogram Tran Type (EMV Tag 9C)

  1359,4                              EMV CVM Verification Indicator

  1361,0840                           Issuer Currency Code (EMV Tag 5F56)

  1376,00000000000000001F00           CVM List EMV Tag (8E)

  1378,1326\|Application Label:\      EMV Approved Receipt Field List
  ;1300\|TC:;1307\|TVR:\              
  ;1325\|AID: ;                       

  1379,1326\|Application Label:\      EMV Declined Receipt Field List
  ;1300\|AAC: ;1307\|TVR:\            
  ;1325\|AID: ;                       

  1380,CHIP                           POS Entry Receipt Indicator

  4747,04051                          

  5002,70117222                       

  5004,G2                             

  5010,EMVDC0838                      EMV kernel version

  7007,1116189776252145               

  8002,SIMTESTVOLT                    

  8006,TSTLA3                         
  -----------------------------------------------------------------------

\

### **Sample Exit Reversal Mode Message Exchange** {#sample-exit-reversal-mode-message-exchange .h3}

The response to an Exit Reversal Mode (36-12) Request is a Void
Transaction (11) Response:

#### Exit Reversal Mode Request {#exit-reversal-mode-request .h4}

  API Field \#, Value   Description
  --------------------- -----------------------------------------------------------------
  0001,36               Transaction Type
  0007,1                Transaction Amount
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,150258           Transaction time (current time) -- HHMMSS

\

#### Void Transaction Response {#void-transaction-response .h4}

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,11                             Transaction Type

  0002,20.00                          Transaction

  0003,;541333\                       Account Data
  \*\*\*0011=25126\                   
  01MUYytYLBrXYG?                     

  0007,35                             Reference Number

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction date(current date) --
                                      MMDDDYY

  0014,135718                         Transaction time (current time) --
                                      HHMMSS

  0017,0                              Cash Back Amount

  0047,5;1;1;1;0;1;5;1;1;3;\*;C       POS Data Code

  0052,0                              Transponder / Proximity Indicator
                                      (0 = contact; 2 = contactless; 5 =
                                      swiped)

  0054,05                             POS Entry Mode (EMV Tag 9F39)

  0055,9                              PIN Capabilities

  0057,0                              ICC Chip Condition Code

  0109,RETAIL                         Terminal ID

  0110,205                            Cashier ID

  0115,10                             Transaction Qualifier

  0163,EN                             Cardholder Language Preference (EMV
                                      Tag 5F2D)

  1002,MTIP06 MCD 13A                 Cardholder Name

  1300,DD38ED49BCA8EA20               Application Cryptogram (EMV Tag
                                      9F26)

  1302,251231                         Application Expiration Date (EMV
                                      Tag 5F24)

  1303,410302                         Cardholder Verification Method
                                      (CVM) Results (EMV Tag 9F34)

  1305,0210A580\                      Issuer Application Data (EMV Tag
  0F0400000000000\                    9F10)
  00000000000FF                       

  1306,E0F8C8                         Terminal Capabilities (EMV Tag
                                      9F33)

  1307,0000008000                     Terminal Verification Results (TVR)
                                      (EMV Tag 95)

  1312,840                            Terminal Country Code (EMV Tag
                                      9F1A)

  1313,03                             Application PAN Sequence Number
                                      (EMV Tag 5F34)

  1317,0002                           Terminal Application Version Number
                                      (EMV Tag 9F09)

  1318,00000070                       Transaction Sequence Counter (EMV
                                      Tag 9F41)

  1319,3000                           Application Interchange Profile
                                      (EMV Tag 82)

  1320,0027                           Application Transaction Counter
                                      (ATC) (EMV Tag 9F36)

  1321,80                             Cryptogram Information Data (EMV
                                      Tag 9F27)

  1322,22                             Terminal Type (EMV Tag 9F35)

  1323,65058BBD                       Unpredictable Number (EMV Tag 9F37)

  1325,A0000000041010                 ICC Application Identifier (AID)
                                      (EMV Tag 4F)

  1326,MasterCard                     ICC Application Preferred Name (EMV
                                      Tag 9F12)

  1327,MASTERCARD                     Terminal Application Label (EMV Tag
                                      50)

  1328,A0000000041010                 Terminal Application Identifier
                                      (AID) (EMV Tag 9F06)

  1332,FF00                           Application Usage Control (EMV Tag
                                      9F07)

  1334,E800                           Transaction Status Information (EMV
                                      Tag 9B)

  1350,F1                             CA Public Key Index (EMV Tag 8F)

  1354,03                             ICC Public Key Exponent (EMV Tag
                                      9F47)

  1357,840                            ICC Transaction Currency (EMV Tag
                                      5F2A)

  1358,00                             Cryptogram Tran Type (EMV Tag 9C)

  1361,0056                           Issuer Currency Code EMV Tag (5F56)

  1376,000000000000000\               CVM List EMV Tag (8E)
  0410342031E031F00                   

  5002,70045363                       Device Serial Number

  5004,G2                             Encryption Provider ID

  5010,EMVDC0838                      EMV kernel version

  8002,EMVG2                          Location Name (provided by Elavon)

  8006,CHAIN                          Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

\

Sample EMV Sale Message {#00041 .h2}
-----------------------

A sample **Sale Request** and **Sale Response** for an approved EMV
transaction is shown below. Note concerning this sample:

-   The POS request to Simplify does not require modification for EMV.

-   Descriptions are given for response fields added to support EMV.

-   Additional fields, not shown in the samples, may also be sent to the
    POS for EMV.

-   For purposes of reference, EMV tags have been noted for potential
    EMV receipt fields.

### Sample Message {#sample-message .h3}

#### Request {#request-14 .h4}

\

  API Field \#, Value   Description
  --------------------- -------------------------------------------------------------------------------------------------------
  0001,02               
  0002,1.00             
  0007,219              
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           
  0014,143210           
  0017,0.00             
  0109,RETERM1          
  0110,205              
  0201,0.00             
  1008,ID:              
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](#00073).
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](#00073).
  8002,SIMTESTVOLT      
  8006,TSTLA3           

#### Response {#response-15 .h4}

\

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,02                             

  0002,1.00                           

  0003,ID:4979252177090148            

  0004,1217                           

  0006,CVI875                         

  0007,219                            

  0009,001                            

  0011,xxx..                          Field 11 is defined as User Data.
                                      See [Simplify-Controlled Field
                                      Definitions](#00073).

  0013,022519                         

  0014,143214                         

  0017,0                              

  0030,1                              

  0032,022519                         

  0033,173225                         

  0035,2469                           

  0036,116189977545650                

  0037,0                              

  0043,228812                         

  0047,M;1;1;1;0;1;5;1;3;1;3;C;0;4    POS Data Code

  0052,0                              Transponder / Proximity Indicator

  0054,05                             POS Entry Mode (EMV Tag 9F39)

  0055,9                              PIN Capabilities

  0057,0                              ICC Chip Condition Code

  0062,201                            

  0109,RETERM1                        

  0110,205                            

  0112,400                            

  0115,010                            

  0125,707173225                      

  0126,2                              

  0129,1                              

  0130,100                            

  0140,USD                            

  0163,fr                             Cardholder Language Preference (EMV
                                      Tag 5F2D)

  0651,0000000                        

  1000,VI                             

  1001,VISA                           

  1002,CARD 14/VISA TEST              

  1003,0000                           

  1004,APPROVAL                       

  1005,0010600008014593613999         

  1008,\*\*\*\*\*\*\*\*\*\*\*\*0148   

  1009,AA                             

  1010,COMPLETE                       

  1012,0774                           

  1200,0000AA                         

  1300,2AF039B4B32A2DCC               Application Cryptogram (EMV Tag
                                      9F26)

  1301,CD120BA4CDD06DFB0012           Issuer Authentication Data (EMV Tag
                                      91)

  1302,171231                         Application Expiration Date (EMV
                                      Tag 5F24)

  1303,410302                         Cardholder Verification Method
                                      (CVM) Results (EMV Tag 9F34)

  1305,06010A03649C00                 Issuer Application Data (EMV Tag
                                      9F10)

  1306,E0F8C8                         Terminal Capabilities (EMV Tag
                                      9F33)

  1307,8000008000                     Terminal Verification Results (TVR)
                                      (EMV Tag 95)

  1312,124                            Terminal Country Code (EMV Tag
                                      9F1A)

  1313,01                             Application PAN Sequence Number
                                      (EMV Tag 5F34)

  1314,A0000000031010                 Dedicated File Name (EMV Tag 84)

  1315,0001                           ICC Application Version Number (EMV
                                      Tag 9F08)

  1317,008C                           Terminal Application Version Number
                                      (EMV Tag 9F09)

  1318,00000190                       Transaction Sequence Counter (EMV
                                      Tag 9F41)

  1319,1C00                           Application Interchange Profile
                                      (EMV Tag 82)

  1320,05E1                           Application Transaction Counter
                                      (ATC) (EMV Tag 9F36)

  1321,40                             Cryptogram Information Data (EMV
                                      Tag 9F27)

  1322,22                             Terminal Type (EMV Tag 9F35)

  1323,D67895E4                       Unpredictable Number (EMV Tag 9F37)

  1325,A0000000031010                 ICC Application Identifier (AID)
                                      (EMV Tag 4F)

  1326,Credit                         ICC Application Preferred Name (EMV
                                      Tag 9F12)

  1327,VISA TEST                      Terminal Application Label (EMV Tag
                                      50)

  1328,A0000000031010                 Terminal Application Identifier
                                      (AID) (EMV Tag 9F06)

  1332,FF80                           Application Usage Control (EMV Tag
                                      9F07)

  1333,06152016                       Last Host EMV Key Download

  1334,6800                           Transaction Status Information (EMV
                                      Tag 9B)

  1339,00                             EMV Response Code (EMV Tag 8A)

  1357,124                            ICC Transaction Currency (EMV Tag
                                      5F2A)

  1358,00                             Cryptogram Tran Type (EMV Tag 9C)

  1359,2                              EMV CVM Verification Indicator

  1361,0076                           Issuer Currency Code (EMV Tag 5F56)

  1362,100                            EMV Cryptogram Amount

  1363,000                            EMV Cryptogram Other Amount

  1376,00000\                         CVM List (EMV Tag 8E)
  0000000000\                         
  041034203\                          
  1E031F02                            

  1378,1327\|Label Application:\      EMV Approved Receipt Field List
  ;1300\|TC:;1307\|TVR:\              
  ;1325\|AID: ;                       

  1379,1327\|Label Application:\      EMV Declined Receipt Field List
  ;1300\|AAC: ;1307\|TVR:\            
  ;1325\|AID: ;                       

  1380,CHIP                           POS Entry Receipt Indicator

  1382,F000F0A001                     Additional Terminal Capabilities
                                      (EMV Tag 9F40)

  4747,04050                          

  5002,70117222                       

  5004,G2                             

  5010,EMVDC0838                      EMV kernel version

  5070,Merchant: Demo;\               Simplify Information. See
  Simplify: V-OG-2.02.02124;\         [Simplify-Controlled Field
  PARM: 2.21.1;TENDERDEF: 2.21.1;\    Definitions](#00073).
  EMVPARM: EMVPARM-E4-1               

  5071,xxx...                         Defines whether card and cardholder
                                      are present. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  5104,xxx...                         Tip Settings. See
                                      [Simplify-Controlled Field
                                      Definitions](#00073).

  7007,1116189775452137               

  8002,SIMTESTVOLT                    

  8006,TSTLA3                         
  -----------------------------------------------------------------------

\

Pay-At-Table {#0005 .h1}
============

Simplify supports Pay\@Table processing on Ingenico iWLxxx PIN Pads.

Pay\@Table transactions can be broken down into three steps:

1.  **Pre-pay** (Simplify Pay\@Table process) -- Simplify sends a
    **Login Request** to login and connect to the POS. Pay\@Table
    configuration values are received in the response. After determining
    a check for processing, Simplify sends a **Get Check Information
    Request** to the POS and receives data on the specified check(s) in
    the response. Simplify finalizes transaction data for a tender and
    sends a **Make Payment Request** to the POS.

2.  **Authorization** (Simplify Payment process) -- Simplify receives a
    financial request from the POS, obtains customer account data, and
    prepares and sends a host request to Fusebox. Simplify processes the
    host response, and sends a financial response to the POS.

    Supported Tran Types for the financial request are Auth Only (01),
    Sale (02), Return (09). For more information on these Tran Types,
    see [Message Details](#core_concepts) . The POS can also send a
    Void (11) or an Inquiry (22) after a host or Simplify timeout; for
    more information see under **Simplify Payment Processing**.

3.  **Post-pay** (Simplify Pay\@Table process) -- Simplify receives a
    **Print Receipt Request** from the POS, prints the receipts and send
    a **Print Receipt Response** to the POS.

POS responsibilities during a Pay\@Table transaction include the
following:

-   Upon **Login Request**, validates user. If valid login, returns
    **Login Response** based on message specification.

-   Upon **Get Check Information Request**, returns list of open checks.

-   After receipt of **Make Payment Request** (completion of Pay\@Table
    pre-pay process), builds and sends financial request to Simplify.

-   After receiving financial response, sends **Print Receipt Request**
    to Simplify.

-   Handle timeout from financial response, if applicable.

-   Upon **Logout/Disconnect Request**, sends response, logs user out
    and disconnects from PIN Pad.

-   There can be multiple Pay\@Table terminals for a single base. All
    terminals connected to the same base will have the same IP address,
    with the POS responsible for managing multiple sockets.

Message Flow {#00042 .h2}
------------

\

#### Simplify Pay\@Table Process {#simplify-paytable-process .h4}

::: {.mermaid align="center"}
sequenceDiagram participant POS Device participant Simplify
Simplify-\>\>POS Device:Login Request Note left of POS Device:Validates
User Note left of POS Device:Opens Connection Note left of POS
Device:Returns config data POS Device-\>\>Simplify:Login Response Note
right of Simplify:Selects Table/\
optional Group\
(Full Service)\
or Check (Quick\
Service) Note right of Simplify:Sends selection Simplify-\>\>POS
Device:Get Check Info Request POS Device-\>\>Simplify:Get Check Info
Response
:::

#### Simplify Payment Process {#simplify-payment-process .h4}

::: {.mermaid align="center"}
sequenceDiagram participant POS Device participant Simplify participant
Fusebox Note left of POS Device:Builds and sends\
financial request POS Device-\>\>Simplify:Inquiry Request
Simplify-\>\>Fusebox:Host Request Note right of Fusebox:Obtains\
authorization Fusebox-\>\>Simplify:Host Reponse Simplify-\>\>POS
Device:Inquiry Response Note left of POS Device:Processes financial\
response (or goes\
to timeout\
processing, see\
next block)
:::

#### Simplify Payment Process (timeout on financial request) {#simplify-payment-process-timeout-on-financial-request .h4}

::: {.mermaid align="center"}
sequenceDiagram participant POS Device participant Simplify participant
Fusebox Note left of POS Device:Can be performed\
on this channel\
or on a\
back channel. POS Device-\>\>Simplify:Inquiry Request
Simplify-\>\>Fusebox:Host Request Note right of Fusebox:Informational\
Response Fusebox-\>\>Simplify:Host Reponse Simplify-\>\>POS
Device:Inquiry Response Note left of POS Device:If no financial\
response or host\
timeout,\
sends inquiry. If\
no response or host\
timeout, resends or\
performs\
[Stand-in processing.](#0003)
:::

#### Simplify Pay\@Table Process {#simplify-paytable-process-1 .h4}

::: {.mermaid align="center"}
sequenceDiagram participant POS Device participant Simplify POS
Device-\>\>Simplify:Print receipt Request Note right of Simplify:Prints
receipts Note right of Simplify:Returns Response Simplify-\>\>POS
Device:Print reciept Response Simplify-\>\>POS Device:Logout Request POS
Device-\>\>Simplify:Logout Response Note left of POS Device:Sends
response Note left of POS Device:Logs user out Note left of POS
Device:Clears connection
:::

Transaction Flow {#00043 .h2}
----------------

::: {.mermaid align="center"}
graph TD A(Send Login request) A \--\> B(Obtain Table/Optional Group
Number) B \--\> D(Get Check Info Request) D \--\> C{Number of Checks in
reponse} C \--\> \|0\| G(Send Logout/Disconnect Request) C \--\> \|1\|
E\[Get Tip amount\] C \--\> \|\>1\| F\[Select check\] F \--\> E E \--\>
H\[Confirm transaction amount\] H \--\> I(Recieive financial request) I
\--\> J\[Obtain customer account data\] J \--\> K(Build & send host
request) K \--\> M(Recieve Host Response) M \--\> L(Build & send
financial request) L \--\> N\[Print Reciepts\] N \--\> O(Send Print
Receipt Response) O \--\> P{Server done?} P \--\> \|No\| B P \--\>
\|Yes\| G
:::

Field Formats and Description {#00044 .h2}
-----------------------------

The following table gives formats/descriptions for all fields included
in Simplify Pay\@Table messages.

**Note:** Data Type = C refers to currency fields. These fields must
include an explicit decimal point.

  -----------------------------------------------------------------------------------
  **Field**      **Field Name** **Size**       **Data Type**  **Description**
  **\#**                                                      
  -------------- -------------- -------------- -------------- -----------------------
  0001           Transaction    2              N              Simplify Tran Type.\
                 Type                                         Always 39 for
                                                              Pay\@Table messages.

  0002           Transaction    1-14           C              Total transaction
                 Amount                                       amount (includes Tip if
                                                              any).\
                                                              The decimal point will
                                                              be explicitly included
                                                              as part of the data.

  0141           Currency Code  3              N              840=USD

  0201           Tip Amount     1-14           C              Entered or selected by
                                                              customer.\
                                                              The decimal point is
                                                              explicitly included in
                                                              the data. Note that the
                                                              POS must send this
                                                              value separately in
                                                              field 201 of the
                                                              financial request.

  5002           Device Serial  1-20           A/N            PIN Pad serial number
                 Number                                       

  5100           Message Type   2              A/N            01=Login\
                                                              02=Get Check Info\
                                                              04=Logout/Disconnect\
                                                              05=Make Payment\
                                                              06=Print Receipt

  5101           Store ID       1-25           A/N            Optional field; may be
                                                              blank or missing\
                                                              Only populated if a
                                                              Store ID is defined
                                                              under Simplify
                                                              configuration.

  5102           Employee ID    1-20           A/N            Server ID

  5103           Service Type   1              N              Controls Simplify
                 Flag                                         prompt displayed on the
                                                              Get Check Information
                                                              screen:\
                                                              00=Table and Check
                                                              Number\
                                                              01=Check Number

  5104           Tip            1-8            A/N            Contains up to three
                 Percentages                                  one or two-digit
                                                              percentages separated
                                                              by semicolons (;)\
                                                              The percentage sign is
                                                              assumed.

  5105           Table Number   1-25           A/N            Entered at prompt

  5106           Check Number   1-25           A/N            Entered at prompt or
                                                              selected from list

  5107           Merchant       1-2047         A/N            Data for merchant
                 Receipt                                      receipt.\
                                                              Receipt lines are
                                                              separated by the pound
                                                              sign (\#). E.g. \#\#
                                                              tells Simplify to print
                                                              a blank line before
                                                              beginning the next
                                                              line.\
                                                              Receipt lines are
                                                              printed using left
                                                              justification. For
                                                              center justification,
                                                              pad with spaces.\
                                                              Note on Font Size: this
                                                              is controlled by
                                                              Simplify in the **Print
                                                              Receipt Request**. See
                                                              **Print Receipt
                                                              Message** for more
                                                              information.

  5108           Customer       1-2047         A/N            Data for customer
                 Receipt                                      receipt. Same format as
                                                              5107.

  5110           POS Response   2              N              Response Code from
                 Code                                         POS:\
                                                              00=approved\
                                                              Any other
                                                              value=declined.

  5111           POS Response   1-50           A/N            Response Message from
                 Message                                      POS.\
                                                              Displayed on PIN Pad.

  5114           Check          1-2047         A/N            Check Information sent
                 Information                                  in five subfields
                                                              (separated by
                                                              semicolons)\
                                                              - Check number. (25
                                                              bytes maximum)\
                                                              - Amount due (includes
                                                              explicit decimal point;
                                                              if negative, the check
                                                              is a refund) (14 bytes
                                                              maximum)\
                                                              - Check receipt (5
                                                              bytes maximun)\
                                                              - Employee ID (10 bytes
                                                              maximum)\
                                                              - Text data (30 bytes
                                                              maximum)\
                                                              See under Get Check
                                                              Information Message for
                                                              more information.

  ...            Check          1-2047         A/N            Information for each
                 Information                                  check is sent in a
                                                              separate field. Up to
                                                              99 checks can be
                                                              processed per table or
                                                              group, using fields
                                                              5114 through 5212.

  5213           Partial        1              N              0=Disabled; 1=Enabled
                 Payment Flag                                 

  5214           Tip Flag       1              N              0=Disabled; 1=Enabled

  5216           Group Number   1-2            N              Entered at prompt
                                                              (optional)

  5217           Type of        2              N              Simplify Tran Type that
                 Transaction                                  should be sent by the
                                                              POS:\
                                                              01=Auth Only\
                                                              02=Sale\
                                                              09=Return (will be sent
                                                              if the check is a
                                                              refund)

  5218           Pay\@Table     1-8            N              Message number
                 Message\                                     incremented for each
                 Reference                                    Pay\@Table request
                 Number                                       (from Simplify or POS)
                                                              and returned in each
                                                              response message (if
                                                              any). Used to match
                                                              requests and
                                                              responses.\
                                                              For **Print Receipt**
                                                              messages, the Reference
                                                              Number must match field
                                                              7 in the preceding
                                                              financial response.

  5219           Pay\@Table     1-8            N              Used if necessary to
                 Session ID                                   recover the correct
                                                              session. Sent in
                                                              **Login Response** and
                                                              all subsequent messages
                                                              until
                                                              logout/disconnect.
                                                              Incremented for each
                                                              **Login Response**.
  -----------------------------------------------------------------------------------

\

Message Summary {#00045 .h2}
---------------

All messages sent and received by the Simplify Pay\@Table process have
39 as the Transaction Type (field 1) and use a Message Type (field 5100)
to define the purpose of the message.

The message sequence used during a Simplify Pay\@Table transaction is as
follows:

The following pages show formats/descriptions for fields used in
Simplify Pay\@Table messages, followed by transaction flow details with
sample messages.

\

  -----------------------------------------------------------------------
  **Pay\@Table Message    **Use**                 **Direction**
  Type**                                          
  ----------------------- ----------------------- -----------------------
  01                      Simplify Pay\@Table     Request from Simplify
                          Process\                to POS\
                          Login Request/Response  Response from POS to
                                                  Simplify

  02                      Get Check Info          Request from Simplify
                          Request/Response        to POS\
                                                  Response from POS to
                                                  Simplify

  05                      Make payment request    Request from Simplify
                                                  to POS\
                                                  No Response message

  N/A                     Simplify Payment        Simplify recieives
                          Process                 financial request from
                                                  POS (Trans Type 01, 02,
                                                  or 09), obtains
                                                  customer account data,
                                                  builds and sends host
                                                  request to Fusebox,
                                                  receives host response,
                                                  and sends financial
                                                  response to POS. No
                                                  Pay\@Table-specific
                                                  processing. See
                                                  Chapters 2-4 for
                                                  details

  06                      Print Receipt           Request from Simplify
                          Request/Response        to POS\
                                                  Response from POS to
                                                  Simplify

  04                      Logout/Disconnect       Request from Simplify
                          Request/Response        to POS\
                                                  Response from POS to
                                                  Simplify
  -----------------------------------------------------------------------

\

Message and Flow Details {#00046 .h2}
------------------------

The following pages provide information on Pay at Table (39-xx) message
types, as follows:

-   The role of the message type in the Pay at Table transaction flow is
    described.

-   The message format is defined, and illustrated with one or more
    sample messages.

\

Login Request and Response (Tran Type 39-01) {#00047 .h2}
--------------------------------------------

Simplify sends a **Login Request** message to the POS after the server
logs in to the PIN Pad. The POS attempts to validate the user and open a
connection.

If login is successful, the **Login Response** from the POS will contain
store configuration values used by Simplify to control Pay\@Table
processing for the transaction (Service Type, Tip Percentages, Partial
Payment Flag, Tip Flag).

### Login Request {#login-request .h3}

A sample **Login Request** message is as follows:

  API Field \#, Value   Description
  --------------------- -------------------------------------
  0001,39               Transaction Type
  5101,12345            Store ID
  5100,01               Message Type
  5102,111              Employee ID
  5002,80667259         Device Serial Number
  5218,713              Pay\@Table Message Reference Number

### Login Response {#login-response .h3}

A sample **Login Response** message is as follows:

  API Field \#, Value   Description
  --------------------- --------------------------------------------------------------------
  0001,39               Transaction Type
  5100,01               Message Type
  5103,00               Service Type
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](#00073).
  5110,00               POS Response Code
  5111,Approved         POS Response Message
  5213,1                Partial Payment Flag
  5214,1                Tip Flag
  5218,713              Pay\@Table Message Reference Number
  5219,12345678         Pay\@Table Session ID

\

Get Check Info Request and Response (Tran Type 39-02) {#00048 .h2}
-----------------------------------------------------

The **Get Check Information Request** is used to request check data from
the POS. Depending on configuration, Simplify can request check
information by table number, check number or group number.

The **Get Check Information Response** returns a list of open checks.
Open checks can be presented as check numbers or as text descriptions
controlled by the POS.

### Get Check Info Request {#get-check-info-request .h3}

A sample **Get Check Info Request** message is as follows:

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,39                             Transaction Type

  5100,02                             Message Type

  5106,1 and/or\                      Check Number and/or Table Number
  5105,1 and/or\                      and/or Group Number.\
  5216,1                              See next table for details.

  5218,714                            Pay\@Table Message Reference Number

  5219,12345678                       Pay\@Table Session ID
  -----------------------------------------------------------------------

#### Controlling Returned Check Data {#controlling-returned-check-data .h4}

The following fields in the **Get Check Info Request** can be used to
control the check(s) for which data will be returned. The field(s) used
for a transaction will depend on values returned in the **Login
Response** (which control Simplify prompting) and on server input, as
follows:

  -----------------------------------------------------------------------
  API Field \#            Contents                Use
  ----------------------- ----------------------- -----------------------
  5105                    Table Number            Used in request if
                                                  prompted for and
                                                  entered.\
                                                  Defines a single table
                                                  for which check data
                                                  will be requested.

  5106                    Check Number            Used in request if
                                                  prompted for and
                                                  entered.\
                                                  Requests data for a
                                                  single check.

  5216                    Group Number            This field is available
                                                  for implementations
                                                  that choose to use it.
  -----------------------------------------------------------------------

\

### Get Check Info Response {#get-check-info-response .h3}

The **Get Check Information Response** contains check data for Simplify
to display. As illustrated by the following samples, Simplify handling
of data for a check is based on whether the corresponding Check
Information field contains valid Text Data (fifth subfield; see next
table):

-   If yes, the Text Data will be displayed and other subfields will be
    ignored.

-   If no, the values in the other subfields will be displayed.

\

  ----------------------------------------------------------------------------
  Field \#       Field Name     Size           Data Type      Description
  -------------- -------------- -------------- -------------- ----------------
  5114\          Check          1-2047         A/N            Check
  5212           Information\                                 Information sent
                 (can be                                      in five
                 repeated up to                               subfields
                 99 times)                                    (separated by
                                                              semi-colons):\
                                                              - Check number.
                                                              (25 bytes
                                                              maximum)\
                                                              - Amount due
                                                              (includes
                                                              explicit decimal
                                                              point; if
                                                              negative, the
                                                              check is a
                                                              refund) (14
                                                              bytes maximum)\
                                                              - Check receipt
                                                              (5 bytes
                                                              maximum)\
                                                              - Employee ID
                                                              (10 bytes
                                                              maximum)\
                                                              - Text data (30
                                                              bytes maximum)

  ----------------------------------------------------------------------------

\

### Sample Messages and Screens {#sample-messages-and-screens .h3}

The following scenarios are distinguished by the type of data (if any)
present in the Text Data subfield of Check Information fields (API
5114-5212) in the **Get Check Information Response** message. For each
scenario, a sample response is shown, followed by the Simplify screen
resulting from this message:

#### No Text Data {#no-text-data .h4}

  API Field \#, Value           Description
  ----------------------------- -------------------------------------
  0001,39                       Transaction Type
  5100,02                       Message Type
  5110,00                       POS Response Code
  5111,Approved                 POS Response Message
  5114,25; \$1.00;22;LCOLE;     Check Information 1
  5115,26; \$2.00;22;JOANNE;    Check Information 2
  5116,1112;\$3.00;12;JEREMY;   Check Information 3
  5218,714                      Pay\@Table Message Reference Number
  5219,12345678                 Pay\@Table Session ID

\

#### Text Data (Check Number, Amount Due, Check Description) {#text-data-check-number-amount-due-check-description .h4}

  API Field \#, Value                                     Description
  ------------------------------------------------------- -------------------------------------
  0001,39                                                 Transaction Type
  5100,02                                                 Message Type
  5110,00                                                 POS Response Code
  5111,Approved                                           POS Response Message
  5114,25; \$1.00;22;LCOLE;\#25 \$1.00 Seat 25;           Check Information 1
  5115,26; \$2.00;22;JOANNE;\#26 \$2.00 Man with cigar;   Check Information 2
  5116,112;\$3.00;12;JEREMY;\#112 \$3.00 Green jacket;    Check Information 3
  5218,714                                                Pay\@Table Message Reference Number
  5219,12345678                                           Pay\@Table Session ID

\

#### Text Data (Check Description only) {#text-data-check-description-only .h4}

  API Field \#, Value                                Description
  -------------------------------------------------- -------------------------------------
  20001,39                                           Transaction Type
  5100,02                                            Message Type
  5110,00                                            POS Response Code
  5111,Approved                                      POS Response Message
  5114,25; \$1.00;22;LCOLE;Guest in Seat 25;         Check Information 1
  5115,26; \$2.00;22;JOANNE;Man with cigar;          Check Information 2
  5116,112;\$3.00;12;JEREMY;Guest in green jacket;   Check Information 3
  5218,714                                           Pay\@Table Message Reference Number
  5219,12345678                                      Pay\@Table Session ID

\

Make Payment Request (Tran Type 39-05) {#00049 .h2}
--------------------------------------

A **Make Payment Request** message is sent by Simplify after transaction
information has been entered for a check (or part of a check if partial
payment is enabled and selected by the customer) and the customer has
approved the transaction amount.

There is no **Make Payment Response** message. The POS responds to a
**Make Payment Request** by sending a financial request to Simplify.

### Make Payment Request {#make-payment-request .h3}

A sample **Make Payment Request** message is as follows:

  API Field \#, Value   Description
  --------------------- -------------------------------------
  0001,39               Transaction Type
  5100,05               Message Type
  5105,1                Table Number
  5106,125              Check Number
  5217,01               Type of Transaction
  0002,14.00            Transaction Amount.
  0201,1.99             Tip Amount
  0141,840              Currency Code
  5218,715              Pay\@Table Message Reference Number
  5219,12345678         Pay\@Table Session ID

\

Simplify Payment Process {#00050 .h2}
------------------------

After the Simplify Pay\@Table process sends a **Make Payment Request**,
the next steps in processing a Pay\@Table transaction are performed by
the Simplify Payment process. For supported Tran Types, this processing
is identical to that performed by Simplify for non-Pay\@Table
transactions:

1.  The POS builds and sends a financial request to Simplify.

2.  Simplify display screens to obtain customer account data (including
    PIN if debit).

3.  Simplify builds and sends the host request to Fusebox.

4.  Fusebox attempts to obtain transaction authorization and sends the
    host response to Simplify.

5.  Simplify processes the host response, and builds and sends a
    financial response to the POS.

The type of financial request that the POS should send is determined by
the Type of Transaction field (5217) that it receives in the **Make
Payment Request**. If the value in this field is 01, the POS should send
an **Auth Only Request**. (As always, if an **Auth Only Request** is
sent, a Completion transaction will also need to be performed.) If the
value is 02, a **Sales Request** should be sent, and if 09, a **Return
Request**.

Stand-In is supported for Pay\@Table transactions using current rules
(as defined under [Stand-in Processing](#0003)). Cashback is *not*
supported on Pay\@Table transactions.

Print Receipt Request and Response (Tran Type 39-06) {#00051 .h2}
----------------------------------------------------

After the Simplify Payment process sends the financial response, control
of the PIN Pad is returned to the Simplify Pay\@Table process.

After receiving a financial response from Simplify for a Pay\@Table
transaction, the POS sends a **Print Receipt Request** message to
Simplify. This request contains data needed by Simplify to print the
receipts. After receiving this request, Simplify will print the Merchant
receipt followed by the Customer receipt.

After printing the receipts, Simplify will send a **Print Receipt
Response** message to the POS. This completes Simplify processing for
the tender.

### Print Receipt Request {#print-receipt-request .h3}

A sample **Print Receipt Request** message is as follows:

  -------------------------------------------------------------------------------------
  API Field \#, Value                               Description
  ------------------------------------------------- -----------------------------------
  0001,39                                           Transaction Type

  5100,06                                           Message Type

  5110,00                                           POS Response Code

  5111,Approved                                     POS Response Message

  5107,RECEIPT DATA IS SENT FROM THE POS\           Merchant Receipt
  \#Elavon Demo Restaurant\                         
  \#4234 Hacienda Drive Suite 250\                  
  \#Pleasanton Ca 94588\                            
  \#\                                               
  \#Merchant Copy\                                  
  \#\                                               
  \#Merchant ID :123456789012345\                   
  \#Terminal ID : RETERM1\                          
  \#Card No. : \*\*\*\*\*\*\*\*\*\*\*\*1111\        
  \#Expiry Date: XX/XX\                             
  \#Card Type : VI\                                 
  \#Trans Type : SALE\                              
  \#Trans Time : 09/18/2015 16:06:55\               
  \#Trace No. : 2\                                  
  \#RRN :100161000312\                              
  \#Auth Code : 000052\                             
  \#\                                               
  \#App Label :Personal Account\                    
  \#AID : A000000025010801\                         
  \#AC :52A80ACE8E0D9CA4\                           
  \#\                                               
  \#AMOUNT :USD \$14.00\                            
  \#APPROVAL\                                       
  \#\                                               
  \# I agree to the terms of my\                    
  \# credit agreement.\                             
  \#\                                               
  \#\                                               
  \#\                                               
  \#\                                               
  \#--------------------------------------------\   
  \# Signature.\                                    
  \[Line breaks added for readability.\]            

  5108,Elavon Demo Restaurant\                      Customer Receipt
  \#4234 Hacienda Drive Suite 250\                  
  \#Pleasanton Ca 94588\                            
  \#\                                               
  \# Customer Copy\                                 
  \#\                                               
  \#Merchant ID : 9795818996\                       
  \#Terminal ID : RETERM1\                          
  \#Card No. : \*\*\*\*\*\*\*\*\*\*\*\*1111\        
  \#Expiry Date: XX/XX\                             
  \#Card Type : VISA\                               
  \#Trans Type : SALE\                              
  \#Trans Time : 09/18/2015 16:06:55\               
  \#Trace No. : refnum.\                            
  \#RRN : 100161000312\                             
  \#Auth Code : 000052\                             
  \#\                                               
  \#App Label: Personal Account\                    
  \#AID : A000000025010801\                         
  \#AC : 52A80ACE8E0D9CA4\                          
  \#\                                               
  \#AMOUNT : USD14.00\                              
  \#APPROVAL\                                       
  \#\                                               
  \# I agree to the terms of my\                    
  \# credit agreement.\                             
  \#\                                               
  \#\                                               
  \#\                                               
  \#\                                               
  \#------------------------------------------\     
  \# Signature.\                                    
  \[Line breaks added for readability.\]            

  5218,21                                           Pay\@Table Message Reference Number

  5219,12345678                                     Pay\@Table Session ID
  -------------------------------------------------------------------------------------

\

### Print Receipt Response {#print-receipt-response .h3}

A sample Print Receipt Response message is as follows:

  API Field \#, Value   Description
  --------------------- -------------------------------------
  0001,39               Transaction Type
  5100,06               Message Type
  5110,00               Fusebox Response Code
  5111,Success          Fusebox Response Message
  5218,11               Pay\@Table Message Reference Number
  5219,12345678         Pay\@Table Session ID

\

### Sample Receipt {#sample-receipt .h3}

A sample merchant receipt is shown below:

\

Logout/Disconnect Request and Response (Tran Type 39-04) {#00052 .h2}
--------------------------------------------------------

After printing the receipts, Simplify will check whether there is a
remaining balance on the check or (if Full Service) whether the table or
group still has open checks.

-   If yes, Simplify will resend the **Get Check Information Request**
    and repeat the processing steps through the **Print Receipt
    Response**.

-   If no, Simplify will send a **Logout/Disconnect Request** to the
    POS. The POS responds by sending a Logout/Disconnect Response,
    logging out the user and disconnecting from the PIN Pad.

### Logout/Disconnect Request {#logout-disconnect-request .h3}

A sample **Logout/Disconnect Request** message is as follows:

  **API Field \#, Value**   **Description**
  ------------------------- -------------------------------------
  0001,39                   Transaction Type
  5002,80667323             Device Serial Number
  5100,04                   Message Type
  5102,2                    Employee ID
  5218,1826                 Pay\@Table Message Reference Number
  5219,11                   Pay\@Table Session ID

### Logout/Disconnect Response {#logout-disconnect-response .h3}

A sample **Logout/Disconnect Response** message is as follows:

  **API Field \#, Value**   **Description**
  ------------------------- -------------------------------------
  0001,39                   Transaction Type
  5100,04                   Message Type
  5110,00                   POS Response Code
  5111,Approved             POS Response Message
  5218,1826                 Pay\@Table Message Reference Number
  5219,11                   Pay\@Table Session ID

\

Recovery {#00053 .h2}
--------

### General Principles {#general-principles .h3}

<!-- -->

<!-- -->

<!-- -->

<!-- -->

<!-- -->

### Simplify Recovery Points and Actions {#simplify-recovery-points-and-actions .h3}

  **State**               **Message**                     Expected Response                                              **Recover State on Timeout**   **Action on Timeout/Dropped Socket**
  ----------------------- ------------------------------- -------------------------------------------------------------- ------------------------------ --------------------------------------
  Idle                                                    Idle                                                           Idle                           Idle
  Login/Connect           Login Request                   Login Response                                                 Login/Connect                  Close and create new socket
  Get Check Information   Get Check Information Request   Get Check Information Response                                 Get Check Information          Close and create new socket
  Make Payment Request    Make Payment Request            financial request                                              Get Check Information          Close and create new socket
  Financial Request       Same process as current         Same process as current                                        Get Check Information          Close and create new socket
  Receipt Printing        Print Receipt Request           Print Receipt Response                                         Receipt printing               Wait for new socket
  Logout/Disconnect       Logout/Disconnect Request       Logout/Disconnect Response, User logged out, POS disconnects   Idle                           Close socket

\

#### POS Recovery {#pos-recovery .h4}

If a timeout or other communication error occurs while waiting for a
financial response, the POS can send an **Inquiry Request** (22) using
current rules (as defined under [Inquiry Message](#00016).

#### Mini Receipt {#mini-receipt .h4}

If Simplify does not receive a **Print Receipt Request** before timing
out, it will not know whether the transaction was successfully posted.
In this case, Simplify will print a mini receipt like the following
sample:

Mini Receipt:

<!-- -->

<!-- -->

This receipt tells the server that Simplify has lost communications with
the POS after sending the financial response for the indicated
transaction. The server will need to find out from the POS what it has
done with the transaction.

Informational Prompting {#0006 .h1}
=======================

Simplify supports an **Informational Prompt Message**. This is a
flexible feature designed to allow merchants to display information for
customers and get customer input using a variety of screen layouts. This
message type does not affect the processing of financial transactions.

The POS controls this process by sending an **Informational Prompt
Request** that defines the screen to be displayed. The PIN Pad must be
in a Closed state to process this request. Exceptions: (1) If another
**Informational Prompt Request** is sent when the PIN Pad is already
displaying an Informational Prompt screen, the display for the second
request will replace the first screen. (2) After sending an
**Informational Prompt Response**, the PIN Pad will display a wait
screen for a configurable interval before going to the Closed state. If
a new **Informational Prompt Request** is sent during this interval, the
PIN Pad will process the request.

Simplify returns the customer input in the **Informational Prompt
Response**. Input includes the action button (virtual button) or hard
key pressed. Depending on the type of **Informational Prompt Message**
sent, input may also include entered text or a selected radio button,
check boxes or slider position. Additional requests can be sent if
further customer interaction is required.

### Generic Non-Financial Message Format {#generic-non-financial-message-format .h3}

The **Informational Prompt Message** is a **Non-Financial** message type
(Transaction Type 36) with a Message Type of 14. It is discussed
separately in this chapter due to its many uses.

As described in Chapter 2 under [Non-Financial Messages](#00021), all
**Non-Financial** messages have the following generic format:

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type 36. Non-Financial
                                      message

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).\
                                      For Transaction Type 36, it will
                                      always include:\
                                      Positions 1-2 Message Type

  5001,xxx..                          Non-Financial Data.\
                                      The format of this field depends on
                                      the value of Message Type.
  -----------------------------------------------------------------------

\

### Fields 11 and 5001 in Informational Prompt Messages {#fields-11-and-5001-in-informational-prompt-messages .h3}

The remainder of this page provides information on fields 11 and 5001
specific to the **Informational Prompt Message**.

#### Field 11 {#field-11 .h4}

The format of field 11 in the **Informational Prompt Message** (36-14)
is modeled on that in the **Signature Request** and **Response
Messages** (36-01, 36-02). Exception: the **Screen ID** subfield of
field 11 is not used. As shown in the following table, the Response
echoes the Request except for the Timeout Value, which is replaced with
the Completion Code.

  -----------------------------------------------------------------------
  Field 11 Subfield       Length                  Description
  ----------------------- ----------------------- -----------------------
  Message Type            2                       Always 14

  Sequence Number         3                       Transaction identifier

  Screen ID               3                       Not used

  Timeout Value/          3                       Request: Screen timeout
  Completion Code                                 in seconds (000=No
                                                  timeout)\
                                                  Response: Completion
                                                  Code (000 = Success)
                                                  See
                                                  [Simplify-Controlled
                                                  Field
                                                  Definitions](#00073).

  VersionBuildInfo        Var                     Response only: '?'
                                                  followed by Version and
                                                  Build numbers
  -----------------------------------------------------------------------

#### Field 5001 {#field-5001 .h4}

In the **Informational Prompt Message**, field 5001 is used in the
Request to define the screen that will be displayed and in the Response
to return customer action/data entered. The generic structure of Field
5001 is TTTLLLVVV..VV, broken down as follows:

+-----------------------+-----------------------+-----------------------+
| Field 5001 Subfield   | Length                | Description           |
+=======================+=======================+=======================+
| TTT                   | 3                     | Tag identifying       |
|                       |                       | screen to be          |
|                       |                       | displayed:            |
+-----------------------+-----------------------+-----------------------+
| LLL                   | 3                     | Length of data        |
|                       |                       | (VVV...VV)\           |
|                       |                       | Note that if the data |
|                       |                       | is longer than 999    |
|                       |                       | bytes, set LLL to     |
|                       |                       | 999. The application  |
|                       |                       | will process the      |
|                       |                       | additional data.      |
+-----------------------+-----------------------+-----------------------+
| VVV...VV              | var                   | Data                  |
+-----------------------+-----------------------+-----------------------+

The following pages provide detailed breakdowns of Field 5001 and sample
messages for each supported value of Tag.

\

Tag 010 - Text with Optional Buttons {#00054 .h2}
------------------------------------

The **Text with Optional Buttons Message** is used to display virtual
buttons and/or fixed text onscreen. The screen may have button(s) on top
(and/or bottom on some models) plus labels (lines of text) below and/or
above any buttons.

A virtual button will only be displayed if data is entered in the
descriptor field (ButtonNDesc) for the button. Note that pressing the
Enter key is not required after pressing a virtual button.

The following details are device-specific:

**For iSC250 and iSC480** -- Screen may have button(s) on top and/or
bottom plus labels (lines of text) in the middle. The maximum number of
labels depends on the buttons present. The maximum is 6 if there are
button(s) on the top and bottom, 7 if there are button(s) on the top or
bottom but not both, and 8 if there are no buttons. *Do not send excess
labels.* The maximum length of each Button Descriptor is 10. The maximum
length of each Button Label is 52 for the iSC250 and 62 for the iSC480.

**For iPP350** -- Buttons on top of the screen are not supported; up to
four buttons are supported on the bottom. Up to six labels are
supported. The maximum length of each Button Descriptor is 7. The
maximum length of each Button Label is 43.

The **Text with Optional Buttons Response** returns the button pressed
by the customer. Fields in the Request (AllowEnter, AllowCancel) control
whether the (hard) Enter and Cancel keys can be used.

### Field 5001 Format {#field-5001-format-4 .h3}

#### Request {#request-15 .h4}

  -------------------------------------------------------------------------------
  Field 5001 Subfield     Length                  Description
  ----------------------- ----------------------- -------------------------------
  TTT                     3                       Tag (always = 010)

  LLL                     3                       Length of the following data

  AllowEnter              1                       Allow Enter hard key (0=Not
                                                  allow, 1=Allow)

  AllowCancel             1                       Allow Cancel hard key (0=Not
                                                  allow, 1=Allow)

  Beeper                  1                       Sound tone (0=No, 1=Yes)

  ButtonADesc             0 (iPP350)\             Descriptor for first button
                          0-10\                   position (from left) on top (A)
                          (iSCxxx)                

  FS                      1                       Field separator (Hex 1C)

  ButtonBDesc             0 (iPP350)\             Descriptor/field separator for
                          0-10\                   second button position on top
                          (iSCxxx)                (B)

  FS                      1                       

  ButtonCDesc             0 (iPP350)\             Descriptor/field separator for
                          0-10\                   third button position on top ©
                          (iSCxxx)                

  FS                      1                       

  ButtonDDesc             0 (iPP350)\             Descriptor/field separator for
                          0-10\                   fourth button position on top
                          (iSCxxx)                (D)

  FS                      1                       

  ButtonEDesc             0-7 (iPP350)\           Descriptor/field separator for
                          0-10\                   first button position (from
                          (iSCxxx)                left) on bottom (E)

  FS                      1                       

  ButtonFDesc             0-7 (iPP350)\           Descriptor/field separator for
                          0-10\                   second button position on
                          (iSCxxx)                bottom (F)

  FS                      1                       

  ButtonGDesc             0-7 (iPP350)\           Descriptor/field separator for
                          0-10\                   third button position on bottom
                          (iSCxxx)                (G)

  FS                      1                       

  ButtonHDesc             0-7 (iPP350)\           Descriptor/field separator for
                          0-10\                   fourth button position on
                          (iSCxxx)                bottom (H)

  FS                      1                       

  Label1Just              1                       Label 1 Justification (1=Left
                                                  justify, 2=Center, 3=Right
                                                  justify)

  Label1Reverse           1                       Reverse mode (0=standard mode,
                                                  1=reverse mode).

  Label1Text              0-43 (iPP350)\          Label 1 Text
                          0-52 (iSC250)\          
                          0-62 (iSC480)           

  FS                      1                       Field separator (Hex 1C)

  Label2Just              1                       Justification/mode/text/field
                                                  separator for Label 2.

  Label2Reverse           1                       

  Label2Text              0-43 (iPP350)\          
                          0-52 (iSC250)\          
                          0-62 (iSC480)           

  FS                      1                       

  Label3Just              1                       Justification/mode/text/field
                                                  separator for Label 3.

  Label3Reverse           1                       

  Label3Text              0-43 (iPP350)\          
                          (iSC250)\               
                          (iSC480)                

  FS                      1                       

  Label4Just              1                       Justification/mode/text/field
                                                  separator for Label 4.

  Label4Reverse           1                       

  Label4Text              0-43 (iPP350)\          
                          0-52 (iSC250)\          
                          0-62 (iSC480)           

  FS                      1                       

  Label5Just              1                       Justification/mode/text/field
                                                  separator for Label 5.

  Label5Reverse           1                       

  Label5Text              0-43 (iPP350)\          
                          0-52 (iSC250)\          
                          0-62 (iSC480)           

  FS                      1                       

  Label6Just              1                       Justification/mode/text/field
                                                  separator for Label 6.

  Label6Reverse           1                       

  Label6Text              0-43 (iPP350)\          
                          0-52 (iSC250)\          
                          0-62 (iSC480)           

  FS                      1                       

  Label7Just              1                       Justification/mode/text/field
                                                  separator for Label 7.

  Label7Reverse           1                       

  Label7Text              0 (iPP350)\             
                          0-52 (iSC250)\          
                          0-62 (iSC480)           

  FS                      1                       

  Label8Just              1                       Justification/mode/text for
                                                  Label 8.

  Label8Reverse           1                       

  Label8Text              0 (iPP350)\             
                          0-52 (iSC250)\          
                          0-62 (iSC480)           
  -------------------------------------------------------------------------------

#### Response {#response-16 .h4}

+-----------------------+-----------------------+-----------------------+
| Field Name            | Length                | Description           |
+=======================+=======================+=======================+
| TTT                   | 3                     | Tag (always = 010)    |
+-----------------------+-----------------------+-----------------------+
| LLL                   | 3                     | Length of the         |
|                       |                       | following data        |
+-----------------------+-----------------------+-----------------------+
| ActionButton          | var                   | If field 11           |
|                       |                       | Completion Code = 000 |
|                       |                       | (success), returns    |
|                       |                       | code for action       |
|                       |                       | button or key         |
|                       |                       | pressed:              |
+-----------------------+-----------------------+-----------------------+

### Sample Message (One Button) {#sample-message-one-button .h3}

#### Request {#request-16 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14123010120                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

5001,010276111FSButton 2FSFSFSFSFSFSFS10Thisline is left justified in
normal mode 52 charsFS20This second line should be centeredFS30This
third line is right justifiedFS21This line should be in reverse
modeFS20This fifth line should be back in normal modeFS10This is line
6left justifyFS10This is line 7 left justify

#### Response {#response-17 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14123010000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#0006){.highlight}.  |
+-----------------------------------+-----------------------------------+
| 5001,0100038880                   | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

### Sample Message (Eight Buttons) {#sample-message-eight-buttons .h3}

#### Request {#request-17 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14123010120                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

#### Response {#response-18 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14123010000                  | User Data                         |
+-----------------------------------+-----------------------------------+
| 5001,0100011                      | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

Tag 011 - Static and Scrolling Text with Optional Buttons {#00055 .h2}
---------------------------------------------------------

The **Static and Scrolling** **Text with Optional Buttons Message** can
be used to display both static (non-scrolling) and scrolling user text
on the same screen, as well as optional buttons. Buttons and static text
and scrolling text are placed in three screen areas, whose heights can
be configured (0 = do not display). These areas are, from top to bottom:

Button area -- Up to four virtual buttons can be displayed at the top of
the screen. As for Tag 010, a virtual button will only be displayed if
data is entered in the request descriptor field for the button
(ButtonNDesc). The vertical extent of this area is defined (as a
percentage of screen height) by a request field; 20(%) is recommended.
Buttons are centered in the button area. Button descriptor font size is
defined by a request field (see samples below). Maximum descriptor
length is 10.

Static text area -- The vertical extent of this area is defined (as a
percentage of screen height) by a request field. Other request fields
define the font size and justification of static text.

Scrolling text area -- The vertical extent of this area is whatever is
left over after the first two areas. Other request fields define the
font size and justification of scrolling text.

For both text areas: See below for sample font sizes. The maximum number
of characters per line depends on the font size. E.g. 60 upper case
characters can be displayed using font size=1, 55 using font size=2 and
44 using font size=3. The maximum number of lines in an area depends on
the height of the area and the font size used. E.g. if the static text
area height is 40(%), up to 5 lines can be displayed for font size = 1,
and up to 4 lines for either 2 or 3.

Pressing the Enter key is not required after pressing a virtual button.

The **Static and Scrolling Text with Optional Buttons Response** returns
the button pressed by the customer. Request fields (AllowEnter,
AllowCancel) control whether the (hard) Enter and Cancel keys can be
used.

Not supported on the iPP.

### Field 5001 Format {#field-5001-format-5 .h3}

#### Response {#response-19 .h4}

  Field 5001 Subfield     Length        Description
  ----------------------- ------------- ------------------------------------------------------------------
  TTT                     3             Tag (always = 011)
  LLL                     3             Length of the following data
  AllowEnter              1             Allow Enter hard key (0=Not allow, 1=Allow)
  AllowCancel             1             Allow Cancel hard key (0=Not allow, 1=Allow)
  Beeper                  1             Sound tone (0=No, 1=Yes)
  FS                      1             Field separator (Hex 1C)
  ButtonAreaHeight        2             Height of Button area (as % of screen height)
  FS                      1             Field separator (Hex 1C)
  ButtonFontSize          1             Button descriptor font size (0 = extra small to 6 = extra large)
  FS                      1             Field separator (Hex 1C)
  ButtonADesc             0-10          Descriptor for first button position (from left) on top (A)
  FS                      1             Field separator (Hex 1C)
  ButtonBDesc             0-10          Descriptor for second button position on top (B)
  FS                      1             Field separator (Hex 1C)
  ButtonCDesc             0-10          Descriptor for third button position on top ©
  FS                      1             Field separator (Hex 1C)
  ButtonDDesc             0-10          Descriptor for fourth button position on top (D)
  FS                      1             Field separator (Hex 1C)
  StaticTextAreaHeight    2             Height of Static text area (as % of screen height)
  FS                      1             Field separator (Hex 1C)
  StaticTextFontSize      1             Static text font size (0 = extra small to 6 = extra large)
  FS                      1             Field separator (Hex 1C)
  StaticTextJust          1             Static text justification (1=Left; 2=Center; 3=Right)
  FS                      1             Field separator (Hex 1C)
  StaticText              (see above)   Static text defined in semi-colon (;) delimited lines
  FS                      1             Field separator (Hex 1C)
  ScrollingTextFontSize   1             Scrolling text font size (0 = extra small to 6 = extra large)
  FS                      1             Field separator (Hex 1C)
  ScrollingTextJust       1             Scrolling text justification (1=Left; 2=Center; 3=Right)
  FS                      1             Field separator (Hex 1C)
  ScrollingText1          (see above)   First line of scrolling text
  FS                      1             Field separator (Hex 1C)
  ScrollingTextLast       (see above)   Last line of scrolling text

#### Request {#request-18 .h4}

+-----------------------+-----------------------+-----------------------+
| Field 5001 Subfield   | Length                | Description           |
+=======================+=======================+=======================+
| TTT                   | 3                     | Tag (always = 011)    |
+-----------------------+-----------------------+-----------------------+
| LLL                   | 3                     | Length of the         |
|                       |                       | following data        |
+-----------------------+-----------------------+-----------------------+
| ActionButton          | var                   | If field 11           |
|                       |                       | Completion Code = 000 |
|                       |                       | (success), returns    |
|                       |                       | code for action       |
|                       |                       | button or key         |
|                       |                       | pressed:              |
+-----------------------+-----------------------+-----------------------+

### Sample Message (Four Buttons) {#sample-message-four-buttons .h3}

#### Request {#request-19 .h4}

The following request tells Simplify to display the screen shown below
(start of scrolling text is shown):

API Field \#, Value

Description

0001,36

Transaction Type

0011,14123010120

User Data. See [Simplify-Controlled Field Definitions](#00073).

5001

See value below

011

Tag

934

Length of data

1

Allow Enter key

1

Allow Cancel key

1

Beeper active

20

Height (%) of Button area

3

Button descriptor font size

Button 1

Descriptor for virtual button position A

40

Height (%) of static text area\
3=Static text font size

3

Static text font size

2

Static text justification

Text1

Text of static line 1

;

Delimiter for text of static line 1

2

Scrolling text font size

2

Scrolling text justification

Text of scrolling line 1

You agree that any Services contain proprietary content,information

#### Response {#response-20 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14123011000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,0110003777                   | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

\

### Sample Message (Two Buttons) {#sample-message-two-buttons .h3}

#### Request {#request-20 .h4}

The following request tells Simplify to display the screen shown below
(start of scrolling text is shown):

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14124011000                    User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,\[see value below\]            Non-Financial Data011=Tag\
                                      899=Length of data\
                                      1=Allow Enter key\
                                      1=Allow Cancel key\
                                      1=Beeper active\
                                      20=Height (%) of Button area\
                                      3=Button descriptor font size\
                                      Button 1=Descriptor for virtual
                                      button position A\
                                      (etc.)\
                                      10=Height (%) of static text area\
                                      2=Static text font size\
                                      2=Static text justification\
                                      Text1=Text of static line 1\
                                      2=Scrolling text font size\
                                      2=Scrolling text justification\
                                      You agree that any Services contain
                                      proprietary content,
                                      information=Text of scrolling line
                                      1\
                                      and material that is protected by
                                      applicable intellectual property
                                      =Text of scrolling line 2\
                                      (etc.)
  -----------------------------------------------------------------------

#### Response {#response-21 .h4}

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14123011000                    User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,0110003888                     Non-Financial Data\
                                      011=Tag\
                                      003=Length of data\
                                      888=Cancel key pressed
  -----------------------------------------------------------------------

Tag 012 - Text and Graphics with Optional Buttons {#00056 .h2}
-------------------------------------------------

The **Text and Graphics with Optional Buttons Message** can be used to
display static (non-scrolling) user text and graphics, as well as
optional buttons. Buttons and static text and graphics are placed in
three screen areas, whose heights can be configured (0 = do not
display). These areas are, from top to bottom:

Button area -- IDENTICAL TO 011 -- Up to four virtual buttons can be
displayed at the top of the screen. As for Tag 010, a virtual button
will only be displayed if data is entered in the request descriptor
field for the button (ButtonNDesc). The vertical extent of this area is
defined (as a percentage of screen height) by a request field; 20(%) is
recommended. Buttons are centered in the button area. Button descriptor
font size is defined by a request field (see samples below). Maximum
descriptor length is 10.

Static text area -- IDENTICAL TO 011 -- The vertical extent of this area
is defined (as a percentage of screen height) by a request field. Other
request fields define the font size and justification of static text
(see samples below). The maximum number of characters per line depends
on the font size. E.g. 60 upper case characters can be displayed using
font size=1, 55 using font size=2 and 44 using font size=3. The maximum
number of lines of static text depends on the height of the area and the
font size used. E.g. if the static text area height is 40(%), up to 5
lines can be displayed for font size = 1 and up to 4 lines for font size
2 or 3 (see samples below).

Graphics area -- The vertical extent of this area is whatever is left
over from the first two areas. It can contain up to two graphics side by
side.

Pressing the Enter key is not required after pressing a virtual button.

The **Text and Graphics with Optional Buttons Response** returns the
button pressed by the customer. Request fields (AllowEnter, AllowCancel)
control whether the (hard) Enter and Cancel keys can be used.

Not supported on the iPP.

### Field 5001 Format {#field-5001-format-6 .h3}

#### **Request** {#request-21 .h4}

::: {.notices .note}
::: {.body-text}
\*\*Note:\*\* Field separators must be sent for both button and label
fields as shown below, even if some of these fields are null.
:::
:::

\

  Field 5001 Subfield   Length        Description
  --------------------- ------------- ------------------------------------------------------------------
  TTT                   3             Tag (always = 012)
  LLL                   3             Length of the following data
  AllowEnter            1             Allow Enter hard key (0=Not allow, 1=Allow)
  AllowCancel           1             Allow Cancel hard key (0=Not allow, 1=Allow)
  Beeper                1             Sound tone (0=No, 1=Yes)
  FS                    1             Field separator (Hex 1C)
  ButtonAreaHeight      2             Height of Button area (as % of screen height)
  FS                    1             Field separator (Hex 1C)
  ButtonFontSize        1             Button descriptor font size (0 = extra small to 6 = extra large)
  FS                    1             Field separator (Hex 1C)
  ButtonADesc           0-10          Descriptor for first button position (from left) on top (A)
  FS                    1             Field separator (Hex 1C)
  ButtonBDesc           0-10          Descriptor for second button position on top (B)
  FS                    1             Field separator (Hex 1C)
  ButtonCDesc           0-10          Descriptor for third button position on top ©
  FS                    1             Field separator (Hex 1C)
  ButtonDDesc           0-10          Descriptor for fourth button position on top (D)
  FS                    1             Field separator (Hex 1C)
  TextAreaHeight        2             Height of text area (as % of screen height)
  FS                    1             Field separator (Hex 1C)
  TextFontSize          1             Text font size (0 = extra small to 6 = extra large)
  FS                    1             Field separator (Hex 1C)
  TextJust              1             Text justification (1=Left; 2=Center; 3=Right)
  FS                    1             Field separator (Hex 1C)
  Text                  (see above)   Text defined in semi-colon (;) delimited lines
  FS                    1             Field separator (Hex 1C)
  Image1                variable      First image
  FS                    1             Field separator (Hex 1C)
  Image2                variable      Second image

#### Response {#response-22 .h4}

  -----------------------------------------------------------------------
  Field 5001 Subfield     Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     3                       Tag (always = 012)

  LLL                     3                       Length of the following
                                                  data

  ActionButton            var                     If field 11 Completion
                                                  Code = 000 (success),
                                                  returns code for action
                                                  button or key pressed:\
                                                  777=Enter (green) key\
                                                  888=Cancel (red) key\
                                                  1=ButtonA\
                                                  2=ButtonB\
                                                  3=ButtonC\
                                                  4=ButtonD
  -----------------------------------------------------------------------

\

### Sample Message (Four Buttons) {#sample-message-four-buttons-1 .h3}

#### Request {#request-22 .h4}

The following request tells Simplify to display the screen shown below:

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14125012000                    User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,\[see value below\]            Non-Financial Data\
                                      012=Tag\
                                      092=Length of data\
                                      1=Allow Enter key\
                                      1=Allow Cancel key\
                                      1=Beeper active\
                                      20=Height (%) of Button area\
                                      3=Button descriptor font size\
                                      Button 1=Descriptor for virtual
                                      button position A\
                                      (etc.)\
                                      40=Height (%) of text area\
                                      3=Text font size\
                                      2=Text justification\
                                      Text1;=Text and delimiter of line
                                      1\
                                      (etc.)\
                                      LOGO.PNG=First (left) image\
                                      TAP.PNG=Second (right) image
  -----------------------------------------------------------------------

#### Response {#response-23 .h4}

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14125012000                    User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,0120003777                     Non-Financial Data\
                                      012=Tag\
                                      003=Length of data\
                                      777=Enter key pressed
  -----------------------------------------------------------------------

### Sample Message (Two Buttons) {#sample-message-two-buttons-1 .h3}

#### Request {#request-23 .h4}

The following request tells Simplify to display the screen shown below:

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14125012000                    User Data. See [Simplify-Controlled
                                      Field Definitions](h#0006).

  5001,\[see value below\]            Non-Financial Data\
                                      012=Tag\
                                      057=Length of data\
                                      1=Allow Enter key\
                                      1=Allow Cancel key\
                                      1=Beeper active\
                                      20=Height (%) of Button area\
                                      3=Button descriptor font size\
                                      Button 1=Descriptor for virtual
                                      button position A\
                                      (etc.)\
                                      25=Height (%) of text area\
                                      2=Text font size\
                                      2=Text justification\
                                      Text 1=Text of line 1\
                                      LOGO.PNG=First (left) image\
                                      TAP.PNG=Second (right) image
  -----------------------------------------------------------------------

#### Response {#response-24 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125012000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,0120003888                   | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

Tag 020 - Scrolling Text {#00057 .h2}
------------------------

The Scrolling Text Message is used to display scrolling text onscreen.
Up to 100 lines of scrolling text are supported.

The Scrolling Text Response returns whether the customer pressed the
Enter (green) or Cancel (red) key.

Not supported on the iPP.

###  {#section .Field .5001 .Format}

#### Request {#request-24 .h4}

  Field Name   Length   Description
  ------------ -------- ----------------------------------------
  TTT          3        Tag (always = 020)
  LLL          3        Length of the following data
  Beeper       1        Sound tone (0=No, 1=Yes)
  Info1        1-48     Information 1
  FS           1        Field separator (Hex 1C)
  Info2        1-48     Text/field separator for Information 2
  FS           1        
  Info3        1-48     Text/field separator for Information 3
  FS           1        
  Info4        1-48     Text/field separator for Information 4
  FS           1        
  Info5        1-48     Text/field separator for Information 5
  FS           1        
  Info6        1-48     Text/field separator for Information 6
  FS           1        
  ...          .        ...
  Info100      1-48     Information 100

#### Response {#response-25 .h4}

+-----------------------+-----------------------+-----------------------+
| Field Name            | Length                | Description           |
+=======================+=======================+=======================+
| TTT                   | 3                     | Tag (always = 020)    |
+-----------------------+-----------------------+-----------------------+
| LLL                   | 3                     | Length of the         |
|                       |                       | following data        |
+-----------------------+-----------------------+-----------------------+
| ActionButton          | 3                     | If field 11           |
|                       |                       | Completion Code = 000 |
|                       |                       | (success), returns    |
|                       |                       | code for key pressed  |
|                       |                       | by customer:          |
+-----------------------+-----------------------+-----------------------+

### Sample Message {#sample-message-1 .h3}

The following request tells Simplify to display the screen shown below:

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125020000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

#### Response {#response-26 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125020000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,020003777                    | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

#### Additional Samples (field 5001) {#additional-samples-field-5001 .h4}

  Value in Field 5001                                              Screen Use
  ---------------------------------------------------------------- --------------------------
  030049Enter AmountFSFSFS0 FS/d/d/d/d/d/d/d/d/d/d/D./D/D US\$FS   Prompt for dollar amount
  030041Enter Date (YYMMDD)FSFSFS0FS/d/d///d/d///d/dFS             Prompt for date
  030039Enter Time (HHMMSS)FSFSFS0FS/d/d:/d/d:/d/dFS               Prompt for time
  030036Enter PasswordFSFSFS1FS/c/c/c/c/c/c/c/cFS                  Prompt for password

#### Tag 040 - Radio Buttons {#tag-040---radio-buttons .h2}

Simplify supports a **Radio Buttons Message**. The Request displays a
screen with up to 100 radio buttons and up to three lines of text. The
customer can select one radio button. A field in the Request (Required)
determines whether the Enter key is accepted when no radio button is
selected.

One field in the **Radio Buttons Response** (ActionButton) will indicate
whether Enter or Cancel was pressed. If the customer presses the Enter
key, another field (Data) indicates the radio button selected by the
customer (if any).

Not supported on the iPP.

### Field 5001 Format {#field-5001-format-7 .h3}

#### Request {#request-25 .h4}

  Field Name   Length   Description
  ------------ -------- ------------------------------------------------------
  TTT          3        Tag (always = 040)
  LLL          3        Length of the following data
  Required     1        Data is required when ENTER is pressed (0=No, 1=Yes)
  FS           1        Field separator (Hex 1C)
  Title1       0-48     Title 1
  FS           1        Field separator (Hex 1C)
  Title2       0-48     text/field separator for Title 2
  FS           1        
  Title3       0-48     text/field separator for Title 3
  FS           1        
  Choice1      0-40     Choice 1
  FS           1        Field separator (Hex 1C)
  Choice2      0-40     button text/field separator for Choice 2
  FS           1        
  Choice3      0-40     button text/field separator for Choice 3
  FS           1        
  Choice4      0-40     button text/field separator for Choice 4
  FS           1        
  Choice5      0-40     button text/field separator for Choice 5
  FS           1        
  Choice6      0-40     button text/field separator for Choice 6
  FS           1        
  ...          .        ...
  Choice100    0-40     Choice 100

#### Response {#response-27 .h4}

  -----------------------------------------------------------------------
  Field Name              Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     3                       Tag (always = 040)

  LLL                     3                       Length of the following
                                                  data

  ActionButton            3                       If field 11 Completion
                                                  Code = 000 (success),
                                                  returns code for key
                                                  pressed by customer:\
                                                  777=Enter (green) key\
                                                  888=Cancel (red) key

  FS                      1                       Field separator (Hex
                                                  1C)

  Data                    var                     If ActionButton = 777
                                                  (Enter), returns
                                                  selected item using
                                                  index of 1 to nn(=
                                                  number of selections).
  -----------------------------------------------------------------------

### Sample Message {#sample-message-2 .h3}

#### Request {#request-26 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125040000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

#### Response {#response-28 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125040000?V102.18B01803    | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,040006777FS100               | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

Tag 050 - Check Boxes {#00058 .h2}
---------------------

Simplify supports a **Check Boxes Message**. The Request displays a
screen with up to 100 check boxes and up to three lines of text. The
customer can select one or more check boxes. A field in the Request
(Required) determines whether the Enter key is accepted when no check
box is selected. With the exception of the Tag value, the format of this
request is identical to that for Tag 040.

One field in the **Check Boxes Response** (ActionButton) will indicate
whether Enter or Cancel was pressed. If Enter was pressed, another field
(Data) will indicate the check box(es) selected by the customer (if
any). Not supported on the iPP.

### Field 5001 Format {#field-5001-format-8 .h3}

#### Request {#request-27 .h4}

\

Field Name

Length

Description

TTT

3

Tag (always = 050)

LLL

3

Length of the following data

Required

1

Data is required when ENTER is pressed (0=No, 1=Yes)

FS

1

Field separator (Hex 1C)

Title1

0-48

Title 1

FS

1

Field separator (Hex 1C)

Title2

0-48

text/field separator for Title 2

FS

1

Title3

0-48

text/field separator for Title 3

FS

1

Choice1

0-40

Choice 1\
Field separator (Hex 1C)

FS

1

Choice2

0-40

button text/field separator for Choice 2

FS

1

Choice3

0-40

button text/field separator for Choice 3

FS

1

Choice4

0-40

button text/field separator for Choice 4

FS

1

Choice5

0-40

button text/field separator for Choice 5

FS

1

Choice6

0-40

button text/field separator for Choice 6

FS

1

...

.

...

Choice100

0-40

Choice 100

#### Response {#response-29 .h4}

  -----------------------------------------------------------------------
  Field Name              Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     3                       Tag (always = 050)

  LLL                     3                       Length of the following
                                                  data

  ActionButton            3                       If field 11 Completion
                                                  Code = 000 (success),
                                                  returns code for key
                                                  pressed by customer:\
                                                  777=Enter (green) key\
                                                  888=Cancel (red) key

  FS                      1                       Field separator (Hex
                                                  1C)

  Data                    var                     If ActionButton = 777
                                                  (Enter), returns
                                                  selected check boxes
                                                  (if any).\
                                                  Each check box is
                                                  represented as either 0
                                                  (not selected) or 1
                                                  (selected).
  -----------------------------------------------------------------------

### Sample Message {#sample-message-3 .h3}

#### Request {#request-28 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125050000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
|                                   |                                   |
|                                   | <!-- -->                          |
|                                   |                                   |
|                                   | <!-- -->                          |
|                                   |                                   |
|                                   | <!-- -->                          |
|                                   |                                   |
|                                   | <!-- -->                          |
+-----------------------------------+-----------------------------------+

#### Response {#response-30 .h4}

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14125050000?V102.18B01803      User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,050017777FS10101000000000      Non-Financial Data\
                                      050=Tag017=Length of data\
                                      777=Enter key pressed\
                                      1010100000000=Check boxes 1, 3 and
                                      5 selected
  -----------------------------------------------------------------------

Tag 060 - Slider Message {#00059 .h2}
------------------------

Simplify supports a **Slider Message**. The Request displays a screen
with up to three lines of text and an adjustable slider.

One field in the Response (ActionButton) indicates whether Enter or
Cancel was pressed. If the customer presses Enter, another field (Data)
indicates the customer-selected position of the slider.

Not supported on the iPP.

### Field 5001 Format {#field-5001-format-9 .h3}

#### Request {#request-29 .h4}

  Field Name   Length   Description
  ------------ -------- ------------------------------------------------------
  TTT          3        Tag (always = 060)
  LLL          3        Length of the following data
  Msg1         0-50     Message 1
  FS           1        Field separator (Hex 1C)
  Msg2         0-50     Message 2
  FS           1        Field separator (Hex 1C)
  Msg3         0-50     Message 3
  FS           1        Field separator (Hex 1C)
  MinValue     var      Minimum Value to start (e.g. 0)
  FS           1        Field separator (Hex 1C)
  MaxValue     var      Maximum Value to end (e.g. 100)
  FS           1        Field separator (Hex 1C)
  Increment    var      Incremental steps of the slider (e.g. 5)
  FS           1        Field separator (Hex 1C)
  Initial      var      Initial Value of the slider (e.g. 0 = start at zero)
  FS           1        Field separator (Hex 1C)
  ProgLabel    var      Text label for the progress of the slide (e.g. %)

#### Response {#response-31 .h4}

  -----------------------------------------------------------------------
  Field Name              Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     3                       Tag (always = 060)

  LLL                     3                       Length of the following
                                                  data

  ActionButton            3                       If field 11 Completion
                                                  Code = 000 (success),
                                                  returns code for key
                                                  pressed by customer:\
                                                  777=Enter (green) key\
                                                  888=Cancel (red) key

  FS                      1                       Field separator (Hex
                                                  1C)

  Data                    var                     If ActionButton = 777
                                                  (Enter), returns
                                                  selected position of
                                                  the slider as a Percent
                                                  (%).
  -----------------------------------------------------------------------

### **Sample Message** {#sample-message-4 .h3}

#### Request {#request-30 .h4}

The following request tells Simplify to display the screen shown below:

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125060060                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

#### **Response** {#response-32 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125060000?V102.18B01803    | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,060006777FS650               | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

Tag 070 - Scrolling Text with Radio Buttons {#00060 .h2}
-------------------------------------------

Simplify supports a **Scrolling Text with Radio Buttons Message**. This
Tag can be used to display a Consent screen. The Request displays a
screen with up to 2 radio buttons and up to 100 lines or text through
which the customer can scroll. A field in the Request (Required)
determines whether the Enter key is accepted when no radio button is
selected.

**Device details** -- The maximum length of radio button text is 40
characters for the iSC250 and 43 for the iSC480. The maximum length of
text lines (Info fields) is 47 characters for the iSC250 and 49 for the
iSC480. Not supported on the iPP.

One field in the Response (ActionButton) indicates whether Enter or
Cancel was pressed. Another field (Data)indicates the radio button
selected by the customer (if any).

### Field 5001 Format {#field-5001-format-10 .h3}

#### Request {#request-31 .h4}

  -----------------------------------------------------------------------
  Field Name              Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     3                       Tag (always = 070)

  LLL                     3                       Length of the following
                                                  data

  Required                1                       Data is required when
                                                  ENTER is pressed (0=No,
                                                  1=Yes)

  FS                      1                       Field separator (Hex
                                                  1C)

  Radio1                  0-40 (iSC250)\          Radio button1 text
                          0-43 (iSC480)           (left justified).

  FS                      1                       Field separator (Hex
                                                  1C)

  Radio2                  0-40 (iSC250)\          Radio button2 text
                          0-43 (iSC480)           (left justified)

  FS                      1                       Field separator (Hex
                                                  1C)

  InfoJust                1                       Justification for all
                                                  Information fields
                                                  (1=Left justify,
                                                  2=Center, 3=Right
                                                  justify)

  FS                      1                       Field separator (Hex
                                                  1C)

  Info1                   0-47 (iSC250)\          Information 1 (left
                          0-49 (iSC480)           justified)

  FS                      1                       Field separator (Hex
                                                  1C)

  Info2                   0-47 (iSC250)\          Text/field separator
                          0-49 (iSC480)           for Information 2

  FS                      1                       

  Info3                   0-47 (iSC250)\          Text/field separator
                          0-49 (iSC480)           for Information 3

  FS                      1                       

  Info4                   0-47 (iSC250)\          Text/field separator
                          0-49 (iSC480)           for Information 4

  FS                      1                       

  Info5                   0-47 (iSC250)\          Text/field separator
                          0-49 (iSC480)           for Information 5

  FS                      1                       

  Info6                   0-47 (iSC250)\          Text/field separator
                          0-49 (iSC480)           for Information 6

  FS                      1                       

  ...                     .                       ...

  Info100                 0-47 (iSC250)\          Information 100
                          0-49 (iSC480)           
  -----------------------------------------------------------------------

#### Response {#response-33 .h4}

  -----------------------------------------------------------------------
  Field Name              Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     8                       Tag (always = 070 )

  LLL                     3                       Length of the following
                                                  data

  ActionButton            3                       If field 11 Completion
                                                  Code = 000 (success),
                                                  returns code for key
                                                  pressed:\
                                                  777=Enter hard key
                                                  pressed\
                                                  888=Cancel hard key
                                                  pressed

  FS                      1                       Field separator (Hex
                                                  1C)

  Data                    1                       If ActionButton=777,
                                                  returns selected radio
                                                  button, if any (1 = top
                                                  button, 2= bottom
                                                  button)
  -----------------------------------------------------------------------

### Sample Message {#sample-message-5 .h3}

#### Request {#request-32 .h4}

The following request tells Simplify to display the screen shown below
(start and end of scrolling text are shown):

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125070000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

#### Response {#response-34 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125070000?V102.18B01803    | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,070005777FS10                | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

Tag 071 - Scrolling Text with Virtual Buttons {#00061 .h2}
---------------------------------------------

Simplify supports a **Scrolling Text with Virtual Buttons Message**. The
Request displays a screen with scrolling text plus virtual buttons at
the bottom of the screen. This message can be used to display a Consent
screen.

Scrolling text -- Up to 100 lines of scrolling text can be defined. Font
size and justification are defined in the request. The maximum number of
characters per line depends on the font size. E.g. 60 upper case
characters can be displayed using font size=1, 55 using font size=2 and
44 using font size=3.

Buttons -- Up to two virtual buttons can be defined. The maximum length
of the button descriptors depends on the font size defined in the
request. E.g. for font size =3, each descriptor can be up than 20
characters in length.

One field in the Response (ActionButton) indicates which action button
or key was pressed (Cancel, Virtual button 1, Virtual button 2) was
pressed. Another field (Data) indicates the virtual button selected by
the customer (if any).

Not supported on the iPP.

### Field 5001 Format {#field-5001-format-11 .h3}

#### **Request** {#request-33 .h4}

  Field Name       Length        Description
  ---------------- ------------- ---------------------------------------------------------------
  TTT              3             Tag (always = 071)
  LLL              3             Length of the following data
  ButtonSize       1             Font size of virtual buttons (0=extra small to 6=extra large)
  FS               1             Field separator (Hex 1C)
  VirtualButton1   (see above)   Virtual button1 text (left justified).
  FS               1             Field separator (Hex 1C)
  VirtualButton2   (see above)   Virtual button2 text (left justified)
  FS               1             Field separator (Hex 1C)
  InfoFontSize     1             Font size for Info fields (0=extra small to 6=extra large)
  FS               1             Field separator
  FS               1             Field separator (Hex 1C)
  Info1            (see above)   Text for Information 1 (left justified)
  FS               1             Field separator (Hex 1C)
  Info2            (see above)   Text for Information 2
  FS               1             Field separator
  Info3            (see above)   Text for Information 3
  FS               1             Field separator
  Info4            (see above)   Text for Information 4
  FS               1             Field separator
  Info5            (see above)   Text for Information 5
  FS               1             Field separator
  Info6            (see above)   Text for Information 6
  FS               1             Field separator
  ...              .             ...
  Info100          (see above)   Text for Information 100

#### **Response** {#response-35 .h4}

  -----------------------------------------------------------------------
  Field Name              Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     8                       Tag (always = 071 )

  LLL                     3                       Length of the following
                                                  data

  ActionButton            3                       If field 11 Completion
                                                  Code = 000 (success),
                                                  returns code for key
                                                  pressed:\
                                                  1=Virtual button 1
                                                  (button on left)
                                                  pressed\
                                                  2=Virtual button 2
                                                  (button on right)
                                                  pressed\
                                                  888=Cancel hard key
                                                  pressed

  FS                      1                       Field separator (Hex
                                                  1C)

  Data                    1                       Returns selected
                                                  virtual button, if any
                                                  (1 = left button, 2=
                                                  right button)
  -----------------------------------------------------------------------

### Sample Message {#sample-message-6 .h3}

#### **Request** {#request-34 .h4}

The following request tells Simplify to display the screen shown below
(note that bottom of scrolling screen is shown):

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125071000                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,\[see value below\]          | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

#### **Response** {#response-36 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14125071000?V102.18B01803    | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](#00073).             |
+-----------------------------------+-----------------------------------+
| 5001,071005777FS1                 | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

Dynamic Currency Conversion (DCC) {#0007 .h1}
=================================

Dynamic Currency Conversion (DCC) allows customers with eligible cards
to pay in the base currency of the card. Simplify has modified
processing for Sale (02) and Auth Only (01) transactions to support DCC.
Other Tran Types are not eligible for DCC. Supported terminal types are
iPP3xx, iSC250, iSC480, iSMP4 and all Tetra devices.

(Note that if the POS builds a Financial Request using a converted
currency, Simplify will pass through the converted currency.)

Simplify supports a DCC Inquiry Message from the POS. This is a
non-financial message used to support DCC processing. If Simplify
receives this message, it will send it as a pass through message to
Fusebox (see below for message sample).

Simplify will process a Sale or Auth Only transaction using DCC if the
following conditions are met:

1.  Field 169 is sent in the Financial Request and set to 1, and the
    request does not include a token.

    (Possible values of Field 169 are as follows: 0 = not DCC-capable; 1
    = DCC-capable/enabled; 2 = DCC-capable/not enabled. 3 =
    DCC-capable/enabled, but merchant opted for no DCC on this
    transaction.)

2.  The card is DCC-eligible.

3.  The customer approves currency conversion when prompted at the PIN
    Pad ("customer Opt-In").

If Simplify processes a transaction using DCC, the Financial Response to
the POS will include DCC information from Fusebox. For more information
on DCC fields, see the **Fusebox DCC Integration Guide**.

### Sample Message {#sample-message-7 .h3}

#### Request {#request-35 .h4}

The following table shows a sample DCC Inquiry Request sent from the POS
to Fusebox via Simplify:

  API Field \#, Value        Description
  -------------------------- -----------------------------------------------------------------
  0001,46                    Transaction Type
  0002,1.00                  Transaction Amount
  0003,ID:5915537177642302   Account Number (token)
  0007,65                    Transaction ID / Reference Number
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                Transaction Date (current date)-- MMDDYY
  0014,014500                Transaction Time (current time) -- HHMMSS
  0017,0.00                  Cash Back Amount
  0109,DCC250                Terminal ID (provided by Elavon)
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = Credit; 030 -- Debit)
  **0169,1**                 **Merchant PMS/POS DCC Capability**
  0201,0.00                  Tip Amount
  5002,80005652              Device Serial Number
  5004,G2                    Encryption Provider ID
  8002,LDG                   Location Name (provided by Elavon)
  8006,AGILYS                Chain Code (provided by Elavon)

#### Response {#response-37 .h4}

The following table shows a sample DCC Inquiry Response sent from
Fusebox to the POS via Simplify:

  API Field \#, Value                 Description
  ----------------------------------- ----------------------------------------------------------------------------------
  0001,46                             Transaction Type
  0002,1.00                           Transaction Amount
  0003,ID:5915537177642302            Account Data (token)
  0007,65                             Transaction ID / Reference Number
  0009,001                            Fusebox -- Host Batch number
  0011,xxx..                          User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519                         Transaction Date (current date) -- MMDDYY
  0014,014500                         Transaction Time (current time) -- HHMMSS
  0017,0.00                           Cash Back Amount
  0030,1                              Fusebox -- Online Indicator
  0032,022519                         Fusebox -- Authorization Transaction Date
  0033,164529                         Fusebox -- Authorization Transaction Time
  0037,0                              Fusebox -- Authorizer
  0043,000000                         System Trace Audit Number
  0047,C;1;1;1;0;1;1;0;5;1;3;1;0;4    POS Data Code
  0052,5                              Transponder / Proximity Indicator (0 = contactless; 2 = contactless, 5 = swiped)
  0061,00                             Terminal Type
  0063,00                             CAT Indicator
  0109,DCC250                         Terminal ID
  0110,205                            Cashier ID
  0112,400                            Fusebox -- Processor ID
  0115,010                            Transaction Qualifier (010 = credit; 030 = debit)
  0126,0                              Track Indicator (may need to appear on receipt)
  0140,USD                            Merchant Currency
  0142,GBP                            Cardholder Currency
  0144,0.72                           Converted Amount
  **0150,71953**                      **DCC Rate**
  **0159,5**                          **DCC Exponent**
  0163,en                             Cardholder Language Preference (EMV Tag 5F2D)
  **0165,0550**                       **DCC Markup Percentage**
  **0166,US Bank**                    **DCC Rate Provider Name**
  **0169,1**                          **Merchant PMS/POS DCC Indicator**
  0201,0.00                           Tip Amount
  0307,1                              Duration of Stay
  1000,MasterCard                     Card Type
  1001,MASTERCARD                     Card Name
  1003,0000                           Gateway Response Code
  1004,APPROVAL                       Host Response Message
  1005,0010600008024724760542         Merchant Number
  1008,\*\*\*\*\*\*\*\*\*\*\*\*2302   Masked Account Number (for printing on receipt)
  1009,AA                             Host Response Code
  1010,COMPLETE                       Gateway Response Message
  1012,0021                           Gateway Batch Number
  1200,0000AA                         Issuer Network Information
  4747,04020                          Third Party Interface POS Data Code
  5002,80005652                       Device Serial Number
  5004,G2                             Encryption Provider ID
  5010,EMVDC0838                      EMV kernel version
  **7007,1116147747290484**           **Transaction Link Identifier. (Required for DCC transactions)**
  8002,LEADING                        Location Name
  8006,AGILYS                         Chain Code

Point to Point Encryption (P2PE) {#0008 .h1}
================================

Point to Point Encryption (P2PE) enhances the security of account data
by encrypting it between a Point of Interaction (POI) device and the
decryption environment. Starting with version 2.02.021, Simplify can be
implemented as part of an Elavon PCI-validated P2PE solution. This will
allow Simplify customers to reduce the scope of their PCI audits.

The principal purpose of this chapter is to serve as a guide to inform
users on the role of Simplify in Elavon's PCI-validated P2PE solution.
Customer requirements for PCI-validated P2PE can be summarized as
follows:

-   Ingenico Telium or Tetra PIN Pads using On-Guard encryption. See
    [Versioning](#00085) for more information.

-   All general requirements for secure communications must be followed.
    Network security must be reviewed periodically.

-   Any PCI-sensitive data received by the POS (encrypted or
    unencrypted) must be securely deleted when no longer needed.

-   Printing must conform with PCI and TPP rules for masking.

-   Informational Prompt messages (see [Informational Prompting](#0006))
    must not be used to request PCI-sensitive data from the customer.

Encryption Types {#00062 .h2}
----------------

Simplify supports two types of encryption (starting with version
2.02.021):

-   The legacy Voltage encryption. Not eligible for PCI-validated P2PE.

-   Ingenico's On-Guard encryption. Eligible for PCI-validated P2PE.

The type of encryption used in an implementation can be displayed on the
PIN Pad, as described in Chapter 1 under [Versioning](#00085). This
information is also sent in API field 5004, which has been modified as
follows:

**Encryption Provider ID (field 5004)**

The Elavon API uses field 5004 to indicate the encryption type as
follows:

-   G2 = Voltage

-   OG = On-Guard (version 2.02.021 and higher)

Whitelisting {#00063 .h2}
------------

Simplify uses a Whitelisting process to determine which accounts can be
exempted from encryption of PCI-sensitive data and returned to the POS
unencrypted. This process is based on two lists of account numbers, a
whitelist (merchant-configurable) and a blacklist, used together as
follows:

-   Data for accounts in the whitelist will not be sent to the host, but
    will be returned to the POS unencrypted for use as determined by the
    merchant (Whitelist response).

    -   **Exception:** Sensitive data for PCI-protected accounts (as
        defined in the blacklist) will never be sent to the POS
        unencrypted, even if the PAN is included in the whitelist.

-   PCI-sensitive data fields for non PCI-protected accounts not in the
    whitelist (i.e. for accounts not in the whitelist or blacklist) will
    normally be encrypted.

    -   **Exception:** If there is an encryption failure (not caused by
        system failure), sensitive data for these accounts can be sent
        unencrypted.

-   A Whitelist response is triggered by the POS sending a financial
    request for an account in the whitelist and not in the blacklist.
    Please see below for a sample request/Whitelist response.

If you want to use a [Whitelisting](#00063) process, please contact your
Elavon representative for whitelist configuration.

### Sample Transaction with Whitelist Response {#sample-transaction-with-whitelist-response .h3}

The following sample of a whitelisted Sale transaction shows the
Whitelist response sending account data to the POS in the clear (field
3). The PAN must be in the whitelist and not in the blacklist.

#### Request {#request-36 .h4}

  API Field \#, Value   Description
  --------------------- -----------------------------------------------------------------------
  0001,02               Transaction Type
  0002,4.00             Transaction Amount
  0007,1025             Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](#00073).
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,143005           Transaction Time (current time) -- HHMMSS
  0017,0.00             Cash Back Amount
  0109,TERM1            Terminal ID
  0110,205              Cashier ID
  0201,0.00             Tip Amount
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox.
  8002,ONGUARD          Location Name (provided by Elavon)
  8006,TSTLA3           Chain Code (provided by Elavon)

#### Whitelist Response {#whitelist-response .h4}

The Response Message field (1010) will contain \*SLR WHITELIST,
indicating a Whitelist response. Note that field 5004 (Encryption
Provider ID) is not sent in a whitelist response because the account
data is not encrypted.

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,02                             Transaction Type

  0002,4.00                           Transaction Amount

  0003,&&&&&&&&&&&&&&&&&=&&&&         **Account data in the clear**\
                                      See under [Usage](/#00079) for
                                      details.)

  0007,1025                           Transaction ID / Reference Number

  0011,xxx..                          User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  0013,022519                         Transaction Date (current date) --
                                      MMDDYY

  0014,143005                         Transaction Time (current time) --
                                      HHMMSS

  0017,0.00                           Cash Back Amount

  0109,TERM1                          Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0201,0.00                           Tip Amount

  1003,0000                           Response Code

  1004,-99                            Response Message

  1008,ID:                            Echoes values in request

  1009,999                            Response Code

  **1010,\*SLR WHITELIST**            Simplify Response Message

  5002,81112159                       Device Serial Number

  5010,EMVDC0838                      EMV kernel version

  8002,ONGUARD                        Location Name (provided by Elavon)

  8006,TSTLA3                         Chain Code (provided by Elavon)

                                      
  -----------------------------------------------------------------------

Auto Signature {#00064 .h2}
--------------

Auto Signature is a feature that allows Simplify to automatically prompt
for a signature and send a Signature message (**Signature Response**
format) to the POS, *without* first receiving a **Signature Request**.
(Signature prompt will occur before or after the prompt to remove EMV
card, depending on configuration.)

The following transactions are eligible for auto signature: approved
**Sale**, **Auth Only** and **Return** transactions on touchscreen PIN
Pads. If Auto Signature is supported, all Stand In responses from
Simplify must be approved by the POS, as signature processing will occur
*regardless* of the POS decision.

Configuration settings determine whether auto signature will occur for
an eligible transaction. However these settings can be overridden by a
field in the authorization request. This design provides two ways to
trigger an auto signature:

-   Configuration -- Simplify can be configured to perform an auto
    signature for all transactions that satisfy a configured minimum.

    -   This minimum is defined independently for each combination of
        supported transaction type and tender type. If set to 0, auto
        signature will be disabled.

-   POS message -- An optional Auto Signature Control field in the
    authorization request (field 11 bytes 4-5) can be used to force or
    suppress an auto signature for the transaction, regardless of
    configuration.

    -   The use of the Auto Signature Control field must be enabled.
        This is controlled by a separate setting that only affects the
        use of this field. This setting is defined independently for
        each combination of supported transaction type and tender type.

    -   To force an auto signature, send S1 in this field.

    -   To suppress auto signature (regardless of configuration) send S0
        in this field.

    -   If this field is blank, configuration settings will determine
        whether auto signature processing occurs.

For auto signature-eligible transactions, Simplify will use field 5001
bytes 1-8 in the authorization response to inform the POS whether
Simplify is performing auto signature processing for the transaction, as
follows:

-   991002S0 = Simplify will not prompt for signature. It is in CLOSED
    state

-   991002S1 = Simplify is asking for signature, wait for Signature
    Response.

The wording on the auto signature screen can be customized by Elavon. Up
to three lines of text can be defined, with a maximum length of 40
characters each. Please contact your Elavon representative regarding
your requirements.

### Sample Messages {#sample-messages .h3}

#### **Sale Request** {#sale-request .h4}

The following table shows an example of a **Sale Request** message (from
the POS to Simplify) with field 11 set to force an auto signature:

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,02                             Transaction Type

  0002,1000.00                        Transaction Amount

  0007,34                             Transaction ID / Reference Number

  0011,035**S1**                      User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).\
                                      **Bytes 4-5 = S0 suppresses
                                      signature**\
                                      **Bytes 4-5 = S1 forces auto
                                      signature**

  0013,022519                         Transaction Date (current date)--
                                      MMDDYY

  0014,115654                         Transaction Time (current time) --
                                      HHMMSS

  0017,0.00                           Cash Back Amount

  0109,Term02                         Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  1008,ID:                            Set to 'ID:' to request that an
                                      account Token be returned by
                                      Fusebox

  8002,ONGUARD                        Location Name (provided by Elavon)

  8006,TSTLA3                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------

#### **Sale Response** {#sale-response .h4}

The table below is an example of a **Sale Response** message (from
Simplify to the POS) with field 5001 set to indicate that Simplify is
performing an auto signature process.

  -----------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------------------------------------------------------------------
  0001,02                             Transaction Type

  0002,1000.00                        Transaction Amount

  0003,ID:4295897590750119            Account Data (token)

  0004,1222                           Expiration Date (MMYY)

  0006,26793F                         Authorization Code (returned by Fusebox)

  0007,33                             Transaction ID / Reference Number

  0009,001                            Fusebox -- Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled Field Definitions](#00073).

  0013,022519                         Transaction Date (current date) -- MMDDYY

  0014,113425                         Transaction Time (current time) -- HHMMSS

  0017,0.00                           Cash Back Amount

  0030,1                              Fusebox -- Online Indicator

  0032,022519                         Fusebox -- Authorization Transaction Date

  0033,143439                         Fusebox -- Authorization Transaction Time

  0034,E                              Fusebox -- Authorization Characteristics Indicator

  0035,RXG9                           Validation Code

  0036,307229668795255                Host Transaction Identifier

  0037,5                              Fusebox -- Authorizer

  0043,207870                         System Trace Audit Number

  0047,C;1;1;1;0;1;5;5;4;3;3;C;0;4    POS Data Code

  0049,F                              Fusebox -- Card Product Result Code

  0052,0                              Transponder / Proximity Indicator (0 = contact; 2 = contactless , 5 = swiped)

  0054,05                             POS Entry Mode

  0055,1                              PIN Capabilities

  0057,0                              ICC Chip Condition Code

  0061,00                             Terminal Type

  0062,201                            Service Code

  0063,00                             CAT Indicator

  0109,TERM02                         Terminal ID

  0110,205                            Cashier ID

  0112,400                            Fusebox -- Processor ID

  0115,010                            Transaction Qualifier (010 = credit; 030 = debit)

  0125,817183439                      Retrieval Reference Number (may need to appear on receipt)

  0126,2                              Track Indicator (may need to appear on receipt)

  0129,0                              Fusebox -- Compliance Data

  0130,1000.00                        Authorized Amount

  0140,USD                            Merchant Currency

  0201,5.00                           Tip Amount

  0651,0000000                        Reversal data (for reversal, if needed)

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1002,UAT USA/Test Card 03           Cardholder Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,\*\*\*\*\*\*\*\*\*\*\*\*0119   Masked Account Number (for printing on receipt)

  1009,AA                             Host Response Code

  1010,COMPLETE                       Gateway Response Message

  1012,0021                           Gateway Batch Number

  1200,0000AA                         Issuer Network Information

  1333,03062017                       Last Host EMV Key Download

  1359,1                              Card Verification Method

  1378,1326\|Application Label:       EMV Approved Receipt Field List
  ;1300\|TC: ;1307\|TVR: ;1325\|AID:  
  ;                                   

  1379,1326\|Application Label:       EMV Declined Receipt Field List
  ;1300\|AAC: ;1307\|TVR: ;1325\|AID: 
  ;                                   

  1380,CHIP                           POS Entry Receipt Indicator

  4747,040511                         Third Party Interface POS Data Code

  5001,**991002S1**                   **991002S0 = No auto signature.**\
                                      **991002S1 = Wait for auto signature.**

  5002,80649419                       Device Serial Number

  5004,OG                             Encryption Provider ID

  5006,FFFF4D4D4D0000C00152050006     Terminal KSN

  5007,V                              [PCI P2PE]{.tooltip tooltip-content="#PCIP2PE"
                                      style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}-validated
                                      solution indicator

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See[Simplify-Controlled Field Definitions](#00073).

  8002,ONGUARD                        Location Name (provided by Elavon)

  8006,TSTLA3                         Chain Code (provided by Elavon)
  -----------------------------------------------------------------------------------------------------------------------------------

### **Sample Signature Message** {#sample-signature-message .h3}

An example of a Signature Message sent for an auto signature (from
Simplify to the POS) is shown below. The format is identical to a
**Signature Response** (36-02) message.

  API Field \#, Value                      Description
  ---------------------------------------- -------------------------------------------------------------------------------
  0001,36                                  Transaction Type. A value of 36 indicates a Non-Financial transaction
  0011,xxx..                               User Data. See [Simplify-Controlled Field Definitions](#00073).
  0052,0                                   Transponder / Proximity Indicator (0 = contact; 2 = contactless , 5 = swiped)
  5000,xxxxxxxxxxxxxxxxxxxxxxxx.......xx   Signature data

Quick Chip Tendering {#00065 .h2}
--------------------

Quick Chip is a feature used to speed up the processing of EMV and other
transactions. This feature has two parts:

-   On EMV transactions, no second Application Cryptogram (AC) will be
    required when processing the response. This will allow the customer
    to complete card processing and remove their card before Simplify
    receives the host response.

-   A **Quick Chip** **Message** (Tran Type 36-40) will be supported for
    Sale, Auth and Refund transactions (EMV or non-EMV). If Simplify
    receives a valid Quick Chip request from the POS, it will allow the
    customer to insert their card and complete card processing before
    the PINpad receives the transaction total. The Quick Chip request
    will then need to be followed by a financial request.

A Quick Chip tender is defined as a tender whose processing includes a
valid Quick Chip Message.

Quick Chip Message details are as follows:

-   Message fields are field 1 (Tran Type = 36) and field 11.

-   Field 11 in the request must contain a Q token.

-   Field 11 in the response contains a Completion Code (bytes 9-11)
    giving the outcome of the request. A value of 000 indicates a valid
    Quick Chip request; if non-zero, processing ahead of the transaction
    total will not be allowed.

-   See [Simplify-Controlled Field Definitions](#00073) especially under
    Token Area for more information on field 11 in the Quick Chip
    Message.

Other processing modifications for Quick Chip tenders include the
following:

-   After Simplify receives a Quick Chip request, the following screens
    will be suppressed until the Financial request is received: Amount
    OK or DCC, Tip Amount.

-   Additional Status Messages have been added to support Quick Chip.
    Please consult your Elavon representative for more information.

-   Simplify can be configured to support Cash Back for Quick Chip Sale
    tenders. Please consult your Elavon representative for more
    information.

-   If a tender type is sent in both the Quick Chip request and the
    financial request (both optional), the tender types must match; if
    not the transaction will be declined.

-   Simplify can be configured to require customer confirmation if
    Cancel is pressed during a Quick Chip tender.

Simplify-Generated Messages {#0009 .h1}
===========================

Simplify-generated response messages are used for transactions processed
offline. This will occur if a transaction is declined locally (no host
message) or if the host is unavailable.

For EMV, Simplify will also generate a response message if the chip
declines a host-approved transaction or the customer removes the card
before the transaction is completed.

Simplify-generated response messages are indicated by an asterisk (\*)
as the first character of the message. The first four characters
indicate the type of transaction as follows:

\***SLR** -- non-EMV

\***ICC** -- contact or contactless EMV

Non-EMV {#00066 .h2}
-------

  ----------------------------------------------------------------------------------------
  Field 1003     Field 1004     Field 1010       Condition        Action
  (Gateway       (Host Response (Gateway                          
  Response Code) Code)          Response                          
                                Message)                          
  -------------- -------------- ---------------- ---------------- ------------------------
  -7                            \*SLR NO         An [Inquiry      Decline -- No Inquiry
                                MATCHING         message (Tran    needed
                                RECORDS.         Type             
                                                 22)](#00016) was 
                                                 received by      
                                                 Simplify, but    
                                                 Simplify could   
                                                 not find the     
                                                 corresponding    
                                                 Account Number.  

  -16                           \*SLR FINAL \$   Amount of Cash   Decline -- No Inquiry
                                TOO LRG.         back is over     needed
                                                 limit            

  0                             \*SLR STAND-IN.  Setting is for   POS decides to approve
                                                 Simplify to      or decline.\
                                                 Stand In, and    Inquiry needed. See
                                                 either request   under [Stand-in
                                                 timed out or no  Processing](#0003)for
                                                 communication.   more information.
                                                 The response     
                                                 contains the     
                                                 encrypted        
                                                 account number,  
                                                 which is         
                                                 required for the 
                                                 store to perform 
                                                 Stand-In.        

  0000           -99            \*SLR WHITELIST. Whitelisted      POS processes the
                                                 transaction      returned data.\
                                                 returned to POS  See
                                                 (not sent to     [Whitelisting](#00063)
                                                 Fusebox) with    for more information.
                                                 account data in  
                                                 the clear.       

  3                             \*SLR            Simplify cannot  Inquiry needed
                                COMMUNICATIONS   get connected to 
                                ERROR.           Fusebox.         

  30                            \*SLR BUSY.      Simplify is      Retry -- No Inquiry
                                                 processing       needed
                                                 another request. 

  41                            \*SLR BAD ACCT   Account number   Decline -- No Inquiry
                                NUMBER.          failed MOD 10    needed
                                                 validation       

  47                            \*SLR BAD CARD   Card not valid   Decline -- No Inquiry
                                TYPE.                             needed

  49                            \*SLR BAD        Invalid          Decline -- No Inquiry
                                EXPIRATION.      expiration date  needed

  60             99             \*SLR INVALID    Request message  Decline -- No Inquiry
                                FORMAT.          format is        needed
                                                 invalid.         

  60             -99            \*SLR CALL HELP  Voltage error    Decline -- No Inquiry
                                DESK.            invalidating     needed
                                                 account data or  
                                                 error in         
                                                 On-Guard         
                                                 process.         

  88                            \*SLR SWITCH     Host timeout     Inquiry needed
                                TIMEOUT.                          

  173                           \*SLR TRAN NOT   Offline not      Decline -- No Inquiry
                                ALLOWED          allowed          needed

  174                           \*SLR ACCOUNT    The account      Decline -- No Inquiry
                                NOT TOKEN        number entered   needed
                                ELIGIBLE.        as a result of a 
                                                 Token Request is 
                                                 not Token        
                                                 eligible         

  208                           \*SLR CANCEL KEY The Cancel key   Decline -- No Inquiry
                                PRESSED.         was pressed on   needed
                                                 the PIN Pad, or\ 
                                                 Timeout on PIN   
                                                 entry            

  208                           \*SLR INCOMPLETE (Requires        Decline -- No Inquiry
                                PIN              special          needed
                                                 configuration.   
                                                 Will not occur   
                                                 in most          
                                                 installations.   
                                                 Consult Elavon   
                                                 for more         
                                                 information.)    

  259                           \*SLR Reset      Error condition  Decline -- Inquiry
                                                 from invalid     needed
                                                 input            
  ----------------------------------------------------------------------------------------

EMV {#00067 .h2}
---

  -----------------------------------------------------------------------
  **Field 1003 (Gateway   **Field 1010 (Gateway   **Action**
  Response Code)**        Response Message)**     
  ----------------------- ----------------------- -----------------------
  208                     \*SLR INCOMPLETE PIN    (Requires special
                                                  configuration. Will not
                                                  occur in most
                                                  installations. Consult
                                                  Elavon for more
                                                  information.)\
                                                  No Inquiry needed

  253                     \*ICC EMV PROCESSING    Inquiry
                          ERROR.                  

  254                     \*ICC EMV CANCELED      Inquiry
                          TRANS.                  

  255                     \*ICC EMV CARD ERROR.   Inquiry

  258                     \*ICC CARD STILL        Informational - No
                          PRESENT.                Inquiry needed

  260                     \*ICC EMV UNDEFINED     Inquiry
                          STATUS.                 

  264                     \*ICC EMV DECLINED.     Decline - No Inquiry
                                                  needed
  -----------------------------------------------------------------------

Appendices {#0010 .h1}
==========

Appendices A-E in this chapter provide some generic information on
Simplify transaction flow, communications, and message flow.

[Appendix F](#0006) describes Simplify-controlled field definitions.

Appendix G provides notes on [Usage.](/#00079)

Appendix H provides a revision history for this document on the Elavon
Developer Portal.

Appendix I is an [Addendum](/#00081) containing material added since the
initial Developer Portal release for this version of Simplify.

Appendix A - Generic Transaction Flow {#00068 .h2}
-------------------------------------

The following diagram shows the Point of Sale (POS) System, PIN Pad and
Fusebox host communicating over a TCP / IP connection:

::: {.mermaid}
sequenceDiagram participant Customer Network participant Retail Location
participant Fusebox Retail Location-\>\>Customer Network:Sending data
from POS1 Retail Location-\>\>Customer Network:Sending data from POS2
Customer Network-\>\>Retail Location:Sending data to Ingenico Telium
Retail Location-\>\>Fusebox:Using Simplify to send to Fusebox
:::

\

Appendix B - Simplify RS-232 Communication Protocol {#00069 .h2}
---------------------------------------------------

When using the Simplify RS-232/HID Communication Protocol, the PIN Pad
is attached to the POS device using an RS-232 serial connection (or USB
emulating RS-232). The communication protocol between the POS device and
the Simplify application includes the following elements:

-   Start of Text (STX)

-   End of Text (ETX)

-   Longitudinal Redundancy Check (LRC)

The **Longitudinal Redundancy Check** (**LRC**) is generated by
performing an exclusive OR on all characters in the message except the
**Start of Text** (**STX**), but inclusive of the **End of Text**
(**ETX**). The LRC calculation is performed by both the sending and
receiving stations, as shown in [Appendix C](#00070).

There are two types of messages flowing between the POS device and
Simplify:

-   Link-level messages

-   Data-level messages

Data-level messages are described in Chapter 2 [Message
Details](#core_concepts). This appendix describes the Link-level
messaging.

The **Link**-**level Response** between the POS device and Simplify
provides positive acknowledgement to a message. All messages result in a
**Link**-**level Response**:

-   An ACK (hex 06) is a positive acknowledgement to a received message.
    It indicates to the sending station that the message was correctly
    received, including proper message format and a successful LRC
    check. If the sending station does not receive an ACK within a
    parameterized amount of time, it must retransmit the previous
    message. If the retransmission is repeated a parameterized number of
    times for the same message and an ACK is not received, communication
    with the device is assumed to be lost and the proper actions are to
    be taken by the sending station.

-   A NAK (hex 15) is a negative acknowledgement to a received message.
    It indicates to the sending station that some data was received but
    it was not received correctly. The reasons for a NAK include invalid
    format or failed LRC check. If the sending station receives a NAK
    response to a message, it should re-transmit the previous message.
    If a NAK continues to be received after a parameterized number of
    retransmissions, communications with the other device is assumed to
    be lost and the proper actions are to be taken by the sending
    station.

**Note**: The following values are configurable parameters in Simplify
(it is suggested they should also be configurable parameters in the POS
device as well):

-   Number of Retries -- a default value of 3

-   Timeout Waiting for ACK / NAK -- a default value of 1 second.

Appendix C - Example Link Level Exchanges (Serial Communications and USB emulating Serial) {#00070 .h2}
------------------------------------------------------------------------------------------

The POS device will attempt to transmit the message a parameterized
number of times before assuming communications are lost.

#### Normal Message Flow {#normal-message-flow .h4}

::: {.mermaid}
sequenceDiagram participant POS Device participant Simplify POS
Device-\>\>Simplify:\<STX\>MSG\<ETX\>\<LRC\> Simplify-\>\>POS
Device:\<ACK\> Simplify-\>\>POS Device:\<STX\>MSG\<ETX\>\<LRC\> POS
Device-\>\>Simplify:\<ACK\>
:::

#### NAK Response Message Flow {#nak-response-message-flow .h4}

::: {.mermaid}
sequenceDiagram participant POS Device participant Simplify POS
Device-\>\>Simplify:\<STX\>MSG\<ETX\>\<LRC\> Note right of Simplify:Bad
LRC Simplify-\>\>POS Device:\<NAK\> POS
Device-\>\>Simplify:\<STX\>MSG\<ETX\>\<LRC\> Simplify-\>\>POS
Device:\<ACK\> Simplify-\>\>POS Device:\<STX\>MSG\<ETX\>\<LRC\> POS
Device-\>\>Simplify:\<ACK\>
:::

Appendix D - Recovery after Timeout Flow {#00071 .h2}
----------------------------------------

Simplify attempts to transmit the message a parameterized number of
times before assuming communications are lost.

The message flow is bi-directional. The POS device or Simplify can
initiate a message. In order to avoid timeouts and retransmissions
between the POS device and Simplify, each endpoint (POS device or
Simplify) should read an incoming message, calculate the LRC, and
immediately respond with an ACK or NAK.

::: {.mermaid}
sequenceDiagram participant POS Device participant Simplify
Simplify-\>\>POS Device:\<STX\>MSG\<ETX\>\<LRC\> Note right of
Simplify:1 second timeout Simplify-\>\>POS
Device:\<STX\>MSG\<ETX\>\<LRC\> POS Device-\>\>Simplify:\<ACK\> POS
Device-\>\>Simplify:\<STX\>MSG\<ETX\>\<LRC\> Simplify-\>\>POS
Device:\<ACK\>
:::

**Exception to Timeout/Recovery Rules**

After a timeout on a non-critical message, Simplify does not expect an
ACK and will not retry the message. Sending an ACK for a non-critical
message will not cause any issue. The following messages are considered
non-critical, with the default exceptions noted:

  -----------------------------------------------------------------------
  Message Type                        Exceptions
  ----------------------------------- -----------------------------------
  Status messages\                    Exceptions: Status Identifier =
  (Tran Type 36-51)                   001, 021\
                                      (For information on Status
                                      Identifiers, see
                                      [Simplify-Controlled Field
                                      Definitions](#00073).)

  -----------------------------------------------------------------------

The list of Status Identifiers for which a Status Message must be ACK'd
is configurable. Please consult your Elavon representative for more
information.

Appendix E - LRC Calculation {#00072 .h2}
----------------------------

Returns: Longitudinal Redundancy Checksum (LRC)

Appendix F - Simplify-Controlled Field Definitions {#00073 .h2}
--------------------------------------------------

This appendix describes the following fields whose definition is
controlled by Simplify:

**Field 0011 (User Data)**\
\
**Field 5001 (Non-Financial Data)**\
\
**Field 5070 (Simplify Information)**\
\
**Field 5071 (Card/Cardholder Present?)**\
\
**Field 5104 (Tip Prompting)**\
\

Since Fusebox does not modify these fields (and in some cases, does not
receive them), they allow the POS and Simplify to communicate with each
other with no concern for how Fusebox might affect the data.

Field 11 (User Data) {#00074 .h2}
--------------------

Field 11 is defined by the Gateway Interface Specification as a
user-defined field with a variable length (up to a maximum of 512
characters).

### Structure of Field {#structure-of-field .h3}

For added flexibility, this field contains two data areas, a **Command
Area** for non-tokenized data and a **Token Area** for tokenized data
("TAG Length Data Structure"). These data areas are used as follows (see
below for details):

-   The **Command Area** contains subfields required in the request.
    Some or all of these subfields may be echoed in the response. In
    [Non-Financial Messages](#00021), the Command Area in the response
    may contain a Completion Code indicating the outcome of the request.

-   The **Token Area** is informational. It can be used to inform the
    POS of error conditions and/or Simplify version data.

    -   Exception: In the Quick Chip (36-40) Message, data is required
        in both the Command and Token areas of the request.

The generic format of field 11 is as follows:

  -----------------------------------------------------------------------
  Subfield Name     Description       Offset            Length
  ----------------- ----------------- ----------------- -----------------
  Command Area      The format of     0                 VAR
                    fields in the                       
                    Command Area                        
                    depends on the                      
                    Transaction Type                    
                    (and Message Type                   
                    for Transaction                     
                    Type = 36). The                     
                    Maximum Length of                   
                    this area is                        
                    currently 11                        
                    characters.                         

  Field Separator   The character '?' VAR               1
                    is used to                          
                    separate the                        
                    Command Area from                   
                    the Token Area                      

  Token Area        The Token Area    VAR               VAR
                    contains                            
                    Tokenized fields                    
                    in the format                       
                    "TLLDDD..."                         
                    where\                              
                    T = Token\                          
                    LL = Length of                      
                    Data\                               
                    DDD... = Data                       
                    (Length = LL)                       
  -----------------------------------------------------------------------

The Command Area will be discussed below, followed by the [Token
Area](#TokenArea){.highlight}

### **Command Area** {#command-area .h3}

As shown in the following tables, the use of the Command Area can vary
by Tran Type and (for [Non-Financial Messages](#00021)) by Message Type.
Since the use of this field for Financial Messages is totally distinct
from that for [Non-Financial Messages](#00021), the following discussion
will be broken down by these two categories.

**Command Area - Financial Messages**

Depending on Tran Type, the following subfields may be used in the
Command Area of field 11 for Financial Messages.

  Bytes   Subfield Name            Use
  ------- ------------------------ ----------------------------------------------------------
  1-3     Switch Timeout Value     Defines host timeout value used by Simplify
  4-5     Auto Signature Control   Can be used to ovrride configured Auto Sigature settings

The following table shows supported Command Area subfields for each
defined Financial Message Type:

Field 11 Command Area subfields are used in Financial messages as
follows:

-   **Switch Timeout Value** -- Three-digit field (right-justified /
    zero-filled) controls how long (in seconds) Simplify will wait for a
    response from Fusebox.

    ::: {.notices .note}
    <div>

    \*\*Note:\*\* The length of this timeout value \*must be shorter\*
    than the POS timeout value.

    </div>
    :::

-   **Auto Signature Control** -- Two-byte field that can be used to
    override auto signature configuration on a per transaction basis.
    The use of this field is optional and must be enabled under
    configuration. Use as follows:

    -   Send S0 to suppress auto signature for the transaction
        regardless of configuration settings. (No signature processing
        will occur unless a **Signature Request** is received.)

    -   Send S1 to force auto signature for the transaction regardless
        of configuration settings.

    -   If blank, configured settings will determine whether auto
        signature processing occurs.

    For additional information on auto signature,see Chapter 9.

**Command Area - [Non-Financial Messages](#00021)**

The purpose of a Non-Financial Message (Tran Type 36) is defined by its
Message Type (field 11 bytes 1-2). The structure of the Command Area for
field 11 on a Non-Financial Message can vary depending on the Message
Type (bytes 1-2), but the following subfields are typical:

  Bytes   Subfield Name                 Use
  ------- ----------------------------- --------------------------------------------------------------------------------------
  1-2     Message Type                  Defines purpose of message.
  3-5     Transaction Sequence Number   POS transaction sequence number.
  6-8     Screen ID                     Used in request to define PIN Pad screen to be displayed (may be blank or not used).
  9-11    Completion Code               Used in response to inform POS of request outcome.

Variations from the above structure are illustrated in the following
table showing supported Command Area subfields for each defined Message
Type. Except where indicated, the Command Area in the response echoes
the request.

Note concerning the following Non-Financial Message Types:

-   Message Type 40 (Quick Chip Message) -- Data is also required in the
    Token Area (Q token).

-   Message Types 08, 09, 13, 16-21 -- These values are reserved for
    future use.

Field 11 Command Area subfields are used in [Non-Financial
Messages](#00021) as follows:

**Message Type** -- Two-digit field used along with the Tran Type to
identify the purpose of the message. Always present for Tran Type = 36.

**Transaction Sequence Number** -- Three-byte field containing POS
transaction sequence number. This field is echoed back in the response.
Always present for Tran Type = 36.

**Screen ID** -- Three-digit field in **Signature Request** used to
indicate which screen should be displayed when prompting for the
customer's signature. This field is echoed back in **Signature
Response**. (Currently supported values are 001 and 002.) This field is
also present in the **Informational Prompt** request and response
messages, but is not used.

**Completion Code** -- Three-digit field in **Signature Response** or
**Informational Prompt**, **Response** indicating the outcome of the
request.

  -----------------------------------------------------------------------
  **Completion Code**                 **Outcome**
  ----------------------------------- -----------------------------------
  000                                 In Informational Prompt and Quick
                                      Chip responses: Successful

  004                                 DONE/ACCEPT key pressed with
                                      Signature data present

  006                                 ABORT/CANCEL key pressed twice with
                                      no detectable signature

  008                                 Signature entry aborted by Simplify

  009                                 Signature entry aborted due to
                                      memory being exceeded

  010                                 Memory exhaustion

  099                                 Customer pressed CANCEL after
                                      starting to sign. (NA 006 will be
                                      sent if cannot detect signature)

  100                                 Transaction not allowed for
                                      device.\
                                      PIN Pad is currently busy.\
                                      For signature capture: Unable to
                                      create sigcap object or signature
                                      too small two times.\
                                      In Quick Chip response: error (e.g.
                                      Quick Chip not enabled).

  131                                 In Quick Chip response: Customer
                                      pressed Cancel.

  132                                 In Quick Chip response: Bad Card
                                      Type

  133                                 In Quick Chip response: Transaction
                                      not allowed.

  200                                 EMV card still inserted

  998                                 Invalid format

  999                                 Timed out
  -----------------------------------------------------------------------

**Version Build Info** -- Simplify version and build information.

**Timeout** -- Screen timeout in seconds. (000=No timeout)

**Status Identifier** -- Three-digit transaction status code sent from
Simplify to POS in Status Messages. A table included in a Simplify
parameter file indicates which Status Identifiers are enabled. The
following Status Identifiers are currently defined:

  **Status Identifier**   **Status Message**
  ----------------------- ------------------------------------
  001                     Processing Please Wait
  002                     Slide Card
  003                     Enter PIN
  004                     Amount OK
  005                     Enter Tender Type (Debit / Credit)
  006                     Cash Back
  007                     Enter Account Number
  008                     Enter Expiration Date
  009                     Enter CVV
  010                     Enter ZIP Code (AVS Data)
  011                     Cash Back Other
  012 -- 016              \[Reserved\]
  017                     EMV AID list
  018                     Language Selection
  019                     EMV Account Type Selection
  020                     Enter Tip
  021                     EMV card has been removed
  022                     Swiped not allowed, must use chip
  023                     EMV fallback

**Sample Field 11**

The following sample of field 11 is for a Signature Response message
sent in response to a Signature Request:

0011,02555001004

This value is broken down as follows:

  Bytes   Subfield Value   Use
  ------- ---------------- -----------------------------------------------------------------------------
  1-2     02               Message Type 02 -- Signature Response
  3-5     555              POS Transaction sequence number.
  6-8     001              Screen ID (Echoed from Signature Request message)
  9-11    004              Completion Code. 004 = DONE/ACCEPT key pressed with signature data present.

### **Token Area** {#token-area .h3}

Defined Tokens for the Token Area are as follows:

  -----------------------------------------------------------------------
  Token\            Description       Usage             Max\
  (Case Sensitive)                                      Length
  ----------------- ----------------- ----------------- -----------------
  V                 Simplify Version  Simplify response 10
                                      to POS            

  S                 Identifies the    Simplify error    40
                    Source Routine of response to POS   
                    the Error                           

  R                 Return code from  Simplify error    20
                    Source Routing    response to POS   

  E                 Actual Error if   Simplify error    20
                    different from    response to POS   
                    'R'                                 

  Q                 Transaction Type  POS Quick Chip    20
                    and Tender Type\  request to        
                    (data is          Simplify, echoed  
                    optional)         in response       
  -----------------------------------------------------------------------

With the exception of the Q token, the above tokens are for
informational purposes only.

**Q token**

The Q token must be present in order for Simplify to approve a Quick
Chip (36-40) request. The format of the Q token is as follows:

Qaabb\<FS\>ccc\<FS\>, where:

A sample Quick Chip request, showing the Command Area, '?' separator and
Token Area for field 11 is as follows:

0001,36\
0011,40001000000?Q0402\<FS\>\<FS\>

This request is for a Sale (=02) transaction. (Tender Type not
specified.)

Field 5001 (Non-Financial Data) {#00075 .h2}
-------------------------------

Field 5001 is used in the following types of messages as follows:

-   In [Non-Financial Messages](#00021) (Tran Type 36):

    Used in requests and/or responses for most Message Types:

    -   In request, used to define display or screen operation.

    -   In response, used to indicate outcome of requested operation. In
        [Informational Prompting](#0006) Messages (36-14), this field
        returns customer feedback.

    Details are message-specific. For more information, see the formats
    and sample messages given under [Non-Financial Messages](#00021) and
    [Informational Prompting](#0006) Messages.

-   In Financial Responses:

    For auto signature-eligible transactions, Field 5001 is used in the
    financial response to inform the POS whether Simplify is performing
    [Auto Signature](#00064) processing for the transaction. For
    details, see [Auto Signature](#00064).

Field 5070 (Simplify Load Information) {#00076 .h2}
--------------------------------------

Field 5070 is used in financial responses to the POS to return the
Simplify version number and other Simplify load information (e.g.
parameter file version numbers, TMS Identifier). The maximum length of
this field is 256 bytes.

A current sample of this field is as follows:

This field contains the following information about the PIN Pad's
Simplify implementation:

  **Subfield Name**   **Current value**   **Meaning**
  ------------------- ------------------- ---------------------------------------------
  Merchant            \<Merchant Name\>   Identifies implementation by merchant name.
  Simplify            G2-2.02.52402       Simplify version number
  PARM                2.24.1              parm.fil parameter file version
  TENDERDEF           2.24.1              tenderdef.fil parameter file version
  EMVPARM             EMVPARM-E4          emvparm.fil parameter file version
  TMS                 87654321            TMS identifier of the PIN Pad

Field 5071 (Card/Cardholder Present?) {#00077 .h2}
-------------------------------------

[]{#Field_5071 .highlight}

Field 5071 is used in financial requests from the POS to inform Simplify
whether the card and cardholder were present for the transaction. This
field is only used by Simplify to help set field 47, and is not sent to
Fusebox. If sent in the request, this field will be echoed in the
response.

Supported values are:

<!-- -->

<!-- -->

If the value in 5071 is invalid or not present, Simplify will use a
default value of 1.

Field 5104 (Tip Prompting) {#00078 .h2}
--------------------------

Simplify can be configured to automatically prompt for a Tip amount. If
configured to do so, the Tip prompting screen will also allow the
customer to select the Tip amount from displayed amounts based on up to
three configured Tip percentages.

Field 5104 can be sent in a Financial Request to override the configured
Tip parameters for the current transaction. If sent in the request, this
field will be echoed in the response.

The format of this field is aa;bb;cc\<FS\>d where:

The semi-colons (;) and field separator (\<FS\>) are required even if
the Tip percentages are not present.

A sample of this field is as follows:

The effect of this field is as follows:

-   If the Tip prompting flag in field 5104 is set to 0, the Tip screen
    will not be displayed.

-   If this flag is set to 1, the Tip screen will be displayed.

-   If one or more Tip percentages are defined, the corresponding Tip
    amounts will be displayed on the Tip screen.

-   The customer can either key in the Tip amount or select it from the
    displayed amounts.

-   If no Tip percentages are defined, the Tip amount can only be keyed
    in by the customer.

Appendix G - Usage {#00079 .h2}
------------------

Note concerning usage in this document:

-   When you see an ampersand (&), please expect real data that has been
    masked for documentation.

-   This guide will refer to POS / PMS as POS only.

Appendix H - Revision History {#00080 .h2}
-----------------------------

**Note:** This documentation applies to Simplify version 2.02.024 builds
35 and higher, and version 2.02.025 all builds.

  --------------------------------------------------------------------------
  Document\               Date                    Revision Notes
  version                                         
  ----------------------- ----------------------- --------------------------
  2.02.025.5              OCT 2019                Added support for
                                                  non-Pay\@Table printing
                                                  (Print Request Message).\
                                                  \
                                                  Added API 1379 (Offline
                                                  EMV Receipt Field List) to
                                                  Stand-in Response to POS.

  2.02.025.4              JUL 2019                Modified headings of
                                                  sample messages to be more
                                                  uniform and to avoid
                                                  unnecessary Table of
                                                  Contents entries in the
                                                  pdf.

  2.02.025.3              JUN 2019                Changed references to
                                                  Telium PIN Pads to refer
                                                  to Telium and Tetra.

  2.02.025.2              MAY 2019                Added ability to process
                                                  Returns sent to Fusebox as
                                                  EMV transactions.\
                                                  \
                                                  Added back description of
                                                  HID USB (removed in
                                                  2.02.025). Updated ID
                                                  information for HID USB to
                                                  include Tetra devices.
                                                  Added instructions for
                                                  obtaining additional ID
                                                  information.
                                                  ([Addendum](/#00081)
                                                  only)\
                                                  \
                                                  Added timeout on PIN entry
                                                  as additional condition
                                                  for API 1010 = "\*SLR
                                                  Cancel Key Pressed."\
                                                  \
                                                  Added tag 072 under
                                                  [Informational
                                                  Prompting](#0006) to
                                                  display scrolling text
                                                  with configurable buttons
                                                  ([Addendum](/#00081)
                                                  only).

  2.02.025.1              APR 2019                Updated sample messages.\
                                                  \
                                                  Updated information on
                                                  matching fields when a
                                                  transaction depends on a
                                                  prior transaction.

  2.02.025                MAR 2019                Supported Hardware - Added
                                                  support for Tetra devices
                                                  on Version 25. Added list
                                                  of all supported Ingenico
                                                  devices.\
                                                  \
                                                  Communications - Added
                                                  support for Wifi and
                                                  Bluetooth.\
                                                  \
                                                  [Versioning](#00085) -
                                                  Added table of current
                                                  version numbers for
                                                  Simplify and supporting
                                                  software.\
                                                  \
                                                  [Message
                                                  Details](#core_concepts)
                                                  -- Added tables of
                                                  matching fields required
                                                  for transaction types
                                                  dependent on prior
                                                  transactions\
                                                  \
                                                  EMV - Corrected
                                                  description of Return
                                                  transaction using ICC chip
                                                  card to say that card must
                                                  be swiped.\
                                                  \
                                                  [Auto Signature](#00064) -
                                                  Added support for auto
                                                  signature.\
                                                  \
                                                  Signature Request Message
                                                  - Added tag 002.\
                                                  \
                                                  Initiate Ingestate Message
                                                  - Added capability for POS
                                                  to set IngEstate
                                                  identifier (TMSID).\
                                                  \
                                                  Scrolling Receipt Message
                                                  - Added capability to send
                                                  up to five lines of text
                                                  plus a total line in a
                                                  single request.\
                                                  \
                                                  EMV - Added support for
                                                  contactless EMV.\
                                                  \
                                                  EMV -- Added list of EMV
                                                  tags.\
                                                  \
                                                  EMV - Added option to
                                                  return EMV tags on a
                                                  Stand-In response.\
                                                  \
                                                  EMV - For ICC decline of
                                                  host-approved transaction,
                                                  added reason for decline
                                                  to response to POS.\
                                                  \
                                                  Pay\@Table - Added
                                                  enhancements from customer
                                                  feedback.\
                                                  \
                                                  [Informational
                                                  Prompting](#0006) - Added
                                                  tags 011, 012, 071.\
                                                  \
                                                  [Quick Chip
                                                  Tendering](#00065) - Added
                                                  support.\
                                                  \
                                                  Simplify-Generated
                                                  Response Messages - Added
                                                  additional messages.\
                                                  \
                                                  Status Message ACKing -
                                                  Made configurable the list
                                                  of Status Identifiers for
                                                  which a Status Message
                                                  require an ACK. Added 021
                                                  to the default list.\
                                                  \
                                                  Simplified-Controlled
                                                  Fields - Renamed and
                                                  rewritten. Added
                                                  subsections on API 5001
                                                  (Financial Data), 5070
                                                  (Simplify Information),
                                                  5071 (Card/Cardholder
                                                  Present?), 5104 (Tip
                                                  Prompting). Documented
                                                  Quick Chip token. Added
                                                  Quick Chip and PIN Pad
                                                  busy entries to Completion
                                                  Code table.

  2.02.021                OCT 2017                Initial Developer Portal
                                                  version
  --------------------------------------------------------------------------

Appendix I - Addendum {#00081 .h2}
---------------------

### EMV {#emv .h3}

Added ability to process Returns sent to Fusebox as EMV transactions.
Updated information on supported transaction types as follows:

Simplify supports EMV processing, both contact and contactless, for the
following Tran Types: - Auth Only (01): - Sale (02): - Return (09):

Based on settings, each supported Tran Type can be processed as either
EMV or swiped. Please contact your Elavon representative for
configuration setting.

### Simplify-Generated Messages {#simplify-generated-messages .h3}

Added timeout on PIN entry as new condition for "\*SLR CANCEL KEY
PRESSED." in API 1010. Updated description of this message as follows:

  --------------------------------------------------------------------------
  Field 1003     Field 1004     Field 1010     Condition      Action
  -------------- -------------- -------------- -------------- --------------
  208                           \*SLR CANCEL   The Cancel key Decline -- No
                                KEY PRESSED.   was pressed on Inquiry needed
                                               the PIN Pad,   
                                               or\            
                                               Timeout on PIN 
                                               entry.         

  --------------------------------------------------------------------------

### Tag 072: Scrolling Text with Configurable Buttons {#tag-072-scrolling-text-with-configurable-buttons .h3}

(\*Added under **[Informational Prompting](#0006)**\*)

Simplify supports a Scrolling Text with Configurable Buttons Message.
The Request displays a screen with scrolling text plus configurable
buttons at the bottom of the screen. This message can be used to display
a Consent screen.

Scrolling text -- Up to 100 lines of scrolling text can be defined. Font
size and justification are defined in the request. The maximum number of
characters per line depends on the font size.

Buttons -- Up to two buttons can be defined in the request. Buttons can
be on every page or only at the end, and arranged horizontally or
vertically. Button type can be push (action) or radio (Enter key
required). For radio buttons, a button can be selected by default (user
just presses Enter key) and pressing Enter without any selection can
allowed or disallowed.. The maximum length of the button descriptors
depends on the defined font size.

A field in the Response will indicate the action performed by the
customer.

Not supported on the iPP.

### **Field 5001 Format** {#field-5001-format-12 .h3}

#### Request {#request-37 .h4}

  -----------------------------------------------------------------------
  Subfield Name           Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     3                       Tag (always = 072)

  LLL                     3                       Length of the following
                                                  data

  ButLoc                  1                       Screen location of
                                                  buttons:\
                                                  0 -- At the end of the
                                                  scrolling screen\
                                                  1 -- At the bottom of
                                                  each page of the screen

  ButPos                  1                       Relative location of
                                                  buttons:\
                                                  0 -- left and right\
                                                  1 -- top and bottom

  ButScale                1                       Button scale:\
                                                  1=XXSMALL, 2=XSMALL,
                                                  3=SMALL,4=MEDIUM,
                                                  5=LARGE,6=XLARGE,
                                                  7=XXLARGE

  ButType                 1                       Button type:\
                                                  0 -- Push button
                                                  (action button)\
                                                  1 -- Radio button (must
                                                  follow with Enter key)

  RadCheck                1                       Check settings (only
                                                  used if Radio buttons
                                                  active):\
                                                  0 - No check (no
                                                  default)\
                                                  1 - Check 1st button
                                                  (left or above button
                                                  is default)\
                                                  2 - Check 2nd button
                                                  (right or below button
                                                  is default)

  RadReq                  1                       Button selection (only
                                                  used if Radio buttons
                                                  active):\
                                                  0 - Can press ENTER
                                                  without radio
                                                  selection\
                                                  1 - Radio button must
                                                  be selected when ENTER
                                                  is pressed

  FS                      1                       Field separator (Hex
                                                  1C)

  But1Txt                 (see above)             Button 1 text

  FS                      1                       Field separator (Hex
                                                  1C)

  But2Txt                 (see above)             Button 2 text

  FS                      1                       Field separator (Hex
                                                  1C)

  LblScale                1                       Label scale:\
                                                  1=XXSMALL, 2=XSMALL,
                                                  3=SMALL,4=MEDIUM,
                                                  5=LARGE, 6=XLARGE,
                                                  7=XXLARGE

  FS                      1                       Field separator (Hex
                                                  1C)

  LblAlign                1                       Label alignment:\
                                                  1=Left, 2=Center,
                                                  3=Right

  FS                      1                       Field separator (Hex
                                                  1C)

  Lbl1                    (see above)             Label 1 text

  FS                      1                       Field separator (Hex
                                                  1C)

  Lbl2                    (see above)             Label 2 text

  FS                      1                       Field separator

  ...                                             

  Lblx                    (see above)             Label x text
  -----------------------------------------------------------------------

Response

  -----------------------------------------------------------------------
  Subfield Name           Length                  Description
  ----------------------- ----------------------- -----------------------
  TTT                     3                       Tag (always = 072)

  LLL                     3                       Length of the following
                                                  data

  ActionButton/Data       var.                    If field 11 Completion
                                                  Code = 000 (success),
                                                  indicates button or key
                                                  pressed:\
                                                  1 - button 1 (button on
                                                  left or top) selected\
                                                  2 - button 2 (button on
                                                  right or bottom)
                                                  selected\
                                                  888 -- Cancel key
                                                  pressed\
                                                  Not present (LLL=000)
                                                  -- Enter key pressed
                                                  with no button selected
  -----------------------------------------------------------------------

### **Sample Message** {#sample-message-8 .h3}

#### Request {#request-38 .h4}

The following request tells Simplify to display the screen shown below
(end of first page of scrolling text is shown):

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14125072000                    User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,\[see value below\]            Non-Financial Data\
                                      072=Tag\
                                      883=Length of data\
                                      1=Screen location of buttons\
                                      1=Relative location of buttons\
                                      3=Button scale\
                                      1=Button type\
                                      1=Check settings\
                                      0=Button selection\
                                      I Agree=Descriptor for first (top)
                                      radio button\
                                      I do not agree=Descriptor for
                                      second (bottom) radio button\
                                      3=Label scale\
                                      2=Label alignment\
                                      You agree that any Services contain
                                      proprietary content,
                                      information=Text of Label 1\
                                      (etc.)
  -----------------------------------------------------------------------

#### Reponse {#reponse .h4}

  -----------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------
  0001,36                             Transaction Type

  0011,14125072000                    User Data. See [Simplify-Controlled
                                      Field Definitions](#00073).

  5001,0720011                        Non-Financial Data:\
                                      072=Tag\
                                      001=Length of data\
                                      1=Button 1 pressed
  -----------------------------------------------------------------------

### **HID USB Interface** {#hid-usb-interface .h3}

(\*Added under **Message and Communication Protocols**\*)

HID USB is a protocol that allows for serial bidirectional data transfer
in a manner similar to the serial protocol (as described in Appendix B),
but using the USB link layer. This has some advantages over "regular"
Serial, for example you don't need to specify baud rate or stop bits, as
these are not part of the USB link layer.

In general there are two ways an ECR can communicate using HID USB. The
first is via a third-party driver; this software will hide the HID
complexity and allow existing ECR software to work unmodified. However
if a direct HID USB interface is preferred, additional steps must be
taken to conform to the HID USB link layer data transfer requirements:

For Ingenico PIN Pads, the HID interface requires 32 byte frames, with
the first byte being a Report ID and the next 31 bytes available for
payload data. Extra bytes must always be padded with zeroes, as you can
never transfer less or more than a full 32 byte frame. For frames going
to the PIN Pad, the Report ID byte must be 2; when receiving data from
the PIN Pad, you can expect a Report ID byte with a value of 1. Messages
longer than 31 bytes must be transferred in multiple frames. The payload
data must still start with STX and include ETX and LRC (same as for
Visa2 transfers).

Messages received from the PIN Pad must also be filtered to skip over
both the Report ID bytes (value = 1) and any extra padding bytes (value
= 0) from the incoming data stream. This will allow the ECR to interpret
messages received from the PIN Pad. Special care must be taken in
locating the LRC byte when processing incoming data. It's not
necessarily the byte following the ETX, as that byte might be a Report
ID. Also, the LRC byte can have any value (including 1) so it's not
sufficient to simply ignore a "1" byte after the ETX. The correct
algorithm keeps track of how many bytes into the frame it is,
identifying the Report ID byte by its position (i.e. at the start of the
frame), not its value.

HID USB protocol also includes the concepts of Interface and Endpoint.
In this implementation, there is only one Interface (0) and two
endpoints:\
Telium 2 terminals: ENDPOINT\_OUT (0x04) and ENDPOINT\_IN (0x85).\
Tetra terminals: ENDPOINT\_OUT (0x02) and ENDPOINT\_IN (0x81).

The endpoint information can be obtained from a Windows utility (e.g.
the Simplify POS simulator).

To connect to a HID USB terminal, an application must know the Vendor ID
and Product ID values. For Ingenico PIN Pads, the following table (see
next page) shows the model name, the VID and the PID for each supported
hardware model:

  TERMINAL    VID      PID      String               Class
  ----------- -------- -------- -------------------- -------
  iPP320      0x0B00   0x0071   Ingenico iPP320      HID
  iPP350      0x0B00   0x0072   Ingenico iPP350      HID
  iSC480      0x0B00   0x0073   Ingenico iSC480      HID
  iSC250      0x0B00   0x0074   Ingenico iSC250      HID
  Lane/7000   0x0B00   0x6780   Ingenico Lane 7000   HID

If the VID and PID is not on the above list, they can be obtained by the
following procedure:

#### **To obtain the VID and PID from a Windows PC:** {#to-obtain-the-vid-and-pid-from-a-windows-pc .h4}

1\) Connect the PIN Pad to the PC. Open the "Device Manager", look for
"Human Interface Devices" 2) Under "Human Interface Devices",
Right-click on the "HID-compliant device" or "USB Input Device", select
"Properties". The properties dialog box will be displayed. 3) Select the
"Details" tab on the Properties dialog box.\
4) Open the "Property" drop-down list and select "Hardware IDs". 5) In
the "Value" text box, look for string "VID\_0B00"

6\) Next to the "VID\_0B00", you will find the "PID" value in the format
of "PID\_xxxx". 7) If the VID is not "0B00", it is not an Ingenico
device. Go to Step 2 and choose another device.

::: {#support}
:::

#### Ingenico Download Configuration and Troubleshooting Guide 2.02.024-025 {#ingenico-download-configuration-and-troubleshooting-guide-2.02.024-025 .h1}

Introduction {#introduction .h2}
------------

The purpose of this guide is to provide information on configuring
Simplify, downloading files and troubleshooting.

The document is distributed with the application and available to the
customer on request. It is reviewed for every application update and
change to [PCI P2PE]{.tooltip tooltip-content="#PCIP2PE"
style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}
requirements (at least annually) and updated as required.

Overview {#overview .body-text}
--------

Simplify is an application that resides on the PIN pad that works
together with a POS application to process electronic payment
transactions. Authorization requests are sent directly from the PIN pad,
which simplifies PCI-DSS compliance. EMV and Pay\@Table are supported.

Simplify can be integrated into a POS system by following the
instructions in the [Simplify Developer Guide](#overview).

This document covers implementations of Simplify that operate as
follows:

-   Simplify runs on Ingenico Telium or Tetra PIN pads, using Voltage or
    On-Guard encryption

-   Simplify is programmed to send transactions directly to Elavon's
    Fusebox Gateway

Supported Features {#supported-features .h2}
------------------

  ----------------------------------- -----------------------------------
  Supported tender types:             • Credit\
                                      • Debit\
                                      • Gift Card

  EMV                                 Supported in U.S and Canada.
                                      (Interac not supported)

  Pay\@Table                          Supported in U.S. and Canada. (For
                                      all supported tender types.)

  Supported transaction types:        • Authorization Only; Tokenization
                                      supported\
                                      • Sale; Tokenization supported\
                                      • Prior-Authorized Sale
                                      \[Completion\]\
                                      • Return\
                                      • Void Sale\
                                      • Transaction Inquiry\
                                      • Gift Card\
                                      • Request for Token\
                                      • Full Authorization Reversal\
                                      • Incremental Authorization\
                                      • Void Return\

  Additional supported features:      Card Entry:\
                                      • Swiped\
                                      • Key-entered\
                                      • Contactless magstripe emulation\
                                      • Contact or contactless EMV\
                                      Application download: via
                                      IngEstate\
                                      Communications between POS and
                                      Simplify:\
                                      • TCP/IP\
                                      • RS-232 (including USB emulation)\
                                      Communication to Fusebox\
                                      • TCP/IP -- Encrypted based on
                                      Fusebox security requirements\
                                      • Fusebox certificate\
                                      Configuration using Elavon Menu\
                                      Voltage or On-Guard End to End
                                      Encryption\
                                      Signature Capture\
                                      Scrolling Receipt\
                                      Status Message to the POS\
                                      Batch Close Support
  ----------------------------------- -----------------------------------

Navigation and Data Entry on Ingenico PIN Pads {#navigation-and-data-entry-on-ingenico-pin-pads .h1}
==============================================

The chapter describes the techniques used to configure Simplify Telium
or Tetra PIN Pads. Accessing Elavon configuration, selecting menu items,
scrolling and entering dots are described separately for touchscreen
models (ISCxxx) and non-touchscreen models (iPPxxx, iWL250, iSMP4).
Additional comments concerning Elavon setup menus and data entry screens
apply to all models.

Touchscreen Models {#touchscreen-models .h2}
------------------

-   **Accessing the Elavon Sub Menu**

    Reboot the PIN Pad by pressing the Clear and minus (--) keys. The
    Elavon Sub Menu can be accessed during bootup whenever a white
    circle in a green rectangle is present in the lower right corner of
    the screen. To display this menu, touch this white circle or press
    the **Enter** (green) key.

-   **Using Elavon Menus**

    A menu item can be selected by touching the item or by scrolling to
    the item using the plus (+) or minus (--) keys and pressing the
    **Enter** (green) key.

    If a scroll bar appears in the lower right corner, additional
    parameters are available after the first screenful. These items can
    be made visible by scrolling as described above or by dragging the
    scroll bar.

-   **Entering Dots**

    To type a dot on data entry screens, use the minus (--) key.

Non-Touchscreen Models {#non-touchscreen-models .h2}
----------------------

-   **Accessing the Elavon Sub Menu**

    Reboot the PIN Pad by pressing the Clear and .,\#\* keys until a
    happy face appears in the upper left corner of the screen. The
    Elavon Sub Menu can be accessed by pressing the **Enter** (green)
    key during bootup whenever a rectangle is present in the lower right
    corner of the screen. On the iPP350, this rectangle is a white
    circle on a green background. On the iPP320, this rectangle appears
    as follows:

-   **Using Elavon Menus**

    A menu item can be selected by keying the item number or by
    scrolling to the item and pressing the **Enter** (green) key. The up
    and down keys are used for scrolling.

    If a scroll bar (iWLxxx) or arrow (IPPxxx) appears in the lower
    right corner, more parameters are available after the first screen.
    These items can be made visible by scrolling as described above.

-   **Entering Dots**

    To type a dot on data entry screens, use the .,\#\* key.

-   **Timeout**

    To save battery life, iWLxxx screens timeout after a 60 second idle.

All Models {#all-models .h2}
----------

-   **Using Elavon Setup Menus**

    Each parameter name is followed by a colon (:) followed by the
    current value of the parameter. E.g. **DHCP:0**

    When a setup menu is displayed, the first parameter on the screen is
    selected by default.

    If the value of a Simplify parameter is changed, the re-displayed
    setup menu displays the updated value.

    Pressing the **Cancel** (red) key returns to the **Elavon Main
    Menu** without changing anything.

-   **Using Elavon Data Entry Screens**

    All data entry screens accessed through the **Elavon Main Menu**
    initially display the current value of the parameter. This value is
    automatically overwritten by any entered data.

    Pressing the **Enter** (green) key saves the entered data and
    displays the updated setup menu.

    Pressing the **Cancel** (red) key discards any change and
    re-displays the setup menu.

    Pressing the **Clear** (yellow) key deletes the last character
    entered on this screen. Pressing the **Clear** key again will delete
    additional characters from the right, one character at a time.

    To enter a letter on the PIN pad, key in the applicable number
    (example: 2 for A, B or C) and repeat quickly to toggle through its
    associated letters.

Configuring Simplify {#configuring-simplify .h1}
====================

The **Elavon Main Menu** is used to configure Simplify. This menu is
available on all Simplify Telium or Tetra PIN pads. This chapter
describes:

-   Accessing the Elavon Menu

-   Network Setup

-   Host Setup

-   POS Setup

-   Terminal Setup

-   Wireless

    -   Wifi Setup

    -   Bluetooth Setup

-   Status Bar

-   Enabling Configuration Changes

::: {.notices .note}
<div>

**Note:**

-   Unless stated otherwise, all screenshots shown under "Configuring
    Simplify" are taken from the following devices:

    -   Move 5000 for Wireless and its submenus.
    -   iSMP4 for all other menus.

-   All values displayed are samples. Contact your network administrator
    for the values required on your system.

\

Accessing the Elavon Main Menu {#accessing-the-elavon-main-menu .h2}
------------------------------

To access the **Elavon Main Menu:**

1.  Once this rectangle appears, press the **Enter** (green) key to
    display the **Elavon Sub Menu** (see below).\
    The Elavon Sub Menu can be accessed whenever this rectangle is
    displayed during the boot up sequence. This menu provides access to
    IngEstate (see Initiating IngEstate) and the **Elavon Main Menu**.\
    \
    For systems that support Point to Point Protocol (PPP)
    communications, the Elavon Sub Menu will contain a third entry,
    Disable PPP Session (see below). This selection will temporarily
    disable PPP functionality, which will allow PIN Pad maintenance to
    be performed through an IP connection. PPP functionality will be
    restored following the next reboot.\
    \
    **Note:** the above screenshot was taken on an iPP320.

2.  Select **Elavon Main Menu** to display the login screen for this
    menu.\

3.  Use the login screen to type in the Elavon password. The **Elavon
    Main Menu** will display.\
    \

4.  To display a Setup screen, select the item from the **Elavon Main
    Menu**. When done with this menu, Restart can be used to restart the
    PIN Pad.

5.  Additional items are available at the end of this menu.\

::: {.notices .important}
<div>

**Important**: The Voltage encryption key should only be rotated when
instructed to do so by the Elavon Help desk.

</div>
:::

::: {.notices .note}
<div>

**Note:**

-   **Telium Manager** displays the initial screen for Ingenico's Telium
    Manager. For more information, refer to Ingenico documentation.

-   **Renew Voltage Key** rotates the Voltage encryption key.

-   On Wireless-capable PIN Pads, there is an additional menu item,
    **Wireless**. This is located between **Telium Manager** and **Renew
    Voltage Key**, and provides access to **Wifi Setup** and **Bluetooth
    Setup**.

</div>
:::

Network Setup {#network-setup .h2}
-------------

Simplify supports Ethernet as the network type. Ethernet communications
on the Telium or Tetra can be configured under **Network Setup**. As
described below, the use of this menu is controlled by the setting of
0-DHCP.

**Access Network Setup**

1.  Select Network Setup on the Elavon Main Menu to display the
    following menu.\
    \

2.  Scroll down to display more items.

**Available Parameters**

**DHCP:**

View/modify whether DHCP is enable/disabled. Set by Elavon prior to
shipping Simplify, based on the customer's network requirements.
Controls how Network Setup parameters are defined:

-   If set to 1: DHCP will be enabled (IP mode = DHCP). The values of
    other Network Setup parameters will be defined by the DHCP server
    and read-only under Network Setup.

-   If set to 0: DHCP will be disabled (IP mode = Static). The values of
    other Network Setup parameters will be displayed under Network Setup
    and available for editing.

**IP:**

View IP Address (and modify if allowed). Must be unique value; cannot be
shared with anything else on the network.

**NTM:**

View Netmask (and modify if allowed).

**Gateway:**

View Gateway (and modify if allowed).

**DNS1:**

View primary DNS server address (and modify if allowed). If IP: is
defined as a symbolic name, DNS1: must be defined.

**DNS2:**

View secondary DNS server address (and modify if allowed). Backup for
DNS1

Host Setup {#host-setup .h2}
----------

The **Host Setup** menu displays the current values of parameters
required for host communications. Most parameters on this menu are
read-only. This menu can be used as follows:

**Access Host Setup**

1.  Select Host Setup on the Elavon Main Menu to display the following
    menu:\
    \
    \
2.  Scroll down to display more items.\

**Available Parameters**

**IP:**

View the IP address of the Fusebox gateway.

**PORT:**

View the Fusebox port that communicates with Simplify.

**SECURED:**

View whether or not communications with Fusebox are encrypted. (0=No,
1=Yes)

**METHOD:**

View encryption type used for communications with Fusebox.

**TMS ID:**

View/modify the TMS identifier. This is an IngEstate locator value
assigned to the PIN Pad by Elavon. This value must only be changed on
instructions from Elavon, using the Elavon-supplied value.

POS Setup {#pos-setup .h2}
---------

The POS Setup menu displays/defines parameters required for Simplify-POS
communications and other POS-related parameters. The contents of this
menu vary depending on communications type. There are three versions,
used for:

-   IP communications with Simplify as server (non-Pay\@Table systems)

-   IP communications with Simplify as client (Pay\@Table systems)

-   RS-232 communications or USB emulating RS-232

The appropriate menu for your system will be displayed, based on the
setting of the parameter that controls the Simplify-POS communications
type.

### IP Communications, Simplify as Server {#ip-communications-simplify-as-server .h3}

In non-Pay\@Table systems, Simplify acts as TCP/IP server. POS Setup can
be used on these systems as follows:

**Access POS Setup**

1.  Select **POS Setup** on the Elavon Main Menu to display the **Client
    IP** Setup menu:\
    \

**Available Parameters**

**Port:**

View/modify port ID on which the POS Server listens for the Simplify
client.

**Secured:**

View whether or not Simplify-POS communications are encrypted. (0 = No
encryption, 1 = Encryption)

**Method:**

View encryption type used for Simplify-POS communications. (1=SSLv2;
2=SSLv3; 3=TLSv1; 4=SSLv23; 5=TLSv1.1; 6=TLSv1.2)

### IP Communications, Simplify as Client {#ip-communications-simplify-as-client .h3}

In Pay\@Table systems, Simplify acts as a TCP/IP client. POS Setup can
be used on these systems as follows:

**Access POS Setup**

::: {.notices .note}
::: {.body-text}
**Note:** the following screenshot was taken from an iWL250 PIN Pad.
:::
:::

1.  Select POS Setup on the Elavon Main Menu to display the POS Setup
    menu.\
    \

2.  Additional items are available by scrolling down:

**Available Parameters**

**0-IP:**

View/modify IP Address of the POS.

**1-Port:**

View/modify port ID on which the POS Server listens for the Simplify
client.

**2-Persist:**

View/modify persistence of the Simplify-POS link. (0 = Non-persistent, 1
= Persistent)

**3-Store:**

View/modify the Store Number.

**4-Font:**

View/modify the Font Size for receipts. (1 = XXSMALL; 2 = XSMALL; 3 =
SMALL; 4 = MEDIUM; 5 = LARGE (the default); 6 = XLARGE; 7 = XXLARGE)\
If a receipt field does not fit on one line using the defined font, it
will wrap around to print on multiple lines.

**5-Secured:**

View whether or not Simplify-POS communications are encrypted. (0 = No
encryption, 1 = Encryption)

**6-Method:**

View encryption type used for Simplify-POS communications. (1=SSLv2;
2=SSLv3; 3=TLSv1; 4=SSLv23; 5=TLSv1.1; 6=TLSv1.2)

### RS-232 Communications (or USB Emulating RS-232) {#rs-232-communications-or-usb-emulating-rs-232 .h3}

On systems using RS-232 Communications or USB Emulating RS-232, POS
Setup can be used as follows:

**Access POS Setup**

::: {.notices .note}
**Note:** the following screenshot was taken from an iPP320 PIN Pad.
:::

1.  Select POS Setup on the Elavon Main Menu to display the POS Setup
    menu:\
    \

2.  Additional items are available by scrolling down:

**Available Parameters**

**0-Port:**

ID of the POS COM port that communicates with the PIN Pad. 3 = RS-232.
10 = USB emulating RS-232.

**1-Baud:**

Speed used for Simplify-POS communications.

**2-Databit:**

Number of bits in each byte that are used to transmit data. This value
should be set to 8 (the default).

**3-Parity:**

Type of check bit used to detect corrupted data. This value should be
set to N =no parity (the default).

**4-Stopbit:**

The number of bits in the end-of-text marker. This value should be set
to 1 (the default).

**5-v4683:**

Two-byte retry parameter. Byte 1 defines the number of retries. Byte 2
defines the interval between retries (in seconds). Change only upon
instruction from Elavon.

Terminal Setup {#terminal-setup .h2}
--------------

The Terminal Setup menu displays the current values of parameters used
in the operation of the PIN Pad, excluding communications parameters.
Most parameters shown in this menu are read-only. This menu can be used
as follows:

**Access Terminal Setup**

1.  Select Terminal Setup on the Elavon Main Menu to display the
    Terminal Setup menu.\
    \

2.  Scroll down to display more items.

**Available Parameters**

**MerchLang:**

View the Merchant Preferred Language. (0=English. 1=French)

**AllowedLang:**

View available languages. (en = English. fr = French. enfr =
English/French. fren = French/English). This parameter is used for EMV
and Pay at the Table transactions, as follows:

-   EMV -- A list of Customer Preferred Languages is read from the EMV
    card and compared with the value(s) in **AllowedLang**. The tender
    will be processed using the first match between Customer Preferred
    Language and **AllowedLang**. If there is no match, the Merchant
    Preferred Language will be used.

-   Pay\@Table -- For transactions in Canada: After Pre-Pay server
    interaction, the customer will be prompted to select a language to
    be used for customer interaction (through receipt printing). The
    available languages in this prompt are defined by **AllowedLang**.

**Currency:**

View the default currency. (USD840 = US\$; CAD124 = Canadian \$) The
seventh byte defines the number of currency decimal places.

**DateFormat:**

View the format used for dates.

**Date:**

View/modify the PIN Pad's internal date.

**Time:**

View/modify the PIN Pad's internal time.

**Associate Base:**

Renew PINpad/base association. (Only available on the iWL250.) After
selecting Associate Base, a message will be displayed indicating the
result of the attempted re-association.

Wireless {#wireless .h2}
--------

Simplify supports Wifi and Bluetooth communications. The Elavon Main
Menu allows users to configure wireless communications.

-   Wifi can be used to communicate with the POS, Fusebox and Ingestate.

-   Bluetooth can be used to communicate with the POS.

**Access Wireless Setup**

1.  Access the Elavon Main Menu as described under Accessing the Elavon
    Main Menu:\

2.  Scroll down until Wireless is displayed. Select this menu item to
    display Wireless Setup:\

3.  Select Wifi Setup or Bluetooth Setup, based on the setup you wish to
    perform.

### Wifi Setup {#wifi-setup .h3}

Select Wifi Setup from the Wireless Setup menu to display the Wifi Setup
menu:\
\

**Available Configuration**

**Disable/Enable**

**Scan networks**

**Advanced Options**

Selecting this button will provide access to the following functions:

**My Networks**\

This button allows the user to manage configured networks, as follows:

**Force use**\

**Remove**\

**Update**\

Select to modify this network definition as follows:

**Access Point Visibility**\

**Security Type**\

**Wifi Password**\

**Connect**\

**IP configuration**

**Default IP Configuration**\

**Active Roaming**\

**SSID Status**\

### Bluetooth Setup {#bluetooth-setup .h3}

Select Bluetooth Setup from the Wireless Setup menu to display the
Bluetooth Setup menu:\
\

**Available Configuration**

**1-Disable/Enable**

**2-Pair with phone**

**3-Add device**

**4-Paired devices**

**5-Advanced Options**

Status Bar {#status-bar .h2}
----------

Pin Pad status is displayed in a status bar at the top of Simplify
screens, when appropriate. A sample status bar is as follows:

The Status Bar contains the following information:

-   Bluetooth indicator

-   Ethernet indicator

-   Wifi indicator

-   Battery indicator

Enabling Configuration Changes {#enabling-configuration-changes .h2}
------------------------------

Configuration changes made under the **Elavon Main Menu** can be enabled
as follows:

1.  From any Elavon setup menu, select **Main Menu** to return to the
    **Elavon Main Menu**.

2.  Select **Restart** on the **Elavon Main Menu** to restart the PIN
    Pad application.

3.  Allow the application to run until completion.

Terminal Maintenance {#terminal-maintenance .h1}
====================

IngEstate is Ingenico's Terminal Management System. Elavon maintains an
IngEstate server to update Simplify PIN pads. This chapter explains how
PIN Pads are maintained.

Signed Sensitive Files {#signed-sensitive-files .h2}
----------------------

For purposes of security, sensitive Simplify files are signed. Unsigned
sensitive files, or files signed with a different certificate, will not
be accepted by the PIN Pad. If this occurs, a signing error message will
be displayed after the file is loaded to the PIN Pad. The merchant will
then need to contact Elavon.

Initiating IngEstate {#initiating-ingestate .h2}
--------------------

The IngEstate update process can be initiated manually on the PIN Pad,
by command from the POS (see Simplify Developer Guide) under "Initiate
Ingestate Message" for details) or scheduled by Elavon. Once initiated,
the process proceeds automatically.

The IngEstate update process can be initiated manually from the
**Elavon** **Sub Menu**. As described under Accessing the Elavon Main
Menu, this menu can be accessed during the PIN pad boot up sequence.
(See Navigation and Data Entry on Ingenico PIN Pads for device-specific
details.)

Select **Initiate Ingestate** to initiate the IngEstate update process.

Viewing Simplify Load Information {#viewing-simplify-load-information .h2}
---------------------------------

Information on the Simplify load present in the PIN pad is displayed
during boot up and by keying 0 when the PIN pad is in a closed state.
(To lengthen the display, press the + or -- key.) For additional fields,
scroll down. This information may be requested by Elavon for
troubleshooting purposes. The PIN pad will return to the usual closed
screen after several seconds.

The fields on this screen will vary by implementation. The list gives a
sample of the available fields:

Simplify\
Serial: 80498883\
TMS ID: 12345678\
Vers: N-OG-2.02.02504\
Package: 2.25.1\
IP Addr: xx.xxx.xxx.34\
Merchant: Elavon\
Client: TCP Clnt Non-SSL-6000 08/19/18 - 13:46:18\
Base 2.25.1\
EMVCert: 2.25\
EmvKernel: EMVDC0838\
ParmVer: 2.25.1\
TndrVer: 2.25.1\
EMVParm: EMVPARM-E4-1\
ClessParm: CLESSEMV\
TSA Serial: 2214180SC010031 SDK Ver: 11.16.07.Patch G ScrSaver: 0\
RKI\
Device: Lane 5000 Flash Memory: 50332\
Flash Free Code: 396197 Flash Free Data: 396197\
RAM Memory: 518279\
RAM Memory Free: 427438 PosIP Acpt Active

::: {.notices .note}
<div>

**Note:** The **IP Addr** field initially displays the partially masked
IP Address of the PIN Pad. An optional feature is available allowing
this field to display the unmasked address. If this feature is present,
pressing Enter at the load information screen will display a login
screen. After logging in on this screen (special password required), the
load information screen will be redisplayed with the IP Address
unmasked. Please contact your Elavon representative if you want to
implement this feature.

</div>
:::

The above fields provide the following information:

  -----------------------------------------------------------------------------------------------------------------------------------
  Field                               Description
  ----------------------------------- -----------------------------------------------------------------------------------------------
  Serial:                             PIN Pad L3 Serial Number

  TMS ID:                             TMS Identifier

  Vers:                               Simplify version, build and implementation information:\
                                      \
                                      Format is S--PP-X.YY.ABBCC, where:\
                                      \
                                      S = first part of prefix, indicates whether Simplify is operating as part of a [PCI
                                      P2PE]{.tooltip tooltip-content="#PCIP2PE"
                                      style="font-family: 'Roboto Medium', sans-serif; line-height: 24px;color:#417505;"}-validated
                                      solution.\
                                      (Optional. If not present, solution is not validated.)\
                                      \
                                      PP = second part of prefix, indicates encryption type.\
                                      \
                                      X.YY.ABBCC = Simplify version and build information\
                                      \
                                      For more information, see [Simplify Developer Guide](#overview) under
                                      [](#00085)[Versioning](#00085).\
                                      \

  Package:                            ID of package used to build current load

  IP Addr:                            Masked IP address of PIN Pad (see note above for viewing the unmasked IP address)

  Merchant:                           Customer for whom load was built

  Client:                             POS Communications type and port

  (Date/Time)                         Current date/time

  Base                                ID of first package sent to POSPortal for this customer

  EMVCert:                            EMV version

  EmvKernel                           EMV Kernel version

  ParmVer:                            parm version

  TndrVer:                            tenderdef version

  EMVParm:                            EMVParm version

  ClessParm:                          ClessEMV (or ClessMSD) version

  TSA Serial:                         PIN Pad L4 Serial Number

  SDK Ver:                            SDK version

  ScrSaver:                           Screen Saver group ID

  RKI                                 Status of last Remote Key Injection file download

  Device                              PIN Pad model

  Flash Memory:                       Total Flash memory in PIN Pad

  Flash Free Code:                    Unused Flash code space

  Flash Free Data:                    Unused Flash data space

  RAM Memory:                         Total RAM memory in PIN Pad

  RAM Memory Free:                    Unused RAM memory

  PosIP Acpt                          Status of Simplify-POS IP connection
  -----------------------------------------------------------------------------------------------------------------------------------

Remote Key Injection {#remote-key-injection .h2}
--------------------

Simplify supports Remote Key Injection (RKI). This section documents how
to determine the outcome of an attempted key injection. For more
information on RKI, consult your Elavon representative.

When the PIN Pad restarts after an attempted key injection, RKI messages
will be displayed during the bootup sequence. The first RKI message will
always be as follows:

This message will be followed by a second RKI message indicating the
outcome of the attempted injection. There are three possible scenarios:

-   If the RKI file downloaded to the PIN Pad is invalid, the following
    error message will be displayed:\
    \

-   If the RKI file is valid, but the serial number in the file does not
    match that in the PIN Pad, an error message will be displayed
    showing the L4 serial number of the PIN Pad. E.g.:\
    \

-   If the key injection is successful, the following message will be
    displayed:\
    \

Exiting Reversal Mode {#exiting-reversal-mode .h2}
---------------------

The host approval will need to be reversed when either of the following
situations occur:

-   An EMV transaction is approved by the host and declined by the chip.

-   The customer removes their card from the chip reader before the
    transaction is completed.

If a reversal is needed, Simplify will go into reversal mode to force
the reversal. It does this by sending a reversal (Tran Type 11) to the
host, and resending the reversal (if necessary), until a response is
received. While this is taking place, any other transactions that are
sent to the PIN pad will be processed offline.

The PIN pad can be rebooted and commanded to exit reversal mode from the
**Elavon Main Menu**, as follows:

1.  Reboot the PIN pad. When a rectangle appears in the lower right
    corner of the screen, press the **Enter** (green) key to display the
    **ELAVON SUB MENU**.

2.  Select **Elavon Main Menu** and login to display this menu.

3.  Scroll down and select **REMOVE EMV REVERSAL** (only present if
    currently in reversal mode).

4.  Select **RESTART** to reboot the PIN pad.

If Simplify is forced out of reversal mode, the data required to request
the reversal is sent to the POS in a **Void Transaction Response** (11)
message, after which the PIN pad returns to normal processing mode.

::: {.notices .important}
<div>

**Important**: Forcing Simplify to exit reversal mode is an exception
procedure that should only be used when necessary. If Simplify is forced
out of reversal mode, the merchant will be responsible for ensuring that
the transaction is reversed by the host, using the data in the **Void
Transaction Response**. Elavon strongly recommends allowing Simplify to
reverse all host-approved transactions that are declined by the chip.

</div>
:::

Troubleshooting {#troubleshooting .h1}
===============

This chapter describes the following:

-   TCP/IP Comm Error Codes

-   IngEstate Connection Errors

See also [Simplify Developer Guide](#0001) under [Simplify-Generated
Messages](#0009).

TPC/IP Comm Error Codes {#tpcip-comm-error-codes .h2}
-----------------------

  Error Code   Condition                       Resolution
  ------------ ------------------------------- ------------------------------------------------------
  -1           TCP connection failed.          Verify firewall and DNS settings for host connection
  -2           TCP connection timeout.         Verify firewall and DNS settings for host connection
  -3           TCP address is not reachable.   Verify firewall and DNS settings for host connection

IngEstate Connection Errors {#ingestate-connection-errors .h2}
---------------------------

  -----------------------------------------------------------------------
  Status Flag (36-07      Condition               Resolution
  Response)                                       
  ----------------------- ----------------------- -----------------------
  Initial connection                              
  attempt                                         

  01                      PIN pad busy            Retry

  02                      Comm error              • Verify that your
                                                  firewall is configured
                                                  to allow encrypted
                                                  traffic to the
                                                  IngEstate server.
                                                  Please contact your
                                                  Elavon representative
                                                  to verify IngEstate
                                                  communication
                                                  parameters.\
                                                  • Verify that the
                                                  addresses of your DNS
                                                  servers are correctly
                                                  defined using the
                                                  Elavon menu (DNS 1 and
                                                  DNS 2 fields under
                                                  Network Setup)\
                                                  • Verify your DNS
                                                  server can handle the
                                                  configured server name\
                                                  • If the problem cannot
                                                  be resolved, contact
                                                  your Elavon
                                                  representative

  (no response)           (Unknown)               Same as for 02

  Unable to connect after                         
  successful connection                           

  01                      PIN pad busy            Retry

  02                      Comm error              • Verify your firewall
                                                  settings\
                                                  • If the problem cannot
                                                  be resolved, contact
                                                  your Elavon
                                                  representative

  (no response)           Unknown                 Same as for 02
  -----------------------------------------------------------------------

Appendices {#appendices .h1}
==========

This chapter contains the folowing appendices:

Appendix A - Revision History

Appendix B - Usage

Appendix A - Revision History {#appendix-a---revision-history .h2}
-----------------------------

::: {.notices .note}
::: {.body-text}
\*\*Note:\*\* This documentation applies to Simplify version 2.02.024
builds 35 and higher, and version 2.02.025 all builds.\|
:::

\
:::

  -----------------------------------------------------------------------
  Document\               Date                    Revision Notes
  Revision                                        
  ----------------------- ----------------------- -----------------------
  2.02.025.3              JUN 2019                Changed references to
                                                  Telium PIN Pads to
                                                  refer to Telium and
                                                  Tetra.

  2.02.025.2              MAY 2019                (No changes)

  2.02.025.1              APR 2019                (No significant
                                                  changes)

  2.02.025                MAR 2019                Initial Developer
                                                  Portal version
  -----------------------------------------------------------------------

Appendix B - Usage {#appendix-b---usage .h2}
------------------

Note concerning usage in this document:

-   This guide will refer to POS / PMS as POS only.

</div>
:::
