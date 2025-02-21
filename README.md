# Custom App-IDs
This is a repository containing custom Application IDs used in Palo Alto Firewalls. These can allow us to detect application shifts, and investigate SSL or uncategorized traffic for additional vulnerabilities, data patterns, or viruses.

## Status 
These are all still considered works in progress. Some of them are just for identifying and don't enable any additional features. This is dependent upon its characteristics; for instance, if it's capable of file transfer, we would enable scanning for viruses. Whereas if it's something like Splunk that might inherently contain sensitive information, we might purposefully ensure that scanning for data patterns is disabled. Below is a list of common statuses, others may be introduced as this matures.

* Complete - no further developement/modifications expected. Covers all intended use cases.
* Maintenance Only - covers intended use cases and no major re-work needed. Continue to monitor for application changes and update as needed.
* Partial - covers some intended use cases, or may not persist across sessions properly and create unintended application shifts. Further Development needed. 
* Experimental - recently created or created and not validated. Expected to cover intended use cases, but untested/unvalidated.

## Current App-IDs 

| App Name | Requires Decryption | Status | Category | Sub Category | Default Protos/Ports |
| -------- | ------------------- | ------ | -------- | ------------ | -------------------- |
| 1password-connect | yes[^1] | Complete | business-systems | data-privacy | tcp/80, tcp/8080, tcp/443, tcp/8443|
| icmp-timestamp | no | Complete | ip-protocol | networking | ip_proto/13, ip_proto/14 |
| pihole-web | yes[^1] | Maintenance Only | it-infrastructure | networking | tcp/80, tcp/443 |
| pkgbuild | no[^2] | Maintenance Only | software-updates | business-systems | tcp/80, tcp/443 |
| proxmox-base | yes | Maintenance Only | it-management | networking | tcp/8006 |
| splunk-enterprise | yes[^1] | Maintenance Only | it-management | networking | tcp/80, tcp/443, tcp/8000, tcp/8443 |
| truenas-base | yes | Maintenance Only | it-management | networking | tcp/443 |
| verizon-apn-update [^2] | no | Partial | it-infrastructure | networking | tcp/5223 |
| proxmox-vnc [^3] | yes | Experimental | remote-access | networking | tcp/8006, tcp/5000-5999 |



[^1]: SSL is not enabled by default for this application. Required when SSL has been manually enabled, otherwise not required.
[^2]: Signature matches based on Server Name Identifier (SNI) field, decryption is optional but recommended.
[^3]: Experimental App-ID used to detect application shifts within a custom App-ID; experiencing unexpected behavior.

## Formats
App-IDs will be provided in multiple formats to include:

* XML
    * Can be used for interacting with the API.
* CLI
    * Can be used for copy-pasting into the CLI.
* Raw Config (json-esque, but not json)
    * Can be used as a reference/manually transposing to desired form.