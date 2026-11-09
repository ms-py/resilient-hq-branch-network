# CML portfolio export

Use **Resilient-HQ-Branch-portfolio-v2.yaml** for sharing. Earlier portfolio YAML revisions are superseded. Original exports, including the VTP-transparent source export, contain local host passwords and should remain private.

## Preparation

The sharing copy replaces four Linux PASSWORD assignments with REPLACE_LOCALLY, clears exported pyATS password fields, and removes running-configuration output headers. Replace host password placeholders locally before first boot; they are literal text, not prompts. IOS self-signed public certificates remain; no private key material was identified in the review.

## VLAN portability fix

The first revision did not restore VLAN names or VLAN 99. Both switches were changed to VTP transparent mode, saved, and re-extracted. V2 includes that mode and explicit VLAN definitions: HQ 10/20/30/99, branch 10/99. No manual VLAN creation was needed after the v2 import.

## Validation — November 7, 2026

V2 parses with nine nodes and nine links. I imported it as a separate lab, set local host passwords, and booted it. Console evidence confirmed correct switch VLAN names and transparent mode; two FULL OSPF neighbors on all three routers; successful four-packet HQ-to-branch, branch-to-server, and guest-to-gateway tests; and the expected four-packet guest-to-server failure.

Earlier failover evidence belongs to the original lab: primary metric 20, alternate metric 110, automatic preferred-path restoration, and 207/207 ping replies. A subsequent repeat test captured on November 8 showed the same path changes with 213/213 ping replies at a one-second interval; see the guide and screenshots 06–09. Duplicate host default routes were observed on the original lab; a prior rebuilt lab showed one per host, but no route-logic correction has been made.

Package updated November 8 with six additional screenshots: baseline, failure, restoration, ping summary, and VTP/VLAN evidence for both switches. Publishing drafts remain excluded.
