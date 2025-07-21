<!-- SPDX-License-Identifier: MIT OR Apache-2.0 -->

# SecureDNA tools

[![License](https://img.shields.io/badge/license-MIT%2FApache--2.0-informational?style=flat-square)](COPYRIGHT.md)

This repo holds various public tools related to
[SecureDNA](https://securedna.org) project.  It serves as a single
point to hold ancillary ecosystem-related artifacts which are either
updated on a different schedule than the main monorepo or which are
contributed by synthesis vendors, customers, or biosafety
officers. These may include input filters for handling
vendor-proprietary FASTA file formats, tools for generating exemption
certificates in various ways, analyzing the output of synthclient, and
so forth.

## Structure

- `synthclient/`: tools related to synthclient
  - `input-filters/`: Tools which transform vendor-proprietary FASTA formats into the generic format accepted by `synthclient`
    - `multivendor/`: A common filter for Eurofins/IDT formats
  - `manage-exemptions/`: A tool for users who want to manage their customers' exemptions. It augments requests with 2FA OTPs.
