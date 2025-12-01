# **DDO v5 — Full Field List (key → usage comment)**

---

## **Top-level Verifiable Credential**

```md
@context: always overwritten during validation; input ignored.
id: required; must equal DID derived from nftAddress + chainId.
type: required; overwritten to "VerifiableCredential"; input meaning vague/conflict.
issuer: required by type; runtime does NOT validate.
version: required; main version indicator for DDO.
credentialSubject: required; core asset payload.
additionalDdos: optional; array of extra embedded VCs; not validated.
indexedMetadata: app-only; removed before validation; never part of VC.
proof: optional in runtime; required by types; SHACL ignores (vague/conflict).
```

---

## **credentialSubject**

```md
id: optional; usually same as top-level id; not validated.
metadata: required; SHACL-enforced for some mandatory fields.
version: required by type; ignored in v5 validation (vague/conflict).
services: required; SHACL validates core service fields only.
credentials: required by type; runtime ignores internal semantics (vague/conflict).
chainId: required; runtime validates.
nftAddress: required; must be valid checksummed EVM address.
event: optional; not validated; used as passive record.
datatokens: optional; used by app; not validated; exists in examples but not type (vague/conflict).
proof: present in type; runtime uses top-level proof instead (vague/conflict).
```

---

## **metadata**

```md
created: required; SHACL-required.
updated: required; SHACL-required.
name: required; SHACL-required.
providedBy: required; SHACL-required.
description: required by type; not SHACL-enforced (vague/conflict).
copyrightHolder: required by type; SHACL does not enforce.
type: required by type; SHACL may enforce depending on schema (vague/conflict).
displayTitle: optional; unvalidated.
author: optional; unvalidated.
license: optional; inner shape allowed; unvalidated by SHACL.
links: optional; unvalidated.
attachments: optional; unvalidated.
tags: optional; SHACL-optional (≤64).
categories: optional; unvalidated.
additionalInformation: optional; unvalidated.
algorithm: required only if asset type = algorithm (comment-level rule; not enforced).
```

---

## **Metadata.License**

```md
name: required.
ODRL: optional; unvalidated.
licenseDocuments: optional; unvalidated.
```

---

## **LanguageValueObject**

```md
@value: required.
@language: required.
@direction: required.
```

---

## **services[]**

```md
id: required; SHACL-required.
type: required; SHACL-required; (“access”, “compute”).
name: required by type; NOT SHACL-required (vague/conflict).
datatokenAddress: required; SHACL-required.
serviceEndpoint: required; SHACL-required.
files: required by type; NOT SHACL-required (vague/conflict).
timeout: required; SHACL-required.
state: required by type; runtime ignores semantics.
credentials: required by type; NOT SHACL-enforced (vague/conflict).
displayName: optional; unvalidated.
description: optional; unvalidated.
compute: optional; comments say required if type=compute; not enforced.
consumerParameters: optional; unvalidated.
additionalInformation: optional; unvalidated.
dataSchema: optional; comments say required for type=asset; not enforced.
inputSchema: optional; comments say required for algorithms; not enforced.
outputSchema: optional; comments say required for algorithms; not enforced.
```

---

## **Service.State enum**

```md
Active = 0
EndOfLife = 1
Deprecated = 2
RevokedByPublisher = 3
OrderingIsTemporaryDisabled = 4
AssetUnlisted = 5
```

---

## **compute**

```md
allowRawAlgorithm: required.
allowNetworkAccess: required.
publisherTrustedAlgorithmPublishers: required.
publisherTrustedAlgorithms: required.
```

---

## **PublisherTrustedAlgorithms**

```md
did: required.
serviceId: required.
filesChecksum: required.
containerSectionChecksum: required.
```

---

## **Algorithm**

```md
container: required.
language: optional.
version: optional.
consumerParameters: optional.
```

---

## **ConsumerParameter**

```md
name: required.
type: required.
label: required.
required: required.
description: required.
default: required.
options: required.
```

---

## **Option**

```md
<map any>: mixed types allowed; unvalidated.
```

---

## **Container**

```md
image: required.
tag: required.
entrypoint: required.
checksum: required.
```

---

## **RemoteObject**

```md
name: required.
fileType: required.
sha256: required.
mirrors: required.
displayName: optional.
description: optional.
additionalInformation: optional.
```

---

## **RemoteSource**

```md
type: required.
url: optional.
method: optional.
headers: optional.
ipfsCid: optional.
```

---

## **Credential (Access Control)**

```md
match_allow: optional; values "any"/"all".
match_deny: optional; values "any"/"all".
allow: optional; address/policy entries; not validated.
deny: optional; same.
```

---

## **CredentialAddressBased**

```md
type: 'address' required.
values: required.
```

---

## **CredentialPolicyBased**

```md
type: 'verifiableCredential' required.
requestCredentials: required.
```

---

## **RequestCredential**

```md
string OR DetailedCredential.
```

---

## **DetailedCredential**

```md
credential: optional.
policies: optional.
```

---

## **Policy**

```md
string OR PolicyDetail.
```

---

## **PolicyDetail**

```md
policy: required.
args: required.
```

---

## **PolicyArgs**

```md
type: required.
```

---

## **event**

```md
txid: optional.
block: optional.
from: optional.
contract: optional.
datetime: optional.
```

---

## **proof**

```md
header: required by type; SHACL does not check.
signature: required by type; SHACL does not check.
```

---

## **indexedMetadata (removed pre-validation)**

```md
nft: optional; app-only.
purgatory: optional; app-only.
stats: optional; app-only.
lastEvent: optional; app-only.
pricing: optional; legacy/app-only.
```

---
