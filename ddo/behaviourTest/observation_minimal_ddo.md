
---

# **Minimal DDO v5 Map for Asset Publishing**

```
DDO (VerifiableCredential)
├── @context: (ignored; overwritten internally)
├── id: MUST equal DID(nftAddress + chainId)
├── type: "VerifiableCredential" (overwritten, but required field)
├── issuer: string (required but not validated)
├── version: string (required)

├── credentialSubject
│   ├── id: same as top-level id (optional but recommended)
│
│   ├── metadata
│   │   ├── created: string (ISO timestamp)
│   │   ├── updated: string (ISO timestamp)
│   │   ├── name: string
│   │   ├── description:
│   │   │   ├── @value: string
│   │   │   ├── @language: string
│   │   │   └── @direction: string
│   │   ├── type: string (e.g., "dataset")
│   │   ├── providedBy: string
│   │   ├── copyrightHolder: string
│
│   ├── version: string (required by type)
│
│   ├── services: [ Service ]
│   │   └── Service
│   │       ├── id: string
│   │       ├── type: "access"
│   │       ├── name: string
│   │       ├── datatokenAddress: string
│   │       ├── serviceEndpoint: string
│   │       ├── files: string (encrypted file list)
│   │       ├── timeout: number
│   │       ├── state: number (0)
│   │       └── credentials: [] (empty array)
│
│   ├── chainId: number
│   ├── nftAddress: string (checksummed)
│
│   └── credentials: [] (required by type, can be empty)
│
├── proof
│   ├── header: string
│   └── signature: string
```

---

# **Minimal required fields summary**

## **Top-level**

* `@context`
* `id`
* `type`
* `issuer`
* `version`
* `credentialSubject`
* `proof`

## **credentialSubject**

* `metadata`
* `version`
* `services`
* `credentials`
* `chainId`
* `nftAddress`

## **metadata**

* `created`
* `updated`
* `name`
* `description` (`LanguageValueObject`)
* `type`
* `providedBy`
* `copyrightHolder`

## **services[].service**

* `id`
* `type`
* `name`
* `datatokenAddress`
* `serviceEndpoint`
* `files`
* `timeout`
* `state`
* `credentials`

## **proof**

* `header`
* `signature`

---
