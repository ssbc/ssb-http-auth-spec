<!--
SPDX-FileCopyrightText: 2021 Andre 'Staltz' Medeiros

SPDX-License-Identifier: CC-BY-4.0
-->

# SSB HTTP Authentication

**Revision:** `$REVISION`

**Author:** Andre Medeiros <contact@staltz.com>

**License:** This work is licensed under a [Creative Commons Attribution 4.0 International License](http://creativecommons.org/licenses/by/4.0/).

## Abstract

SSB is a peer-to-peer system where there should not be a client-server distinction, but there are exceptions to this nature. "Pub servers" and "room servers" are nodes with privileged internet-wide presence that can provide replication and tunneled-connection services to several peers. Since these servers often also host a public HTTP interface, concern has been raised on how authenticated clients are to interact with these services over HTTP when requesting access-restricted resources. SSB HTTP Authentication is a protocol that utilizes both SSB muxrpc and HTTPS to grant an HTTP client (such as a browser) access to resources authorized for the SSB client peer.

## Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://tools.ietf.org/html/rfc2119).

## Table of contents
