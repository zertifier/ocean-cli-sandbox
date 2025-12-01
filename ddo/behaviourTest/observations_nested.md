# **DDO v5 — Fully Nested Field Map**

```
DDO (VerifiableCredential)
├── @context: overwritten during validation; user input ignored.
├── id: must equal DID (derived from nftAddress + chainId).
├── type: overwritten to "VerifiableCredential"; meaning vague/conflict.
├── issuer: required; not validated.
├── version: required; main DDO version indicator.
├── credentialSubject (object)
│   ├── id: optional; usually same as top-level id.
│   ├── metadata (object)
│   │   ├── created: required (SHACL).
│   │   ├── updated: required (SHACL).
│   │   ├── name: required (SHACL).
│   │   ├── providedBy: required (SHACL).
│   │   ├── description: required by type; NOT SHACL-enforced (conflict).
│   │   ├── copyrightHolder: required by type; NOT SHACL-enforced.
│   │   ├── type: required by type; runtime-dependent enforcement.
│   │   ├── displayTitle: optional.
│   │   ├── author: optional.
│   │   ├── license (object, optional)
│   │   │   ├── name: required.
│   │   │   ├── ODRL: optional.
│   │   │   └── licenseDocuments: optional.
│   │   ├── links: optional.
│   │   ├── attachments: optional.
│   │   ├── tags: optional (SHACL limits ≤64).
│   │   ├── categories: optional.
│   │   ├── additionalInformation: optional.
│   │   ├── algorithm (object, optional; required only for algorithm assets)
│   │   │   ├── container (object)
│   │   │   │   ├── image: required.
│   │   │   │   ├── tag: required.
│   │   │   │   ├── entrypoint: required.
│   │   │   │   └── checksum: required.
│   │   │   ├── language: optional.
│   │   │   ├── version: optional.
│   │   │   └── consumerParameters (array, optional)
│   │   │       └── ConsumerParameter (object)
│   │   │           ├── name: required.
│   │   │           ├── type: required.
│   │   │           ├── label: required.
│   │   │           ├── required: required.
│   │   │           ├── description: required.
│   │   │           ├── default: required.
│   │   │           └── options: required (Option objects; mixed types allowed).
│   ├── version: required by type; runtime ignores (conflict).
│   ├── services (array)
│   │   └── Service (object)
│   │       ├── id: required (SHACL).
│   │       ├── type: required (SHACL) — "access" or "compute".
│   │       ├── name: required by type; NOT SHACL-enforced (conflict).
│   │       ├── datatokenAddress: required (SHACL).
│   │       ├── serviceEndpoint: required (SHACL).
│   │       ├── files: required by type; NOT SHACL-enforced (conflict).
│   │       ├── timeout: required (SHACL).
│   │       ├── state: required by type; semantic ignored runtime.
│   │       ├── credentials (array, optional)
│   │       │   └── Credential (object)
│   │       │       ├── match_allow: optional ("any" / "all").
│   │       │       ├── match_deny: optional ("any" / "all").
│   │       │       ├── allow (array, optional)
│   │       │       │   ├── CredentialAddressBased
│   │       │       │   │   ├── type: "address".
│   │       │       │   │   └── values: required.
│   │       │       │   └── CredentialPolicyBased
│   │       │       │       │   ├── type: "verifiableCredential".
│   │       │       │       │   └── requestCredentials (array)
│   │       │       │       │       │   └── RequestCredential
│   │       │       │       │       │       ├── string OR
│   │       │       │       │       │       └── DetailedCredential (object)
│   │       │       │       │       │           ├── credential: optional.
│   │       │       │       │       │           └── policies (array)
│   │       │       │       │       │               └── Policy
│   │       │       │       │       │                   ├── string OR
│   │       │       │       │       │                   └── PolicyDetail (object)
│   │       │       │       │       │                       ├── policy: required.
│   │       │       │       │       │                       └── args (PolicyArgs)
│   │       │       │       │       │                           └── type: required.
│   │       │       ├── deny (array, optional)
│   │       │       │   └── same structure as allow.
│   │       ├── displayName: optional.
│   │       ├── description: optional.
│   │       ├── compute (object, optional; required only if type=compute)
│   │       │   ├── allowRawAlgorithm: required.
│   │       │   ├── allowNetworkAccess: required.
│   │       │   ├── publisherTrustedAlgorithmPublishers: required.
│   │       │   └── publisherTrustedAlgorithms (array)
│   │               └── PublisherTrustedAlgorithms (object)
│   │                   ├── did: required.
│   │                   ├── serviceId: required.
│   │                   ├── filesChecksum: required.
│   │                   └── containerSectionChecksum: required.
│   │       ├── consumerParameters: optional.
│   │       ├── additionalInformation: optional.
│   │       ├── dataSchema: optional; comments require for type=asset (not enforced).
│   │       ├── inputSchema: optional; comments require for algorithm (not enforced).
│   │       └── outputSchema: optional; comments require for algorithm (not enforced).
│   ├── credentials: required by type; ignored by runtime (conflict).
│   ├── chainId: required.
│   ├── nftAddress: required; must be valid EVM checksummed.
│   ├── event (object, optional)
│   │   ├── txid: optional.
│   │   ├── block: optional.
│   │   ├── from: optional.
│   │   ├── contract: optional.
│   │   └── datetime: optional.
│   ├── datatokens: optional; used in examples; not in type (conflict).
│   └── proof: exists in type; runtime uses top-level instead (conflict).
├── additionalDdos: optional array of nested VCs; not validated.
├── indexedMetadata (object; removed before validation)
│   ├── nft: optional; app-only.
│   ├── purgatory: optional.
│   ├── stats: optional.
│   ├── lastEvent: optional.
│   └── pricing: optional; legacy/app-only.
└── proof (object)
    ├── header: required by type; not SHACL-enforced.
    └── signature: required by type; not SHACL-enforced.
```

---
