# Managing SIP Peers (locations) {#top}

## Overview

* [About SIP Peers (locations)](#about)
* [Voice/Data Traffic](#voice-data-traffic)
* [SIP Peer configuration for use of Origination service](#orig-config)
* [SIP Peer configuration for use of Origination and SMS services](#orig-config-sms)
* [SIP Peer configuration for use of Termination service](#term-config)
* [SIP Peer configuration for use of Origination, Termination and SMS services](#term-orig-sms)
* [SIP Peer settings for Calling Name and other SIP Peer wide features](#cnam-config)
  * [Calling Name display](#cnam)
  * [Final Destination URI](#final-uri)
* [Deleting a SIP Peer](#delete-sippeer)
* [Moving TNs between SIP Peers](#move-tn)

## About {#about}

SIP Peer Management enables customers to configure and manage IP addresses and other attributes for their network connections to Bandwidth. Per section 9, the SIP Peer(s) are set up on the Site to manage the numbers assigned to the account.  In the User Interface, the SIP Peer is referenced as a Location instead of a SIP Peer just as a Site is referenced as a Sub Account.

A SIP Peer is a gateway that sends or receives voice and data traffic to or from Bandwidth’s network. Customer must configure a default SIP Peer on the Site within an Account. Before you can create a SIP Peer, a Site (location) must be created. You can have multiple SIP Peers on a Site. Only one default SIP Peer is allowed per Site.

Aside from being an administration point for IP addresses for network ingress and egress, SIP Peers are also used to associate Telephone Numbers with a Site/Location and Account.  **For a Site to order any Telephone Numbers, at least one SIP Peer must be created for the Site, and one of the SIP Peers needs to be designated as the “Default” SIP Peer with which to associate numbers.**

## Voice/Data Traffic {#voice-data-traffic}

There are three different types of customer calls and messages to and from Bandwidth:

1. Origination - Voice calls from PSTN phone numbers that are delivered to customer-owned telephone numbers.
2. Termination - Voice calls from customer-owned telephone numbers that are delivered to PSTN or other on-net telephone numbers.
3. SMS - Inbound text messages that are delivered to customer-owned telephone numbers and outbound text messages that are delivered to PSTN or other on-net telephone numbers

These services can be used independently.  The following sections outline how SIP Peers should be configured when different combinations of these services are used.

## SIP Peer configuration for use of Origination service {#orig-config}

Each SIP Peer can be configured with multiple IP addresses that will be used in managing traffic presentation to the Customer.

The traffic can be presented to the customer IP endpoints using one of two models – either as a Random distribution across the available voice host IP endpoints, or using a sequential failover model where traffic is preferentially presented to the first IP address until an endpoint failure is detected.

## SIP Peer configuration for use of Origination and SMS services {#orig-config-sms}

This section provides information on defining a SIP Peer for receiving inbound calls (from Bandwidth to customer) and text messages. In the example below, the same host is used for receiving and SMS messages. If there is a different host for origination and SMS, that fact can be identified in the tags. Multiple SMS Hosts and Voice Hosts are allowed as required.  The Termination Hosts field is identified with the DataAllowed element to permit SMS Data to flow in to the Bandwidth network.   The optional Port element is permitted if required.

**Note**: In spite of the Termination Hosts data, this configuration can be blocked from Termination traffic with account level constraints

## SIP Peer configuration for use of Termination service {#term-config}

To define a SIP Peer for sending outbound calls (from customer to Bandwidth, the configuration includes parameters called TerminationHosts, specifiying the IP address from which IP voice packets will be presented to the Bandwidth network.


## SIP Peer configuration for use of Origination, Termination and SMS services {#term-orig-sms}

A SIP Peer can also be configured for all services, namely the ability to send and receive both voice and text messages.

## SIP Peer settings for Calling Name and other SIP Peer wide features {#cnam-config}

A number of features can be established at the SIP Peer level, including Calling Name Display and Final Destination URI.

### Calling Name display {#cnam}

Enabling Calling Name display (CNAM) for all TNs subtending a SIP Peer is done by configuring the CallingName feature for the SIP Peer.   This involves setting the CNAM Display default behavior on or off (true or false) and then declaring whether that default behavior needs to be enforced or can be overridden at the TN level.

### Final Destination URI {#final-uri}

The network configuration of a SIP Peer includes an optional attribute called `finaldestinationuri`. This is used when network connectivity to all previously provided hosts/IPs fails. Request format for the configuration of the SIP Peer, using this attribute, is:

## Deleting a SIP Peer {#delete-sippeer}

A SIP peer can be deleted using the DELETE method.

**Note**:  A SIP peer can be deleted only if there are no TNs.

## Moving TNs between SIP Peers {#move-tn}

A <code class="post">POST</code> to the SIP Peer resource can be used to move Telephone Numbers between SIP Peers.
