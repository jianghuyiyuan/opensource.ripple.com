---
seo:
    description: Create or update a Permissioned Domain.
labels:
  - Compliance
  - Permissioned Domains
---
# PermissionedDomainSet
[[Source]](https://github.com/XRPLF/rippled/blob/develop/src/xrpld/app/tx/detail/PermissionedDomainSet.cpp "Source")

A PermissionedDomainSet transaction creates or modifies a [Permissioned Domain](./index.md).

_(Requires the PermissionedDomains amendment {% not-enabled /%})_

## Example {% $frontmatter.seo.title %} JSON

```json
{
  "TransactionType": "PermissionedDomainSet",
  "Account": "rf1BiGeXwwQoi8Z2ueFYTEXSwuJYfV2Jpn",
  "Fee": "10",
  "Sequence": 390,
  "AcceptedCredentials": [
    {
        "Credential": {
            "Issuer": "ra5nK24KXen9AHvsdFTKHSANinZseWnPcX",
            "CredentialType": "6D795F63726564656E7469616C"
        }
    }
  ]
}
```

<!-- TODO: {% tx-example txid="TODO" /%} -->

{% raw-partial file="/docs/_snippets/tx-fields-intro.md" /%}

| Field                 | JSON Type         | [Internal Type][] | Required? | Description |
|:----------------------|:------------------|:------------------|:----------|:------------|
| `DomainID`            | String - [Hash][] | Hash256           | No        | The ledger entry ID of an existing Permissioned Domain to modify. If omitted, create a new Permissioned Domain. |
| `AcceptedCredentials` | Array             | Array             | Yes       | A list of 1 to 10 [**Accepted Credentials objects**](#accepted-credentials-objects) that grant access to this Domain. The list does not need to be sorted, but it cannot contain duplicates. When modifying an existing domain, this list replaces the existing list. |

{% raw-partial file="/docs/_snippets/accepted-credentials-objects.md" /%}

## {% $frontmatter.seo.title %} Flags

There are no flags defined for {% $frontmatter.seo.title %} transactions.

## Error Cases

Besides errors that can occur for all transactions, {% $frontmatter.seo.title %} transactions can result in the following [transaction result codes](https://xrpl.org/docs/references/protocol/transactions/transaction-results):

| Error Code                | Description |
|:--------------------------|:------------|
| `tecDIR_FULL`             | The transaction would create a new PermissionedDomain, but the sender's owner directory is full. |
| `tecINSUFFICIENT_RESERVE` | The transaction would create a new PermissionedDomain, but the sender does not have enough XRP to meet the increased owner reserve. |
| `tecNO_ENTRY`             | The transaction attempted to modify an existing Domain that does not exist. Check the `DomainID` field of the transaction. |
| `tecNO_ISSUER`            | At least one of the issuers specified in the `AcceptedCredentials` field is does not exist in the XRP Ledger. Check the `Issuer` field of each member of the array. |
| `tecNO_PERMISSION`        | The transaction attempted to modify an existing Domain, but the sender of the transaction is not the owner of the specified Domain. |


{% raw-partial file="/docs/_snippets/common-links.md" /%}
