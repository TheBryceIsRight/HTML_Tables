---
description: Simplify Documentation Guide
title: Simplify Migration
---

<div>

#### Simplify Ingenico Developer Guide 2.02.024-025 {#simplify-ingenico-developer-guide-2.02.024-025 .h4}

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
update and change to PCI P2PE requirements (at least annually) and
updated as required.

See
[Usage](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c01/../../book/c12/s08/c12s8.html){.highlight}
for conventions used in this document.

See
[Addendum](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c01/../../book/c12/s09/c12s9.html){.highlight}
for material added since the initial Developer Portal release for this
version of Simplify.

</div>

Supported Hardware {#supported-hardware .h2}
------------------

Supported Telium Devices: - ipp320 - iPP350 - iSC250 - iCS480 - iSMP4 -
iWL2xx

New for Version 25: - Tetra Lane 3000 - Tetra Lane 5000 - Tetra Lane
7000 - Tetra Link 2500 - Tetra Move 5000

General Guidelines {#general-guidelines .h2}
------------------

POS development for Simplify should be based on the following set of
principles:

1.  PCI DSS Compliance: The customer is responsible for securely
    deleting the encrypted account data and making it unrecoverable
    after authorization using a method that supports PCI DSS secure
    delete standards (*PCI DSS 3.0 Requirement 3.2*).

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
    processing by the POS. See [Stand-in
    Processing](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c01/s01_general_guidelines/../../../book/c03/c03_stand-in_processing.html){.highlight}
    for more information.

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

Message and Communications Protocols {#message-and-communications-protocols .h2}
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

[Appendix
B](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c01/s02_message_and_communications_protocol/../../../book/c12/s02_appendix_b_simplify_rs-232_communication_protocol/c10_s02.html){.highlight}
describes the Simplify RS-232 communication protocol.

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

Versioning {#versioning .h2}
----------

The Simplify versioning scheme (from 2.02.021 on) includes a two-part
prefix (S-PP below) indicating: (1) whether Simplify is operating as
part of a PCI P2PE-validated solution, and (2) the encryption type. The
prefix for a validated solution using On-Guard will be V-OG. Versions
with any other prefix will be non-validated.

The Simplify versioning implemented will be as follows:

  -----------------------------------------------------------------------
  Element                 Data Type               Description
  ----------------------- ----------------------- -----------------------
  S                       alphanumeric            Elavon enterprise
                                                  implementation type
                                                  (PCI P2PE-validated
                                                  solution indicator)\
                                                  V = validated\
                                                  Missing or any other
                                                  value = non-validated

  PP                      alphanumeric            Encryption type used by
                                                  application:\
                                                  OG = On-Guard\
                                                  G2 = Voltage

  X                       numeric                 Major Version\
                                                  Example: X was
                                                  incremented to 2 when
                                                  EMV support was added.

  YY                      numeric                 Minor Version. Changes
                                                  that affect
                                                  architecture or
                                                  security.

  ABBCC                   numeric                 Build release\
                                                  A: 0-4: Only used for
                                                  On-Guard
                                                  implementations.\
                                                  5-9: Only used for
                                                  Voltage
                                                  implementations.\
                                                  BB: Feature changes
                                                  that do not affect
                                                  architecture or
                                                  security.\
                                                  CC: Sequential build
                                                  number for IngEstate
                                                  control. No impact on
                                                  functionality. For bug
                                                  fixes or adjustments.
  -----------------------------------------------------------------------

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

Message Details {#message-details .h1}
===============

This chapter provides details on message types sent between Simplify and
the POS. These messages follow the Elavon Gateway API as specified in
the [Fusebox Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}.
The chapter covers both Financial Messages and Non-Financial Messages
(Tran Type 36). For additional information on Financial Messages, see
the Fusebox industry guides. Message samples in this chapter do not
include EMV fields; please refer to the EMV chapter for more
information.

Guidelines for Handling Financial Messages {#guidelines-for-handling-financial-messages .h2}
==========================================

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
    [Fusebox Integration
    Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s2agenglfin/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight},
    including the rules for POS data code (API field 47).

5.  Fields 13 (date) and 14 (time) are required in all financial
    requests.

6.  Elavon recommends not padding Field 7 (Transaction ID / Reference
    Number) with leading zeros. Elavon recommends presenting this field
    in the same manner in all messages.

7.  The messages in this document are basic samples. The POS should be
    able to handle any additional API fields in the response as defined
    in the [Fusebox Integration
    Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s2agenglfin/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}
    under "API Reference".

8.  If a Void Request needs to be re-sent, it should be sent without
    modification until a Host Response is received.

9.  If a voice auth transaction is sent to Simplify without an account
    number or a token in field 3, Simplify will prompt for account data.
    The operator verifies that the account data for which voice auth was
    obtained matches that entered at the PIN Pad.

10. Elavon recommends sending API 5071 in all financial requests, using
    the value that reflects the actual transaction environment. See
    under [Simplify-Controlled Field
    Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s2agenglfin/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

11. The value in field 0007 (Transaction ID / Reference ID) is
    incremented by the POS for each new transaction.  

\

Sale Message (Tran Type 02) {#sale-message-tran-type-02 .h2}
---------------------------

Simplify supports a Sale message from the POS process.

Request

The following table shows an example of a Sale Request message (from the
POS to Simplify).

  API Field \#, Value   Description
  --------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,02               Transaction Type
  0002,1.00             Transaction Amount
  0007,55               Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s01_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519           Transaction Date (current date)-- MMDDYY
  0014,105007           Transaction Time (current time) -- HHMMSS
  0017,0.00             Cash Back Amount
  0109,Term02           Terminal ID (provided by Elavon)
  0110,205              Cashier ID
  0201,0.00             Tip Amount
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s01_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s01_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,ONGUARD          Location Name (provided by Elavon)
  8006,TSTLA3           Chain Code (provided by Elavon)

### Response {#response .h3}

The table below is an example of a Sale Response message (from Simplify
to the POS).

\

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,02                             Transaction Type

  0002,1.00                           Transaction Amount

  0003,ID:4476082153699999            Account Token (returned by Fusebox)

  0004,0119                           Expiration Date (MMYY)

  0006,419039                         Authorization Code (returned by Fusebox)

  0007,55                             Transaction ID / Reference Number

  0009,001                            Fusebox -- Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s01_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                         Transaction Date (current date) -- MMDDYY

  0014,105007                         Transaction Time (current time) -- HHMMSS

  0017,0.00                           Cash Back Amount

  0030,1                              Fusebox -- Online Indicator

  0032,022519                         Fusebox -- Authorization Transaction Date

  0033,135016                         Fusebox -- Authorization Transaction Time

  0035,5245                           Validation Code

  0036,018031513501628                Host Transaction Identifier

  0037,0                              Fusebox - Authorizer

  0043,117595                         System Trace Audit Number

  0047,M;1;1;1;0;1;2;5;4;1;3;C;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator (0 = contact; 2 = contactless; 5 = swiped)

  0054,90                             POS Entry Mode

  0062,154                            Service Code

  0109,TERM02                         Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,400                            Fusebox -- Processor ID

  0115,010                            Transaction Qualifier (010 = credit; 030 = debit)

  0125,315175016                      Retrieval Reference Number (may need to appear on receipt)

  0126,2                              Track Indicator (may need to appear on receipt)

  0129,0                              Fusebox -- Compliance Data

  0130,1.00                           Authorized Amount

  0140,USD                            Merchant Currency

  0201,0.00                           Tip Amount

  0651,00003@;010011759503151;\       Reversal data (for reversal, if needed)
  750160000047170500000000000;\       
  419039807417117595                  

  0738,106781MMCC539137 Y 0225        Recurring Compliance Data

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1002,CERTIFICATION-VISA/ELAVON      Cardholder Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,\*\*\*\*\*\*\*\*\*\*\*\*9999   Masked Account Number (for printing on receipt)

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

  5070,Merchant: Demo;Simplify:\      Simplify Information. See [Simplify-Controlled Field
  V-OG-2.02.02124;PARM: 2.21.1;\      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s01_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  TENDERDEF: 2.21.1;\                 
  EMVPARM: EMVPARM-E4-1               

  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s01_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5104,xxx...                         Tip Settings. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s01_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  7007,1118074642168320               Transaction Link Identifier (unique identifier to link transactions)

  8002,ONGUARD                        Location Name (provided by Elavon)

  8006,TSTLA3                         Chain Code (provided by Elavon)
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Auth Only Message (Tran Type 01) {#auth-only-message-tran-type-01 .h1}
================================

Simplify supports an Auth Only message from the POS process.

### Request {#request .h3}

The following table shows an example of an Auth Only Request message
from the POS to Simplify.

\

  API Field \#, Value   Description
  --------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,01               Transaction Type
  0002,1.00             Transaction Amount
  0007,57               Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s06_auth_only_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519           Transaction Date (current date)-- MMDDYY
  0014,105120           Transaction Time (current time) -- HHMMSS
  0109,TERM02           Terminal ID (provided by Elavon)
  0110,205              Cashier ID
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s06_auth_only_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s06_auth_only_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,ONGUARD          Location Name (provided by Elavon)
  8006,TSTLA3           Chain Code (provided by Elavon)

\
\

Prior Auth Sale Message (Tran Type 07) {#prior-auth-sale-message-tran-type-07 .h2}
--------------------------------------

Simplify supports a Prior-Auth Sale (Completion) message from the POS
process.

The Prior-Auth Sale transaction type is designed to record a previously
authorized transaction for funding. It is also called a "post-authorized
sale" or a "completion" transaction, and works in conjunction with an
Auth Only transaction.

\

API Field \#

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

User Data. See [Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

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
[Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

5104,xxx...

Tip Settings. See [Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

8002,RETL01

Location Name (provided by Elavon)

8006,TSTLAR

Chain Code (provided by Elavon)

\
\

### Response {#response-1 .h3}

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,07                             Transaction Type

  0002,8.00                           Transaction Amount

  0003,ID:1111748353147271            Account Token (returned by Fusebox)

  0004,1208                           Expiration Date -- MMYY

  0006,CVI014                         Authorization Code (returned by Fusebox)

  0007,1025                           Transaction ID / Reference Number

  0009,0025                           Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                         Transaction Date (current date) -- MMDDYY

  0014,115745                         Transaction Time (current time) -- HHMMSS

  0030,1                              Online Indicator

  0033,115754                         Fusebox -- Authorization Transaction Time

  0035,0DF9                           Validation Code

  0036,111175957465103                Host Transaction Identifier

  0037,0                              Authorizer

  0043,223946                         System Trace Audit Number

  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator (0 = contact; 2 = contactless; 5 = swiped)

  0054,01                             POS Entry Mode

  0109,TERM1                          Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,189                            Processor ID

  0115,010                            Transaction Qualifier (010 = credit; 030 = debit)

  0125,0624155745                     Retrieval Reference Number (may need to appear on receipt)

  0126,2                              Track Indicator (may need to appear on receipt)

  0128,6.00                           Original Authorization Amount

  0129,1                              Compliance Data

  0130,8.00                           Total Authorized Amount

  0131,00                             CPS Total Incremental Auths sent

  0132,0                              Authorization Reversal Sent

  0140,USD                            Merchant Currency

  0651,00003@;\                       Reversal data (for reversal, if needed)
  175016000004717050000000\           
  0000419039807417117595              

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1003,0000                           Gateway Response Code

  1004,ACKNOWLEDGED                   Host Response Message

  1008,466206\*\*\*\*\*\*0005         Masked Account Number (for printing on receipt)

  1010,COMPLETE                       Gateway Response Message

  1012,1832                           Gateway Batch Number

  1200,0000AA                         Issuer Network Information

  1359,4                              EMV CVM Indicator

  5002,80378002                       Device Serial Number

  5004,OG                             Encryption Provider ID

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5104,xxx...                         Tip Settings. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  7007,1111175588200494               Transaction Link Identifier (unique identifier to link transactions)

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Incremental Authorization Message (Tran Type 75) {#incremental-authorization-message-tran-type-75 .h2}
------------------------------------------------

Simplify supports an Incremental Authorization message from the POS
process if tokenization is implemented.

The following table shows a sample of fields in the Incremental
Authorization message that may need to match fields in the original
transaction. See the [Fusebox Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s12_incremental_authorization_message/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}
and the [Lodging Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s12_incremental_authorization_message/@@fusebox/documents/?fusebox-lodging-integration-guide/book/introduction/intro.html){.highlight}
for more information on this Transaction Type.

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
  -------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,07                    Transaction Type.
  0002,8.00                  Transaction Amount. Should be the final amount to be processed
  0003,ID:1111748353147271   Account Data. Must match Auth Only response.
  0004,1208                  Expiration Date -- MMYY. Must match Auth Only response (if present).
  0006,CVI014                Authorization Code. Must match Auth Only response.
  0007,1025                  Transaction ID / Reference Number. Must match Auth Only response
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143005                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID (provided by Elavon)
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit)
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5104,xxx...                Tip Settings. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s09_prior_auth_sale_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,RETL01                Location Name (provided by Elavon)
  8006,TSTLAR                Chain Code (provided by Elavon)

Full Authorization Reversal Message (Tran Type 61) {#full-authorization-reversal-message-tran-type-61 .h2}
--------------------------------------------------

Simplify supports a Full Authorization Reversal message from the POS if
tokenization is implemented.

The following table shows a sample of fields in the Full Authorization
Reversal message that may need to match fields in the original
transaction. See the [Fusebox Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s13_full_authorization_reversal_message/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}
for more information on this transaction type.

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
  -------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,61                    Transaction Type
  0002,1.00                  Transaction Amount
  0003,ID:1111748353147271   Account Data. Must match Auth Only response.
  0004,1208                  Expiration Date -- MMYY. Must match Auth Only response (if present).
  0006,106845                Authorization Code. Must match Auth Only response.
  0007,140                   Transaction ID / Reference Number. Must match Auth Only response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s13_full_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143005                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID (provided by Elavon)
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit)
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s13_full_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,RETL01                Location Name (provided by Elavon)
  8006,TSTLAR                Chain Code (provided by Elavon)

### Response {#response-2 .h3}

An example of a Full Authorization Reversal Response message (from
Simplify to the POS) is:

\

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,61                             Transaction Type

  0002,1.00                           Transaction Amount

  0003,ID:1120106195107475            Account Token (returned by Fusebox)

  0004,1215                           Expiration Date -- MMYY

  0006,CVI790                         Authorization Code (returned by Fusebox)

  0007,140                            Transaction ID / Reference Number

  0009,0104                           Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s13_full_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                         Transaction Date (current date) -- MMDDYY

  0014,143005                         Transaction Time (current time) -- HHMMSS

  0030,1                              Online Indicator

  0032,022519                         Authorization Transaction Date

  0033,161934                         Authorization Transaction Time

  0035,E2F9                           Validation Code

  0036,112010967961779                Host Transaction Identifier

  0037,0                              Authorizer

  0043,118410                         System Trace Audit Number

  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator (0 = contact; 2 = contactless , 5 = swiped)

  0054,01                             POS Entry Mode

  0109,TERM1                          Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,189                            Processor ID

  0115,010                            Transaction Qualifier(010 = credit; 030 = debit)

  0125,0110224915                     Retrieval Reference Number (may need to appear on receipt)

  0126,0                              Track Indicator (may need to appear on receipt)

  0128,16.00                          Original Authorization Amount

  0129,0                              Compliance Data

  0130,32.00                          Total Authorized Amount

  0131,01                             CPS Total Incremental Auths sent

  0132,0                              Authorization Reversal Sent

  0140,USD                            Merchant Currency

  0651,00003@;0100117595031\          Reversal data (for reversal, if needed)
  5175016000004717050000000\          
  0000419039807417117595              

  0738,106781MMCC539137 Y 0225        Recurring Compliance Data

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,400555\*\*\*\*\*\*4460         Masked Account Number (for printing on receipt)

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

  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s13_full_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s13_full_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  7007,1112010821551364               Transaction Link Identifier. A unique identifier to link transactions

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Partial Authorization Reversal Message (Tran Type 76) {#partial-authorization-reversal-message-tran-type-76 .h2}
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
  -------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,76                    Transaction Type.
  0002,1.00                  Transaction Amount
  0003,ID:1120106195107475   Account Data. Must match Auth Only response.
  0004,1215                  Expiration Date -- MMYY. Must match Auth Only response (if present).
  0006,106844                Authorization Code. Must match Auth Only response.
  0007,140                   Transaction ID / Reference Number. Must match Auth Only response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s15_partial_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143008                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID (provided by Elavon)
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit)
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s15_partial_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,RETL01                Location Name (provided by Elavon)
  8006,TSTLAR                Chain Code (provided by Elavon)

### Response {#response-3 .h3}

An example of a Partial Authorization Reversal Response message (from
Simplify to the POS) is:

\

  API Field \#, Value                Description
  ---------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,76                            Transaction Type
  0002,1.00                          Transaction Amount
  0003,ID:1120106195107475           Account Token (returned by Fusebox)
  0004,1215                          Expiration Date -- MMYY
  0006,CVI790                        Authorization Code (returned by Fusebox)
  0007,140                           Transaction ID / Reference Number
  0009,0104                          Host Batch number
  0011,xxx..                         User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s15_partial_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
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
  5070,xxx...                        Simplify Information. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s15_partial_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5071,xxx...                        Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s15_partial_authorization_reversal_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  7007,1112010821551364              Transaction Link Identifier (unique identifier to link transactions)
  8002,RETL01                        Location Name (provided by Elavon)
  8006,TSTLAR                        Chain Code (provided by Elavon)

\

Return Message (Tran Type 09) {#return-message-tran-type-09 .h2}
-----------------------------

Simplify supports a Return message from the POS.

### Request {#request-4 .h3}

An example of a Return Request message (from the POS to Simplify) is:

\

  API Field \#, Value   Description
  --------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,09               Transaction Type.
  0002,125.98           Transaction Amount
  0007,1025             Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s07_return_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,143005           Transaction Time (current time) -- HHMMSS
  0109,TERM1            Terminal ID (provided by Elavon)
  0110,205              Cashier ID
  0115,010              Transaction Qualifier (010 = credit; 030 = debit)
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s07_return_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,RETL01           Location Name (provided by Elavon)
  8006,TSTLAR           Chain Code (provided by Elavon)

### Response {#response-4 .h3}

An example of an Incremental Authorization Response message (from
Simplify to the POS) is:

\

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,01                             Tran Type. Note that the Tran Type in the response is a 01 (Auth Only response) -- not a 75.

  0002,19.00                          Transaction Amount

  0003,ID:1120064425266606            Account Token (returned by Fusebox)

  0004,1208                           Expiration Date -- MMYY

  0006,CVI130                         Authorization Code (returned by Fusebox)

  0007,1123                           Transaction ID / Reference Number

  0009,0102                           Host Batch Number

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s12_incremental_authorization_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                         Transaction Date (current date) -- MMDDYY

  0014,143005                         Transaction Time (current time) -- HHMMSS

  0030,1                              Online Indicator

  0032,022519                         Authorization Transaction Date

  0033,161934                         Authorization Transaction Time

  0035,BF66                           Validation Code

  0036,112006976774166                Host Transaction Identifier

  0037,0                              Authorizer

  0043,211605                         System Trace Audit Number

  0047,2;1;0;1;0;0;6;5;4;1;2;4;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator (0 = contact; 2 = contactless , 5 = swiped)

  0054,01                             POS Entry Mode

  0109,TERM1                          Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0112,189                            Processor ID

  0115,010                            Transaction Qualifier (010 = credit; 030 = debit)

  0125,0106211934                     Retrieval Reference Number (may need to appear on receipt)

  0126,2                              Track Indicator (may need to appear on receipt)

  0128,1.00                           Original Authorization Amount

  0129,1                              Compliance Data

  0130,19.00                          Total Authorized Amount

  0131,00                             CPS Total Incremental Auths sent

  0140,A                              Merchant Currency

  0651,00003@;\                       Reversal data (for reversal, if needed)
  01001175950315\                     
  17501600000471705000000000\         
  00419039807417117595                

  0738,106781MMCC539137 Y 0225        Recurring Compliance Data

  1000,VI                             Card Type

  1001,VISA                           Card Name

  1003,0000                           Gateway Response Code

  1004,APPROVAL                       Host Response Message

  1005,0010600008014593613999         Merchant Number

  1008,400555\*\*\*\*\*\*4460         Masked Account Number (for printing on receipt)

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

  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s12_incremental_authorization_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s12_incremental_authorization_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5104,xxx...                         Tip Settings. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s12_incremental_authorization_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  7007,1112006767740668               Transaction Link Identifier (unique identifier to link transactions)

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Void Return Message (Tran Type 17) {#void-return-message-tran-type-17 .h2}
----------------------------------

Simplify supports a Void Return message from the POS process if
tokenization is implemented. Customers might want to void a return
transaction after it has been completed. The POS does this by sending a
Void Return message to Simplify.

The following table shows a sample of fields in the Void Return message
that may need to match fields in the original transaction. See the
[Fusebox Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s14_void_return_message/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}
for more information on this Transaction Type.

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
  -------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,17                    Transaction Type.
  0002,125.98                Transaction Amount. Must match Return response.
  0003,ID:1120106195107475   Account Data. Must match Return response.
  0004,1208                  Expiration Date -- MMYY. Must match Return response (if present).
  0007,1025                  Transaction ID / Reference Number. Must match Return response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s14_void_return_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143515                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID. Must match Return response.
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit). Must match Return response.
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s14_void_return_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,RETL01                Location Name. Must match Return response.
  8006,TSTLAR                Chain Code. Must match Return response.

\

### Response {#response-5 .h3}

An example of a Void Return Request message (from the POS to Simplify)
is:

  API Field \#, Value        Description
  -------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,17                    Transaction Type.
  0002,125.98                Transaction Amount. Must match Return response.
  0003,ID:1120106195107475   Account Data. Must match Return response.
  0004,1208                  Expiration Date -- MMYY. Must match Return response (if present).
  0007,1025                  Transaction ID / Reference Number. Must match Return response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s14_void_return_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519                Transaction Date (current date) -- MMDDYY
  0014,143515                Transaction Time (current time) -- HHMMSS
  0109,TERM1                 Terminal ID. Must match Return response.
  0110,205                   Cashier ID
  0115,010                   Transaction Qualifier (010 = credit; 030 = debit). Must match Return response.
  5071,xxx...                Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s14_void_return_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
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

### Request {#request-6 .h3}

An example of a Void Request message (from the POS to Simplify) is:

  API Field \#, Value        Description
  -------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,11                    Transaction Type.
  0002,125.98                Transaction Amount. Must match Sale response.
  0003,ID:1102571965098318   Account Data. Must match Sale response.
  0004,1215                  Expiration Date -- MMYY. Must match Sale response (if present).
  0007,1025                  Transaction ID / Reference Number. Must match Sale response.
  0011,xxx..                 User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s03_void_transaction_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
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
  ----------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,11                             Transaction Type.
  0002,125.98                         Transaction Amount
  0003,ID:1102571965098318            Account Token (returned by Fusebox)
  0006,CMC663                         Authorization Code (returned by Fusebox)
  0007,1025                           Transaction ID / Reference Number
  0009,0020                           Fusebox -- Host Batch number
  0011,xxx..                          User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s03_void_transaction_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
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
  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s03_void_transaction_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s03_void_transaction_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  7007,1114281539351186               Transaction Link Identifier (unique identifier to link transactions)
  8002,RETL01                         Location Name. Must match Sale response.
  8006,TSTLAR                         Chain Code. Must match Sale response.

\

Gift Card Messages (Tran Types 01, 02, 07, 09, 11, 17, 24) {#gift-card-messages-tran-types-01-02-07-09-11-17-24 .h2}
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
the [Gift and Stored Value Card Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s08/@@fusebox/documents/?fusebox-gift-integration-guide/book/introduction/intro.html){.highlight}
for more information on this Transaction Type.

### Request {#request-7 .h3}

An example of a **Card Issuance Request** message (from the POS to
Simplify) is:

\

  API Field \#, Value   Description
  --------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,09               Transaction Type of 9, in combination with Field 115 of 050 and Field 117 of 2, indicates a Gift Card Issuance
  0002,50.00            Dollar amount to be authorized
  0007,1025             Transaction ID / Reference Number
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s08/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,131535           Transaction Time (current time) -- HHMMSS
  0109,RETAIL           Terminal ID (provided by Elavon)
  0110,00000301         Cashier ID
  0115,050              Transaction Qualifier (050 = Gift / Stored Value)
  0117,2                Stored Value Function. A Value of 2 indicates a Card Issuance
  1008,ID:              Set to 'ID:' to request that an account Token be returned by Fusebox
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s08/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,PLSNTN           Location Name (provided by Elavon)
  8006,TSTLAR           Chain Code (provided by Elavon)

\

### Response {#response-7 .h3}

An example of a **Card Issuance Response** message (from Simplify to the
POS) is:

\

  API Field \#, Value                 Description
  ----------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,09                             Transaction Type
  0002,000050.00                      Transaction Amount
  0003,ID:1120106195107475            Account Token (returned by Fusebox)
  0004,1218                           Expiration Date -- MMYY
  0006,001000                         Authorization Code (returned by Fusebox)
  0007,1025                           Transaction ID/Reference Number
  0011,xxx..                          User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s08/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
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
  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s08/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s08/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  7007,1111293621357294               Transaction Link Identifier. A unique identifier to link transactions
  8002,PLSNTN                         Location Name (provided by Elavon)
  8006,TEST                           Chain Code (provided by Elavon)

\

Inquiry Message (Tran Type 22) {#inquiry-message-tran-type-22 .h2}
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
        policy. E.g. a **Void Request** can be sent for the transaction.

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
[Fusebox Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s02_inquiry_message/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}
under "Transaction Types" \> "Transaction Inquiry (22)" for more
information on this Transaction Type.

\

  API Field \#   Description
  -------------- -----------------------------------
  0002           Transaction Amount
  0007           Transaction ID / Reference Number
  0109           Terminal ID
  8002           Location Name
  8006           Chain Code

\

### Request {#request-8 .h3}

An example of an **Inquiry Request** message (from the POS to Simplify)
is as follows:

  API Field \#, Value   Description
  --------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,22               Tran Type.
  0002,5.00             Transaction Amount. Must match the financial request.
  0007,1025             Transaction ID / Reference Number. Must match the financial request.
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s02_inquiry_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
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

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,02                             Original Transaction Type (entire response = original host response)

  0002,5.00                           Transaction Amount

  0003,ID:4546705467010002            Account Token (returned by Fusebox)

  0004,1221                           Expiration Date - MMYY

  0006,CVI758                         Authorization Code (returned by Fusebox)

  0007,1025                           Transaction ID / Reference Number

  0009,001                            Fusebox -- Host Batch number

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s02_inquiry_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                         Transaction Date (current date) -- MMDDYY

  0014,151729                         Transaction Time (current time) -- HHMMSS

  0017,0.00                           Cash Back Amount

  0030,1                              Fusebox -- Online Indicator

  0032,022519                         Fusebox -- Authorization Transaction Date

  0033,181733                         Fusebox -- Authorization Transaction Time

  0035,D07D                           Validation Code

  0036,114120980253909                Host Transaction Identifier

  0037,2                              Fusebox -- Authorizer

  0043,214872                         System Trace Audit Number

  0047,M;1;1;1;0;1;2;5;4;1;3;C;0;4    POS Data Code

  0052,5                              Transponder / Proximity Indicator (0 = contact; 2 = contactless; 5 = swiped)

  0054,90                             POS Entry Mode

  0062,110                            Service Code

  0109,TERM1                          Terminal ID

  0110,205                            Cashier ID

  0112,400                            Fusebox -- Processor ID

  0115,010                            Transaction Qualifier (010 = Credit; 030 = debit)

  0125,430181733                      Retrieval Reference Number (may need to appear on receipt)

  0126,2                              Track Indicator (may need to appear on receipt

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

  1008,\*\*\*\*\*\*\*\*\*\*\*\*0002   Masked Account Number (may need to appear on receipt)

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

  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s02_inquiry_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  7007,1114281539351186               Transaction Link Identifier (unique identifier to link transactions)

  8002,RETL01                         Location Name (provided by Elavon)

  8006,TSTLAR                         Chain Code (provided by Elavon)
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

DCC Inquiry Message (Tran Type 46) {#dcc-inquiry-message-tran-type-46 .h2}
----------------------------------

The DCC Inquiry Message is a non-financial message used to support DCC
processing. If Simplify receives a DCC Inquiry Request from the POS, it
will pass through the message to Fusebox. For more information on DCC,
see [Dynamic Currency Conversion
(DCC)](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s18_dcc_inquiry_message/../../../book/c07/c07_dynamic_currency_conversion_dcc.html){.highlight}.

\

Token Request Message (Tran Type 37) {#token-request-message-tran-type-37 .h2}
------------------------------------

Simplify supports a **Token Request** message from the POS process.

The **Token Request** message is a non-financial message, used to obtain
the Fusebox-assigned token for an account number.

### Request {#request-9 .h3}

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

Cancel Message (Tran Type 80) {#cancel-message-tran-type-80 .h2}
-----------------------------

Simplify supports a **Cancel** message from the POS process. When
Simplify receives a **Cancel Request**, it will attempt to cancel the
transaction (return to the Closed state) and send a **Cancel Response**
to the POS.

The **Cancel** message is available to allow the POS process to clear
the PIN Pad. This message should be used if the POS process and the PIN
Pad are out of sync.

### Request {#request-10 .h3}

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

User Data. See [Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s05_cancel_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}
for the use of this field

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

User Data. See [Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s05_cancel_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}
for the use of this field

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

Batch Close Message (Tran Type 13) {#batch-close-message-tran-type-13 .h2}
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

For more details on this tran type, see the [Fusebox Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s16_batch_close_message/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}.

### Request {#request-11 .h3}

An example of a **Batch Close Request** message (from the POS process to
the Simplify application) is:

\

  API Field \#, Value   Description
  --------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,13               Transaction Type
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s16_batch_close_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0109,RETERM1          Terminal ID (provided by Elavon)

\

### Response {#response-11 .h3}

An example of a **Batch Close Response** message (from the Simplify
application to the POS process) is:

\

  API Field \#, Value     Description
  ----------------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,13                 Transaction Type
  0011,xxx..              User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s16_batch_close_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
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

Batch Inquiry Message (Tran Type 14) {#batch-inquiry-message-tran-type-14 .h2}
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

For more details on this tran type, see the [Fusebox Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s17_batch_inquiry_message/@@fusebox/documents/?fusebox-integration-guide/book/intro.html){.highlight}.

### Request {#request-12 .h3}

An example of a **Batch Inquiry Request** message (from the POS to the
Simplify application) is:

\

  API Field \#, Value   Description
  --------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,14               Transaction Type
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s17_batch_inquiry_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,SIMTESTVOLT      Location Name (provided by Elavon)

\

### Response {#response-12 .h3}

An example of a **Batch Inquiry Response** message (from the Simplify
application to the POS) is:

\

  API Field \#, Value     Description
  ----------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,14                 Transaction Type
  0011,xxx..              User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s17_batch_inquiry_message/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0140,USD                Merchant Currency Trigraph
  1003,0022               Gateway Response Code
  1004,EMPTY BATCH        Host Response Message
  1010,EMPTY BATCH        Gateway Response Message
  1012,0248               Gateway Batch Number
  7007,1115126747595135   Transaction Link Identifier. A unique identifier to link transactions
  8002,SIMTESTVOLT        Location Name (provided by Elavon)

\

Non-Financial Messages (Tran Type 36) {#non-financial-messages-tran-type-36 .h2}
-------------------------------------

Transaction Type 36 is used for non-financial purposes. The specific
purpose of a Tran Type 36 message is indicated by the value in the first
two bytes of Field 11, which define the Message Type. Field 5001 may be
used to further define the request and/or return data in the response.

Transaction Type 36 is used for non-financial purposes. The specific
purpose of a Tran Type 36 message is indicated by the value in the first
two bytes of Field 11, which define the Message Type. Field 5001 may be
used to further define the request and/or return data in the response.

### Non-Financial Message Format []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c02/s11/c02_s11_non-financial_messages.html#non-financial-message-format"} {#non-financial-message-format .h3}

\

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36                             Transaction Type 36. Non-Financial message

  0011,xxx..                          User Data.\
                                      The first two bytes of Field 11 define the **Message Type** , as described below.\
                                      Usage of other bytes varies based on Message Type; see [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5001,xxx..                          Non-Financial Data.\
                                      The format of this field depends on the value of message type.\
                                      See the sections on specific messages for details.
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

### **Message Types** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c02/s11/c02_s11_non-financial_messages.html#message-types"} {#message-types .h3}

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

Signature Message (Tran Types 36-01, 36-02) {#signature-message-tran-types-36-01-36-02 .h2}
-------------------------------------------

Simplify supports a signature process on touchscreen PIN Pads. When this
process is triggered, Simplify will prompt for a signature and send the
signature data (or customer Cancel) to the POS in a **Signature
Response** (36-02) message. There are two ways to trigger signature
processing:

-   Request message -- The POS can send Simplify a **Signature Request**
    (36-01) message.

-   Auto signature -- For approved **Sale**, **Auth Only** and
    **Return** transactions, signature process can occur automatically
    (no **Signature Request** required). For details, see [Auto
    Signature](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p01_signature_message/../../../../book/c09/c09_auto_signature.html){.highlight}.

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

### **Field 5001 Format** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c02/s11/p01_signature_message/c02_s11_p01.html#field-5001-format"} {#field-5001-format .h3}

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
|                                   | Definitions](https://developer.el |
|                                   | avon.com/#/api/861b65f6-c5a9-4c28 |
|                                   | -a4e8-5ad37253a475.rcosoomi/versi |
|                                   | ons/0da6edd4-8b7e-4669-b286-26992 |
|                                   | 6a2397b.rcosoomi/documents?simpli |
|                                   | fy-developer-guide/book/c02/s11/p |
|                                   | 01_signature_message/../../../../ |
|                                   | book/c12/s06/c10_s06_appendix_f_t |
|                                   | ran_type_and_message_type.html){. |
|                                   | highlight}.                       |
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
|                                   | Definitions](https://developer.el |
|                                   | avon.com/#/api/861b65f6-c5a9-4c28 |
|                                   | -a4e8-5ad37253a475.rcosoomi/versi |
|                                   | ons/0da6edd4-8b7e-4669-b286-26992 |
|                                   | 6a2397b.rcosoomi/documents?simpli |
|                                   | fy-developer-guide/book/c02/s11/p |
|                                   | 01_signature_message/../../../../ |
|                                   | book/c12/s06/c10_s06_appendix_f_t |
|                                   | ran_type_and_message_type.html){. |
|                                   | highlight}.                       |
+-----------------------------------+-----------------------------------+
| 5001,00109220FS50FS5FS\           | See format described above.\      |
| Message 1; Message 2; Message 3;  |                                   |
| Message 4; Message 5; Message 6   |                                   |
+-----------------------------------+-----------------------------------+

### Response {#response-13 .h3}

An example of a **Signature Response** message (from the Simplify
application to the POS process) is:

  API Field \#, Value                      Description
  ---------------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36                                  Transaction Type. A value of 36 indicates a Non- Financial transaction
  0011,xxx..                               User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p01_signature_message/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0052,5                                   Transponder / Proximity Indicator (0 = contact; 2 = contactless, 5 = swiped)
  5000,xxxxxxxxxxxxxxxxxxxxxxxx.......xx   Signature data

Version Number Inquiry Message (Tran Type 36-06) {#version-number-inquiry-message-tran-type-36-06 .h2}
------------------------------------------------

Simplify supports a **Version Number Inquiry** message from the POS
process.

The POS can send this message to Simplify when it wants to check the
Simplify application (program) version number, parameter version number,
and/or build number.

The **Version Number Inquiry Request** does not contain field 5001. The
only fields are field 1 (Tran Type = 36) and field 11.

### Field 5001 Format {#field-5001-format .h3}

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

### **Sample Response Message** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c02/s11/p02_versionnumberinquirymessage/c02_s11_p02.html#sample-response-message"} {#sample-response-message .h3}

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
|                                   | Definitions](https://developer.el |
|                                   | avon.com/#/api/861b65f6-c5a9-4c28 |
|                                   | -a4e8-5ad37253a475.rcosoomi/versi |
|                                   | ons/0da6edd4-8b7e-4669-b286-26992 |
|                                   | 6a2397b.rcosoomi/documents?simpli |
|                                   | fy-developer-guide/book/c02/s11/p |
|                                   | 02_versionnumberinquirymessage/.. |
|                                   | /../../../book/c12/s06/c10_s06_ap |
|                                   | pendix_f_tran_type_and_message_ty |
|                                   | pe.html){.highlight}.             |
+-----------------------------------+-----------------------------------+
| 5001,006040 Ver: 2.23 - 2.23.1    | Version number data               |
| Build: 52302                      |                                   |
+-----------------------------------+-----------------------------------+
| 5002,80378002                     | PIN Pad serial number             |
+-----------------------------------+-----------------------------------+

\

Initiate IngEstate Message (Tran Type 36-07) {#initiate-ingestate-message-tran-type-36-07 .h2}
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

### **Field 5001 Format** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c02/s11/p03_initiate_ingestate_message/c02_s11_p03.html#field-5001-format"} {#field-5001-format .h3}

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

### Request {#request-13 .h3}

An example of a possible **Initiate IngEstate Request** message (from
the POS process to Simplify) is:

\

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36                             Transaction Type. A value of 36 indicates a Non-Financial transaction

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p03_initiate_ingestate_message/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5001,88100899990000                 881=Tag for TMSID\
                                      008=Length of Data\
                                      99990000=new TMSID
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

### Response {#response-14 .h3}

An example of a possible **Initiate IngEstate Response** message (from
Simplify to the POS process) is:

\

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36                             Transaction Type. A value of 36 indicates a Non-Financial transaction

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p03_initiate_ingestate_message/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5001,0070528007044000               007 = Tag for File download information\
                                      052 = Length of data (must be 52)\
                                      80070440 (plus blanks) = padded PIN Pad Serial \# (must be exactly 50 bytes)\
                                      00 = Status Flag (00 = Simplify successfully communicated with IngEstate)
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

### IngEstate Update Flow {#ingestate-update-flow .h3}

![IngEstate Update flow
Chart.png](IngEstate%20Update%20Flow%20Chart.png)\

Scrolling Receipt Request Message (Tran Type 36-10) {#scrolling-receipt-request-message-tran-type-36-10 .h2}
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

### Field 5001 Format {#field-5001-format .h3}

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

### Request {#request-14 .h3}

An example of a possible **Scrolling Receipt Request** message (from the
POS process to Simplify) is:

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36                             Transaction Type. A value of 36 indicates a Non-Financial transaction

  0011,xxx..                          User Data See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p04_scrolling_receipt_request_message/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5001,001025\                        001 = Tag for Item Data\
  2LB PKG STRAWBERRIES\               025 = Length of Item Data\
  2.98002013\                         2LB PKG STRAWBERRIES 2.98 = Item Data\
  SubTotal 2.98                       002 = Tag for Running Total Data\
                                      013 = Length of Running Total Data\
                                      SubTotal 2.98 = Running Total Data
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Scrolling Receipt Stop Message (Tran Type 36-11) {#scrolling-receipt-stop-message-tran-type-36-11 .h2}
------------------------------------------------

Simplify supports a **Scrolling Receipt Stop** message from the POS
process.

When Simplify receives a **Scrolling** **Receipt** **Stop** message, it
responds by stopping the display of Scrolling Receipt data and
displaying the Idle screen. The PIN Pad will then be available to
process messages as usual. There is no response message to the POS.

This message does not contain field 5001. The only fields are field 1
(Tran Type = 36) and field 11. See [Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p05_scrollingreceiptstopmessage/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}
for the use of field 11.

\

Exit Reversal Mode Message (Tran Type 36-12) {#exit-reversal-mode-message-tran-type-36-12 .h2}
--------------------------------------------

Reversal mode is used to force a host reversal if this is required
during EMV processing. In this processing mode, Simplify resends the
request until a host response is received, while all new transactions on
the PIN Pad are processed offline.

Simplify supports an **Exit Reversal Mode** **Message**. When Simplify
receives this message, it will send a **Void** **Transaction**
**Response** (11) message to the POS, including the data required to
request the reversal, and return to normal processing mode. For more
information, see [Chip Declines and Simplify Reversal
Mode](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p06_exit_reversal_mode_message/../../../../book/c04/s05_icc_declines_and_simplify_reversal_mode/c04_s06.html){.highlight}.

**Important**: Forcing Simplify to exit reversal mode is an exception
procedure that should only be used when necessary. If Simplify is forced
out of reversal mode, the merchant will be responsible for ensuring that
the transaction is reversed by the host, using the data in the **Void**
**Transaction** **Response**. Elavon strongly recommends allowing
Simplify to reverse all host-approved transactions that are declined by
the chip.

Informational Prompting Message (Tran Type 36-14) {#informational-prompting-message-tran-type-36-14 .h2}
-------------------------------------------------

Simplify supports "Informational Prompts", which allow the merchant to
display screens and receive customer feedback in the response. See
[Informational
Prompting](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/c2s11p8/../../../../book/c06/c06_informational_prompting.html){.highlight}.

Quick Chip Message (Tran Type 36-40) {#quick-chip-message-tran-type-36-40 .h2}
------------------------------------

A Quick Chip message can be sent from the POS to Simplify to allow the
customer to insert, swipe or tap a card during item entry. This allows
the customer to complete all payment steps before the total is known.
See [Quick Chip
Tendering](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/c2s11p9/../../../../book/c10/c10_quick_chip_tendering.html){.highlight}
for more information.

Normal tendering steps must follow the Quick Chip process.

Print Message Request (Tran Type 36-45) {#print-message-request-tran-type-36-45 .h2}
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

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36                             Transaction Type. A value of 36 indicates a Non-Financial transaction

  0011,xxx..                          User Data See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/c2s11p10_print_request_message/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5108,\[see value below\]            Customer receipt print data and commands\
                                      (see format table above)

  5111, Printing Receipt              Message displayed on PIN Pad during printing.
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Status Message (Tran Type 36-51) {#status-message-tran-type-36-51 .h2}
--------------------------------

Simplify supports a **Status** **Message** to the POS. This message is
sent to the POS to provide it with status information on the current
transaction.

The **Status** message is informational only and does not follow the
general rules for recovery after a timeout. See [Appendix D: Recovery
after Timeout
Flow](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p07_status_message/../../../../book/c12/s04_appendix_d_recovery/c10_s04.html){.highlight}
for details.

This message does not contain field 5001. The only fields are field 1
(Tran Type = 36) and field 11. See [Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c02/s11/p07_status_message/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}
for the use of field 11.

\

Stand-In Processing {#stand-in-processing .h1}
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

**Important:** Note for purposes of PCI DSS compliance that a contains
encrypted customer data. The merchant is responsible for making this
data unrecoverable after completion of the authorization process (*PCI
DSS 3.0 Requirement 3.2*).

For EMV transactions, Simplify can be configured to return EMV tags in
the Stand-In Response. The POS can include these tags in the resubmitted
transaction. Submitting EMV Stand-In transactions without EMV tags can
cause declines from some issuers. See [Fusebox EMV Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c03/@@fusebox/documents/?fusebox-emv-integration-guide/book/introduction/intro.html){.highlight}
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
[Inquiry
Message](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c03/../../book/c02/s02_inquiry_message/c02_s02.html){.highlight}.

Note: Inquiry processing is not affected by whether or not Stand-in is
enabled.

\

Stand-In and Online Response Differences {#stand-in-and-online-response-differences .h2}
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

Sample Stand-In Response {#sample-stand-in-response .h2}
------------------------

A sample of the **Stand-In Response** for an offline transaction is as
follows:

(Stand-in enabled; EMV enabled but configured not to return EMV tags on
Stand-In)

\

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,02                             Transaction Type

  0002,1.00                           Transaction Amount

  0003,;&&&&&&&&&&&&&&&&\             Encrypted Track Data\
  = &&&&&&&&&&&&&&&&&&&&?             (See under [Usage](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c03/s06_sample_stand_in_response/../../../book/c12/s08/c12s8.html){.highlight} for details.)

  0006,SN:80649419                    Serial Number (needed to Decrypt)

  0007,53                             Reference Number

  0011,xxx...                         User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c03/s06_sample_stand_in_response/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                         Transaction Date

  0014,104720                         Transaction Time

  0017,0.00                           Cash Back Amount

  0047,C;1;1;1;0;1;5;5;4;3;3;C;0;4    POS Data Code

  0052,0                              Transponder / Proximity Indicator (0 = contact; 2 = contactless , 5 = swiped)

  0054,05                             POS Entry Mode

  0109,TERM02                         Terminal ID (provided by Elavon)

  0110,205                            Cashier ID

  0115,010                            Transaction Qualifier (010 = credit; 030 = debit)

  0126,2                              Track Indicator (may need to appear on receipt)

  0201,0.00                           Tip Amount

  1000,VI                             Card Type

  1002,UAT USA/Test Card 03           Cardholder Name

  1003,0000                           Response Code

  1008,476173\*\*\*\*\*\*0119         Masked Account Number

  1010,\*SLR STAND-IN.                Response Message.

  1314,A0000000031010                 Dedicated File Name

  1315,0096                           ICC Application Version Number

  1379,1326\|Application Label:       Offline EMV Receipt Field List
  ;1300\|AAC:\                        
  ;1307\|TVR: ;1325\|AID: ;           

  1382,F000F0A001                     Additional Terminal Capabilities

  5002,80649419                       Serial Number needed to Decrypt

  5004,OG                             Encryption Provider ID

  5006,FFFF4D4D4D0000C0046C050006     Encryption Transmission Block

  5010,EMVDC0838                      EMV kernel version

  5070,xxx...                         Simplify Information. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c03/s06_sample_stand_in_response/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  8002,ONGUARD                        Location Name (provided by Elavon)

  8006,TSTLA3                         Chain Code (provided by Elavon)
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Recommended Rules for Handling Stand-In Responses {#recommended-rules-for-handling-stand-in-responses .h2}
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

Store and Forward Transactions {#store-and-forward-transactions .h2}
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

EMV {#emv .h1}
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
requirements for EMV, refer to the [Fusebox EMV Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/@@fusebox/documents/?fusebox-emv-integration-guide/book/introduction/intro.html){.highlight}.

Simplify will attempt to process a transaction as EMV when the chip
reader successfully communicates with the chip to obtain card data, and
EMV processing is enabled for the card type and transaction type.

EMV processing is largely transparent to the POS, with the exception of
receipt printing. Additional **Status Message** codes are used for EMV
processing; see under [Simplify-Controlled Field
Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

Contactless EMV is supported using rules similar to those used for
contact EMV. Contactless EMV is enabled separately from contact; please
contact your Elavon representative if you would like to enable
contactless EMV. Simplify can also be configured to process contactless
transactions using MSD emulation.

EMV Receipt Printing {#emv-receipt-printing .h2}
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
the [Fusebox EMV Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s01_emv_receipt_printing/@@fusebox/documents/?fusebox-emv-integration-guide/book/introduction/intro.html){.highlight}
under "EMV Receipt Details".

EMV Tags {#emv-tags .h2}
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

Other EMV-Related Response Fields {#other-emv-related-response-fields .h2}
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
which a chip (ICC) is present. For more information, see the [Fusebox
EMV Integration
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s03_other_emv_response_fields/@@fusebox/documents/?fusebox-emv-integration-guide/book/introduction/intro.html){.highlight}
under "Host Request" \> "EMV Elavon Gateway API Request Changes".

\

Offline Situations {#offline-situations .h2}
------------------

Simplify supports Stand-In processing for offline situations based on
configured settings; see [Stand-in
Processing](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s04_offline_situations/../../../book/c03/c03_stand-in_processing.html){.highlight}
for more information. When a transaction is processed offline, a
Simplify-generated response message is returned to the POS in field 1010
of the Stand-In Response; see [Simplify-Generated
Messages](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s04_offline_situations/../../../book/c11/c09_simplify-generated_message_codes.html){.highlight}.

Traditionally EMV tags are not returned in a Stand-In response. Starting
with version 2.02.023, Simplify can be set to return EMV tags to the POS
in Stand-In. This allows the POS to process Store and Forward (deferred
authorization) transactions as EMV.

Other changes to offline processing for EMV: ( 1) If EMV print data is
returned on an offline response, the POS must print the data. (2)
Simplify does not validate the expiration date for offline EMV
transactions.

\

ICC Declines and Simplify Reversal Mode {#icc-declines-and-simplify-reversal-mode .h2}
---------------------------------------

If the ICC chip declines a host-approved transaction, or the customer
removes their card from the chip reader before a host-approved
transaction is completed, the host approval will need to be reversed.

If one of these scenarios occurs, the message in field 1010 will begin
with \*ICC (see [Simplify-Generated
Messages](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s05_icc_declines_and_simplify_reversal_mode/../../../book/c11/c09_simplify-generated_message_codes.html){.highlight})
and field 26 will specify the reason for the reversal. 2 = Chip
requested decline: 3 = Premature EMV card removal.

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
Elavon Main Menu on the PIN Pad; see the [Simplify
Configuration,Download and Troubleshooting
Guide](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s05_icc_declines_and_simplify_reversal_mode/@@simplify/documents/?simplify-config-guide/book/c1/c1.html){.highlight}
under "Exiting Reversal Mode" for details.)

\

**Important**:

\

The following tables provide:

-   A sample of an ICC Chip Decline response.

-   The format of the **Exit Reversal Mode** message.

-   A sample of the **Exit Reversal Mode** / **Void Transaction
    Response** message exchange.

### **Sample ICC Chip Decline Response** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c04/s05_icc_declines_and_simplify_reversal_mode/c04_s06.html#sample-icc-chip-decline-response"} {#sample-icc-chip-decline-response .h3}

Below is a sample response for a **Sale** transaction that was declined
by the ICC:

\

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,02                             

  0002,3.00                           

  0003,ID:5555396468550434            

  0004,1218                           

  0006,006276                         

  0007,221                            

  0009,001                            

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s05_icc_declines_and_simplify_reversal_mode/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                         

  0014,143339                         

  0017,0                              

  0026,2                              Reason for chip decline (2=Chip requested decline; 3=Premature EMV card removal)

  0030,1                              

  0032,022519                         

  0033,173346                         

  0034,M                              

  0035,0707                           

  0036,MCC0110ZU                      

  0037,0                              

  0043,015755                         

  0047,C;1;1;1;0;1;5;0;5;3;3;1;0;4    POS Data Code

  0052,0                              Transponder / Proximity Indicator (0 = contact; 2 = contactless; 5 = swiped)

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

  0163,en                             Cardholder Language Preference (EMV Tag 5F2D)

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

  1300,DF60405EFAA61BE6               Application Cryptogram (EMV Tag 9F26)

  1301,D9816C720D4ECD560012           Issuer Authentication Data (EMV Tag 91)

  1302,181231                         Application Expiration Date (EMV Tag 5F24)

  1303,1F0002                         Cardholder Verification Method (CVM) Results (EMV Tag 9F34)

  1305,021020100F220\                 Issuer Application Data (EMV Tag 9F10)
  4000000000\                         
  00000000000FF                       

  1306,E0F8C8                         Terminal Capabilities (EMV Tag 9F33)

  1307,4200008000                     Terminal Verification Result (TVR) (EMV Tag 95)

  1312,124                            Terminal Country Code (EMV Tag 9F1A)

  1313,00                             Application PAN Sequence Number (EMV Tag 5F34)

  1314,A0000000041010                 Dedicated File Name (EMV Tag 84)

  1317,0002                           Terminal Application Version Number (EMV Tag 9F09)

  1318,00000192                       Transaction Sequence Counter (EMV Tag 9F41)

  1319,5800                           Application Interchange Profile (EMV Tag 82)

  1320,0014                           Application Transaction Counter (ATC) (EMV Tag 9F36)

  1321,00                             Cryptogram Information Data (EMV Tag 9F27)

  1322,22                             Terminal Type (EMV Tag 9F35)

  1323,E66C0DB5                       Unpredictable Number (EMV Tag 9F37)

  1325,A0000000041010                 ICC Application Identifier (AID) (EMV Tag 4F)

  1326,MasterCard                     ICC Application Preferred Name (EMV Tag 9F12)

  1327,MasterCard                     Terminal Application Label (EMV Tag 50)

  1328,A0000000041010                 Terminal Application Identifier (AID) (EMV Tag 9F06)

  1332,FF00                           Application Usage Control (EMV Tag 9F07)

  1333,06152016                       Last Host EMV Key Download

  1334,E800                           Transaction Status Information (EMV Tag 9B)

  1339,00                             EMV Response Code (EMV Tag 8A)

  1350,F1                             CA Public Key Index (EMV Tag 8F)

  1357,124                            ICC Transaction Currency (EMV Tag 5F2A)

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
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

### **Sample Exit Reversal Mode Message Exchange** {#sample-exit-reversal-mode-message-exchange .h3}

The response to an Exit Reversal Mode (36-12) Request is a Void
Transaction (11) Response:

#### Exit Reversal Mode Request {#exit-reversal-mode-request .h4}

  API Field \#, Value   Description
  --------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36               Transaction Type
  0007,1                Transaction Amount
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s05_icc_declines_and_simplify_reversal_mode/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519           Transaction Date (current date) -- MMDDYY
  0014,150258           Transaction time (current time) -- HHMMSS

\

#### Void Transaction Response {#void-transaction-response .h4}

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                           Description
  --------------------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,11                                       Transaction Type

  0002,20.00                                    Transaction

  0003,;541333\*\*\*0011=2512601MUYytYLBrXYG?   Account Data

  0007,35                                       Reference Number

  0011,xxx..                                    User Data. See [Simplify-Controlled Field
                                                Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s05_icc_declines_and_simplify_reversal_mode/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  0013,022519                                   Transaction date(current date) -- MMDDDYY

  0014,135718                                   Transaction time (current time) -- HHMMSS

  0017,0                                        Cash Back Amount

  0047,5;1;1;1;0;1;5;1;1;3;\*;C                 POS Data Code

  0052,0                                        Transponder / Proximity Indicator (0 = contact; 2 = contactless; 5 = swiped)

  0054,05                                       POS Entry Mode (EMV Tag 9F39)

  0055,9                                        PIN Capabilities

  0057,0                                        ICC Chip Condition Code

  0109,RETAIL                                   Terminal ID

  0110,205                                      Cashier ID

  0115,10                                       Transaction Qualifier

  0163,EN                                       Cardholder Language Preference (EMV Tag 5F2D)

  1002,MTIP06 MCD 13A                           Cardholder Name

  1300,DD38ED49BCA8EA20                         Application Cryptogram (EMV Tag 9F26)

  1302,251231                                   Application Expiration Date (EMV Tag 5F24)

  1303,410302                                   Cardholder Verification Method (CVM) Results (EMV Tag 9F34)

  1305,0210A5800F040000000000000000000000FF     Issuer Application Data (EMV Tag 9F10)

  1306,E0F8C8                                   Terminal Capabilities (EMV Tag 9F33)

  1307,0000008000                               Terminal Verification Results (TVR) (EMV Tag 95)

  1312,840                                      Terminal Country Code (EMV Tag 9F1A)

  1313,03                                       Application PAN Sequence Number (EMV Tag 5F34)

  1317,0002                                     Terminal Application Version Number (EMV Tag 9F09)

  1318,00000070                                 Transaction Sequence Counter (EMV Tag 9F41)

  1319,3000                                     Application Interchange Profile (EMV Tag 82)

  1320,0027                                     Application Transaction Counter (ATC) (EMV Tag 9F36)

  1321,80                                       Cryptogram Information Data (EMV Tag 9F27)

  1322,22                                       Terminal Type (EMV Tag 9F35)

  1323,65058BBD                                 Unpredictable Number (EMV Tag 9F37)

  1325,A0000000041010                           ICC Application Identifier (AID) (EMV Tag 4F)

  1326,MasterCard                               ICC Application Preferred Name (EMV Tag 9F12)

  1327,MASTERCARD                               Terminal Application Label (EMV Tag 50)

  1328,A0000000041010                           Terminal Application Identifier (AID) (EMV Tag 9F06)

  1332,FF00                                     Application Usage Control (EMV Tag 9F07)

  1334,E800                                     Transaction Status Information (EMV Tag 9B)

  1350,F1                                       CA Public Key Index (EMV Tag 8F)

  1354,03                                       ICC Public Key Exponent (EMV Tag 9F47)

  1357,840                                      ICC Transaction Currency (EMV Tag 5F2A)

  1358,00                                       Cryptogram Tran Type (EMV Tag 9C)

  1361,0056                                     Issuer Currency Code EMV Tag (5F56)

  1376,000000000000000\                         CVM List EMV Tag (8E)
  0410342031E031F00                             

  5002,70045363                                 Device Serial Number

  5004,G2                                       Encryption Provider ID

  5010,EMVDC0838                                EMV kernel version

  8002,EMVG2                                    Location Name (provided by Elavon)

  8006,CHAIN                                    Chain Code (provided by Elavon)
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Sample EMV Sale Message {#sample-emv-sale-message .h2}
-----------------------

A sample **Sale Request** and **Sale Response** for an approved EMV
transaction is shown below. Note concerning this sample:

-   The POS request to Simplify does not require modification for EMV.

-   Descriptions are given for response fields added to support EMV.

-   Additional fields, not shown in the samples, may also be sent to the
    POS for EMV.

-   For purposes of reference, EMV tags have been noted for potential
    EMV receipt fields.

### **Sample Message** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c04/s06_sample_emv_sale/c04_s05.html#sample-message"} {#sample-message .h3}

#### Request {#request-15 .h4}

\

  API Field \#, Value   Description
  --------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,02               
  0002,1.00             
  0007,219              
  0011,xxx..            User Data. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s06_sample_emv_sale/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  0013,022519           
  0014,143210           
  0017,0.00             
  0109,RETERM1          
  0110,205              
  0201,0.00             
  1008,ID:              
  5071,xxx...           Defines whether card and cardholder are present. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s06_sample_emv_sale/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s06_sample_emv_sale/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  8002,SIMTESTVOLT      
  8006,TSTLA3           

#### Response {#response-15 .h4}

\

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,02                             

  0002,1.00                           

  0003,ID:4979252177090148            

  0004,1217                           

  0006,CVI875                         

  0007,219                            

  0009,001                            

  0011,xxx..                          Field 11 is defined as User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s06_sample_emv_sale/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

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

  0163,fr                             Cardholder Language Preference (EMV Tag 5F2D)

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

  1300,2AF039B4B32A2DCC               Application Cryptogram (EMV Tag 9F26)

  1301,CD120BA4CDD06DFB0012           Issuer Authentication Data (EMV Tag 91)

  1302,171231                         Application Expiration Date (EMV Tag 5F24)

  1303,410302                         Cardholder Verification Method (CVM) Results (EMV Tag 9F34)

  1305,06010A03649C00                 Issuer Application Data (EMV Tag 9F10)

  1306,E0F8C8                         Terminal Capabilities (EMV Tag 9F33)

  1307,8000008000                     Terminal Verification Results (TVR) (EMV Tag 95)

  1312,124                            Terminal Country Code (EMV Tag 9F1A)

  1313,01                             Application PAN Sequence Number (EMV Tag 5F34)

  1314,A0000000031010                 Dedicated File Name (EMV Tag 84)

  1315,0001                           ICC Application Version Number (EMV Tag 9F08)

  1317,008C                           Terminal Application Version Number (EMV Tag 9F09)

  1318,00000190                       Transaction Sequence Counter (EMV Tag 9F41)

  1319,1C00                           Application Interchange Profile (EMV Tag 82)

  1320,05E1                           Application Transaction Counter (ATC) (EMV Tag 9F36)

  1321,40                             Cryptogram Information Data (EMV Tag 9F27)

  1322,22                             Terminal Type (EMV Tag 9F35)

  1323,D67895E4                       Unpredictable Number (EMV Tag 9F37)

  1325,A0000000031010                 ICC Application Identifier (AID) (EMV Tag 4F)

  1326,Credit                         ICC Application Preferred Name (EMV Tag 9F12)

  1327,VISA TEST                      Terminal Application Label (EMV Tag 50)

  1328,A0000000031010                 Terminal Application Identifier (AID) (EMV Tag 9F06)

  1332,FF80                           Application Usage Control (EMV Tag 9F07)

  1333,06152016                       Last Host EMV Key Download

  1334,6800                           Transaction Status Information (EMV Tag 9B)

  1339,00                             EMV Response Code (EMV Tag 8A)

  1357,124                            ICC Transaction Currency (EMV Tag 5F2A)

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

  1382,F000F0A001                     Additional Terminal Capabilities (EMV Tag 9F40)

  4747,04050                          

  5002,70117222                       

  5004,G2                             

  5010,EMVDC0838                      EMV kernel version

  5070,Merchant: Demo;\               Simplify Information. See [Simplify-Controlled Field
  Simplify: V-OG-2.02.02124;\         Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s06_sample_emv_sale/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  PARM: 2.21.1;TENDERDEF: 2.21.1;\    
  EMVPARM: EMVPARM-E4-1               

  5071,xxx...                         Defines whether card and cardholder are present. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s06_sample_emv_sale/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  5104,xxx...                         Tip Settings. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c04/s06_sample_emv_sale/../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  7007,1116189775452137               

  8002,SIMTESTVOLT                    

  8006,TSTLA3                         
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Pay-At-Table {#pay-at-table .h1}
============

Simplify supports Pay\@Table processing on Ingenico iWLxxx PIN Pads.

Pay\@Table transactions can be broken down into three steps (see
[Message
Flow](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c05/../../book/c05/s01_message_flow/c05_s01.html){.highlight}
for additional details):

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
    see [Message
    Details](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c05/../../book/c02/c02_message_details.html){.highlight}
    . The POS can also send a Void (11) or an Inquiry (22) after a host
    or Simplify timeout; for more information see under [Simplify
    Payment
    Processing](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c05/../../book/c05/s05/p04_simplify_payment_process/c05_s05_p04.html){.highlight}.

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

Message Flow {#message-flow .h2}
------------

![Message Flow for Simplify](Message%20Flow.png)

Transaction Flow {#transaction-flow .h2}
----------------

![Transaction Flow.png](Transaction%20Flow.png)

Field Formats and Description {#field-formats-and-description .h2}
-----------------------------

The following table gives formats/descriptions for all fields included
in Simplify Pay\@Table messages.

**Note:** Data Type = C refers to currency fields. These fields must
include an explicit decimal point.

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Field**      **Field Name** **Size**       **Data Type**  **Description**
  **\#**                                                      
  -------------- -------------- -------------- -------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001           Transaction    2              N              Simplify Tran Type.\
                 Type                                         Always 39 for Pay\@Table messages.

  0002           Transaction    1-14           C              Total transaction amount (includes Tip if any).\
                 Amount                                       The decimal point will be explicitly included as part of the data.

  0141           Currency Code  3              N              840=USD

  0201           Tip Amount     1-14           C              Entered or selected by customer.\
                                                              The decimal point is explicitly included in the data. Note that the POS must send this value separately in field 201 of the financial request.

  5002           Device Serial  1-20           A/N            PIN Pad serial number
                 Number                                       

  5100           Message Type   2              A/N            01=Login\
                                                              02=Get Check Info\
                                                              04=Logout/Disconnect\
                                                              05=Make Payment\
                                                              06=Print Receipt

  5101           Store ID       1-25           A/N            Optional field; may be blank or missing\
                                                              Only populated if a Store ID is defined under Simplify configuration.

  5102           Employee ID    1-20           A/N            Server ID

  5103           Service Type   1              N              Controls Simplify prompt displayed on the Get Check Information screen:\
                 Flag                                         00=Table and Check Number\
                                                              01=Check Number

  5104           Tip            1-8            A/N            Contains up to three one or two-digit percentages separated by semicolons (;)\
                 Percentages                                  The percentage sign is assumed.

  5105           Table Number   1-25           A/N            Entered at prompt

  5106           Check Number   1-25           A/N            Entered at prompt or selected from list

  5107           Merchant       1-2047         A/N            Data for merchant receipt.\
                 Receipt                                      Receipt lines are separated by the pound sign (\#). E.g. \#\# tells Simplify to print a blank line before beginning the next line.\
                                                              Receipt lines are printed using left justification. For center justification, pad with spaces.\
                                                              Note on Font Size: this is controlled by Simplify in the **Print Receipt Request**. See [Print Receipt
                                                              Message](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c05/s04_field_formats_and_descriptions/../../../book/c05/s05/p05_print_receipt/c05_s05_p05.html){.highlight}
                                                              for more information.

  5108           Customer       1-2047         A/N            Data for customer receipt. Same format as 5107.
                 Receipt                                      

  5110           POS Response   2              N              Response Code from POS:\
                 Code                                         00=approved\
                                                              Any other value=declined.

  5111           POS Response   1-50           A/N            Response Message from POS.\
                 Message                                      Displayed on PIN Pad.

  5114           Check          1-2047         A/N            Check Information sent in five subfields (separated by semicolons)\
                 Information                                  - Check number. (25 bytes maximum)\
                                                              - Amount due (includes explicit decimal point; if negative, the check is a refund) (14 bytes maximum)\
                                                              - Check receipt (5 bytes maximun)\
                                                              - Employee ID (10 bytes maximum)\
                                                              - Text data (30 bytes maximum)\
                                                              See under Get Check Information Message for more information.

  ...            Check          1-2047         A/N            Information for each check is sent in a separate field. Up to 99 checks can be processed per table or group, using fields 5114 through 5212.
                 Information                                  

  5213           Partial        1              N              0=Disabled; 1=Enabled
                 Payment Flag                                 

  5214           Tip Flag       1              N              0=Disabled; 1=Enabled

  5216           Group Number   1-2            N              Entered at prompt (optional)

  5217           Type of        2              N              Simplify Tran Type that should be sent by the POS:\
                 Transaction                                  01=Auth Only\
                                                              02=Sale\
                                                              09=Return (will be sent if the check is a refund)

  5218           Pay\@Table     1-8            N              Message number incremented for each Pay\@Table request (from Simplify or POS) and returned in each response message (if any). Used to match requests and responses.\
                 Message\                                     For **Print Receipt** messages, the Reference Number must match field 7 in the preceding financial response.
                 Reference                                    
                 Number                                       

  5219           Pay\@Table     1-8            N              Used if necessary to recover the correct session. Sent in **Login Response** and all subsequent messages until logout/disconnect. Incremented for each **Login Response**.
                 Session ID                                   
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

\

Message Summary {#message-summary .h2}
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

Message and Flow Details {#message-and-flow-details .h2}
------------------------

The following pages provide information on Pay at Table (39-xx) message
types, as follows:

-   The role of the message type in the Pay at Table transaction flow is
    described.

-   The message format is defined, and illustrated with one or more
    sample messages.

\

Login Request and Response (Tran Type 39-01) {#login-request-and-response-tran-type-39-01 .h2}
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

### **Login Response** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p01_login_request_and_response/c05_s05_p01.html#login-response"} {#login-response .h3}

A sample **Login Response** message is as follows:

  API Field \#, Value   Description
  --------------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,39               Transaction Type
  5100,01               Message Type
  5103,00               Service Type
  5104,xxx...           Tip Settings. See [Simplify-Controlled Field Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c05/s05/p01_login_request_and_response/../../../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.
  5110,00               POS Response Code
  5111,Approved         POS Response Message
  5213,1                Partial Payment Flag
  5214,1                Tip Flag
  5218,713              Pay\@Table Message Reference Number
  5219,12345678         Pay\@Table Session ID

\

Get Check Info Request and Response (Tran Type 39-02) {#get-check-info-request-and-response-tran-type-39-02 .h2}
-----------------------------------------------------

The **Get Check Information Request** is used to request check data from
the POS. Depending on configuration, Simplify can request check
information by table number, check number or group number.

The **Get Check Information Response** returns a list of open checks.
Open checks can be presented as check numbers or as text descriptions
controlled by the POS.

### **Get Check Info Request** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p02_get_check_info_request_and_response/c05_s05_p02.html#get-check-info-request"} {#get-check-info-request .h3}

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

Make Payment Request (Tran Type 39-05) {#make-payment-request-tran-type-39-05 .h2}
--------------------------------------

A **Make Payment Request** message is sent by Simplify after transaction
information has been entered for a check (or part of a check if partial
payment is enabled and selected by the customer) and the customer has
approved the transaction amount.

There is no **Make Payment Response** message. The POS responds to a
**Make Payment Request** by sending a financial request to Simplify.

### **Make Payment Request** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p03_make_payment_request/c05_s05_p03.html#make-payment-request"} {#make-payment-request .h3}

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

Simplify Payment Process {#simplify-payment-process .h2}
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
(as defined under [Stand-in
Processing](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c05/s05/p04_simplify_payment_process/../../../../book/c03/c03_stand-in_processing.html){.highlight}).
Cashback is *not* supported on Pay\@Table transactions.

Print Receipt Request and Response (Tran Type 39-06) {#print-receipt-request-and-response-tran-type-39-06 .h2}
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

### **Print Receipt Request** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p05_print_receipt/c05_s05_p05.html#print-receipt-request"} {#print-receipt-request .h3}

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

### **Print Receipt Response** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p05_print_receipt/c05_s05_p05.html#print-receipt-response"} {#print-receipt-response .h3}

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

### Sample Receipt[]{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p05_print_receipt/c05_s05_p05.html#sample-receipt"} {#sample-receipt .h3}

A sample merchant receipt is shown below:

\

Logout/Disconnect Request and Response (Tran Type 39-04) {#logoutdisconnect-request-and-response-tran-type-39-04 .h2}
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

### **Logout/Disconnect Request** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p06_logout_disconnect_request/c05_s05_p06.html#logout-disconnect-request"} {#logout-disconnect-request .h3}

A sample **Logout/Disconnect Request** message is as follows:

  **API Field \#, Value**   **Description**
  ------------------------- -------------------------------------
  0001,39                   Transaction Type
  5002,80667323             Device Serial Number
  5100,04                   Message Type
  5102,2                    Employee ID
  5218,1826                 Pay\@Table Message Reference Number
  5219,11                   Pay\@Table Session ID

### **Logout/Disconnect Response** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s05/p06_logout_disconnect_request/c05_s05_p06.html#logout-disconnect-response"} {#logout-disconnect-response .h3}

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

Recovery {#recovery .h2}
--------

### **General Principles** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s06_recovery/c05_s06.html#general-principles"} {#general-principles .h3}

<!-- -->

<!-- -->

<!-- -->

<!-- -->

<!-- -->

### **Simplify Recovery Points and Actions** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c05/s06_recovery/c05_s06.html#simplify-recovery-points-and-actions"} {#simplify-recovery-points-and-actions .h3}

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
current rules (as defined under [Inquiry
Message](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c05/s06_recovery/../../../book/c02/s02_inquiry_message/c02_s02.html){.highlight}.

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

Informational Prompting {#informational-prompting .h1}
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

As described in Chapter 2 under [Non-Financial
Messages](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c06/../../book/c02/s11/c02_s11_non-financial_messages.html){.highlight},
all **Non-Financial** messages have the following generic format:

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  API Field \#, Value                 Description
  ----------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  0001,36                             Transaction Type 36. Non-Financial message

  0011,xxx..                          User Data. See [Simplify-Controlled Field
                                      Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c06/../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.\
                                      For Transaction Type 36, it will always include:\
                                      Positions 1-2 Message Type

  5001,xxx..                          Non-Financial Data.\
                                      The format of this field depends on the value of Message Type.
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Field 11 Subfield       Length                  Description
  ----------------------- ----------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  Message Type            2                       Always 14

  Sequence Number         3                       Transaction identifier

  Screen ID               3                       Not used

  Timeout Value/          3                       Request: Screen timeout in seconds (000=No timeout)\
  Completion Code                                 Response: Completion Code (000 = Success) See [Simplify-Controlled Field
                                                  Definitions](https://developer.elavon.com/#/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/versions/0da6edd4-8b7e-4669-b286-269926a2397b.rcosoomi/documents?simplify-developer-guide/book/c06/../../book/c12/s06/c10_s06_appendix_f_tran_type_and_message_type.html){.highlight}.

  VersionBuildInfo        Var                     Response only: '?' followed by Version and Build numbers
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

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

Tag 010 - Text with Optional Buttons {#tag-010---text-with-optional-buttons .h2}
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

### Field 5001 Format {#field-5001-format-1 .h3}

#### Request {#request-16 .h4}

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

#### Request {#request-17 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14123010120                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](https://developer.el |
|                                   | avon.com/#/api/861b65f6-c5a9-4c28 |
|                                   | -a4e8-5ad37253a475.rcosoomi/versi |
|                                   | ons/0da6edd4-8b7e-4669-b286-26992 |
|                                   | 6a2397b.rcosoomi/documents?simpli |
|                                   | fy-developer-guide/book/c06/s01_t |
|                                   | ag_010_-_text_with_optional_butto |
|                                   | ns/../../../book/c12/s06/c10_s06_ |
|                                   | appendix_f_tran_type_and_message_ |
|                                   | type.html){.highlight}.           |
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
|                                   | Definitions](https://developer.el |
|                                   | avon.com/#/api/861b65f6-c5a9-4c28 |
|                                   | -a4e8-5ad37253a475.rcosoomi/versi |
|                                   | ons/0da6edd4-8b7e-4669-b286-26992 |
|                                   | 6a2397b.rcosoomi/documents?simpli |
|                                   | fy-developer-guide/book/c06/s01_t |
|                                   | ag_010_-_text_with_optional_butto |
|                                   | ns/../../../book/c12/s06/c10_s06_ |
|                                   | appendix_f_tran_type_and_message_ |
|                                   | type.html){.highlight}.           |
+-----------------------------------+-----------------------------------+
| 5001,0100038880                   | Non-Financial Data                |
+-----------------------------------+-----------------------------------+

### **Sample Message (Eight Buttons)** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c06/s01_tag_010_-_text_with_optional_buttons/c06_s01.html#sample-message-eight-buttons"} {#sample-message-eight-buttons .h3}

#### Request {#request-18 .h4}

+-----------------------------------+-----------------------------------+
| API Field \#, Value               | Description                       |
+===================================+===================================+
| 0001,36                           | Transaction Type                  |
+-----------------------------------+-----------------------------------+
| 0011,14123010120                  | User Data. See                    |
|                                   | [Simplify-Controlled Field        |
|                                   | Definitions](https://developer.el |
|                                   | avon.com/#/api/861b65f6-c5a9-4c28 |
|                                   | -a4e8-5ad37253a475.rcosoomi/versi |
|                                   | ons/0da6edd4-8b7e-4669-b286-26992 |
|                                   | 6a2397b.rcosoomi/documents?simpli |
|                                   | fy-developer-guide/book/c06/s01_t |
|                                   | ag_010_-_text_with_optional_butto |
|                                   | ns/../../../book/c12/s06/c10_s06_ |
|                                   | appendix_f_tran_type_and_message_ |
|                                   | type.html){.highlight}.           |
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

Tag 011 - Static and Scrolling Text with Optional Buttons {#tag-011---static-and-scrolling-text-with-optional-buttons .h2}
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

### **Field 5001 Format** []{.anchor clipboard-text="https://developer.elavon.com/content/api/861b65f6-c5a9-4c28-a4e8-5ad37253a475.rcosoomi/documents/simplify-developer-guide/book/c06/s01a_tag_011/c06_s01a.html#field-5001-format"} {#field-5001-format .h3}

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

#### Request {#request-19 .h4}

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

#### Request {#request-20 .h4}
