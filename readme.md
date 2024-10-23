# Safe Transaction DNS Whitelist

This repository houses the whitelist for signing Safe multisig transactions using the safe[.]global frontend. The whitelist is contained in `allowed-names.txt`.

## Understanding DNS and DNS Proxies

DNS (Domain Name System) is like the internet's phone book, translating human-readable domain names into IP addresses. In the context of web3 and cryptocurrency transactions, DNS plays a crucial role in connecting your device to various blockchain services and interfaces.

A DNS proxy acts as an intermediary between your device and DNS servers. It can filter requests, providing an additional layer of security by blocking access to known malicious domains.

## What Does This Whitelist Do?

The provided whitelist enables users to enforce strict DNS rules, allowing only the necessary traffic for signing Safe multisig transactions through the safe[.]global frontend. This ensures that the only network traffic permitted on the host is explicitly approved for the RPC and endpoints essential for utilizing the Safe frontend, giving you peace of mind.

## Why Use a DNS Whitelist?

Most public DNS resolvers use blacklists to block known malicious domains. However, this approach can be reactive and may not catch new threats immediately. By using a local whitelist, we take a proactive approach:

1. We explicitly allow only the domains necessary for Safe transactions.
2. This gives us granular control over our network's attack surface.
3. Any domain not on the whitelist is automatically blocked, significantly reducing the risk of connecting to malicious sites, facilitating malicious telemetry, or private key leakage due to a malicious process.

## Installing DNSCrypt-Proxy

DNSCrypt-Proxy is a flexible DNS proxy with strong encryption features. Here's how to install it:

1. Visit the [DNSCrypt-Proxy releases page](https://github.com/DNSCrypt/dnscrypt-proxy/releases).
2. Download the appropriate version for your operating system.
3. Extract the downloaded archive.
4. Navigate to the extracted folder and locate the `dnscrypt-proxy.toml` configuration file.
5. Replace the contents of `dnscrypt-proxy.toml` with the configuration provided in this repository.
6. Copy the `allowed-names.txt` file from this repository to the same directory as `dnscrypt-proxy.toml`.

For detailed, OS-specific installation instructions, refer to the [DNSCrypt-Proxy documentation](https://github.com/DNSCrypt/dnscrypt-proxy/wiki/Installation).

## Using This Whitelist

This repository contains a carefully curated whitelist (`allowed-names.txt`) designed for users executing Safe transactions on high-value multisig wallets. To use it:

1. Clone this repository or download the `allowed-names.txt` file.
2. Place `allowed-names.txt` in the same directory as your `dnscrypt-proxy.toml` file.
3. Ensure your `dnscrypt-proxy.toml` is configured to use this whitelist (see the provided configuration file).
4. Restart DNSCrypt-Proxy to apply the changes.


## Start the proxy

`sudo ./dnscrypt-proxy --config ./dnscrypt-proxy.toml`

NOTICE: Remember to change your clients DNS to point to `127.0.0.1`

## RPC endpoints
This whitelist was created for signing transactions on the BASE network, using the llamaRPC. While other networks should work if you use the llamaRPC, if you wish to use a custom RPC or network, ensure you add it to `allowed-names.txt`. 

## Enhanced Security by Design

By implementing these stringent DNS rules, you significantly reduce the risk of falling victim to various attacks:

1. **Phishing Protection**: Only whitelisted domains can be accessed, making it nearly impossible to accidentally visit a phishing site mimicking a legitimate service.

2. **Malware Mitigation**: Many types of malware need to communicate with command and control servers. With a strict whitelist, such communication attempts are blocked by default.

3. **Data Exfiltration Prevention and Privacy Protection**: 
   - If an infostealer or other malicious process attempts to send data to an unknown domain, it will be blocked.
   - The limited network access due to the whitelist significantly reduces the risk of transaction data or private key leakage.
   - Malicious processes are prevented from communicating with their command and control (C2) servers, effectively neutralizing their ability to exfiltrate sensitive information or receive further instructions.
   - This approach creates a secure environment where even if a system is compromised, the attacker's ability to extract valuable data or control the malware is severely limited.

4. **Reduced Attack Surface**: By limiting connections to only necessary services, you dramatically reduce potential entry points for attackers.

Remember, while this approach significantly enhances security, it's not a silver bullet. A DNS whitelist works best with a **fresh** device. Always practice good operational security, use hardware wallets when possible, and stay informed about the latest security best practices in the web3 space.


## Disclaimer

This DNS whitelist and associated tools are provided "as is", without warranty of any kind, express or implied. The creators and contributors of this project are not liable for any damages or losses arising from the use or misuse of this software. Users are responsible for their own security practices and should exercise caution when dealing with cryptocurrency transactions. Always verify the integrity of your transactions and consult with security professionals when handling high-value assets.