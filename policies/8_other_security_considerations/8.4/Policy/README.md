# 8.4 Ensure the key vault is recoverable

## Policy Effects
Audit
Disabled

## Azure Policy Docs
See more information and a complete walk-through of deploying Policy programmatically at
[docs.microsoft.com](https://docs.microsoft.com/azure/governance/policy/samples/allowed-custom-images).

### Description: 
The key vault contains object keys, secrets and certificates. Accidental unavailability of a
key vault can cause immediate data loss or loss of security functions (authentication,
validation, verification, non-repudiation, etc.) supported by the key vault objects.
It is recommended the key vault be made recoverable by enabling the "Do Not Purge" and
"Soft Delete" functions. This is in order to prevent loss of encrypted data including storage
accounts, SQL databases, and/or dependent services provided by key vault objects (Keys,
Secrets, Certificates) etc., as may happen in the case of accidental deletion by a user or from
disruptive activity by a malicious user.

### Rationale: 
There could be scenarios where users accidentally run delete/purge commands on key vault
or attacker/malicious user does it deliberately to cause disruption. Deleting or purging a
key vault leads to immediate data loss as keys encrypting data and secrets/certificates
allowing access/services will become non-accessible. There are 2 key vault properties that
plays role in permanent unavailability of a key vault.
1> enableSoftDelete:
Setting this parameter to true for a key vault ensures that even if key vault is deleted, Key
vault itself or its objects remain recoverable for next 90days. In this span of 90 days either
key vault/objects can be recovered or purged (permanent deletion). If no action is taken,
after 90 days key vault and its objects will be purged.
2> enablePurgeProtection:
enableSoftDelete only ensures that key vault is not deleted permanently and will be
recoverable for 90 days from date of deletion. However, there are chances that the key
vault and/or its objects are accidentally purged and hence will not be recoverable. Setting
enablePurgeProtection to "true" ensures that the key vault and its objects cannot be
purged.
Enabling both the parameters on key vaults ensures that key vaults and their objects
cannot be deleted/purged permanently.

## Deploy with Azure portal

[![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/?#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmrajess%2FAzure-Policy-CIS%2Fmaster%2Fpolicies%2F8_other_security_considerations%2F8.4%2FPolicy%2Fazurepolicy.json)
[![Deploy to Azure Gov](https://docs.microsoft.com/azure/governance/policy/media/deploy/deployGovbutton.png)](https://portal.azure.us/?#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmrajess%2FAzure-Policy-CIS%2Fmaster%2Fpolicies%2F8_other_security_considerations%2F8.4%2FPolicy%2Fazurepolicy.json)