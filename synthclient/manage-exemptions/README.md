# manage-exemptions

This tool is for SecureDNA users (e.g. DNA providers) who want to manage their customers' exemptions.

## Background

Ordinarily, when placing an order that has an exemption, customers submit a six-digit 2FA code that gets forwarded to synthclient and checked by SecureDNA. However, a provider may with to manage [exemption tokens](https://github.com/SecureDNA/SecureDNA/wiki/Requesting-exemptions) instead of handing them out to its customers. In this case, the provider becomes responsible not only for requesting and approving exemptions on behalf of its customers, but also for keeping the 2FA secrets and generating six-digit codes.

This tool consists of a Bash shell script, `add-ets`, that helps out with this scenario.

## Using this tool

A provider should keep a directory of customer exemption tokens and associated "TOTP secret keys", as follows:

```
customers/
  johndoe/
    jd-2025-01-01.et
    jd-2025-01-01.secret
  genedoe/
    gd-2025-02-02.et
    gd-2025-02-02.secret
```

The names of the subdirectories should identify individual customers. For example, they can be usernames within your service.

The process of adding an exemption on behalf of a customer becomes as follows:

* In the [Request Tool](https://pages.securedna.org/exemption/request/), fill out the customer's information.
* When adding a TOTP 2FA method, click the QR code to copy the secret string to your clipboard. Hold onto this string for now, for example in a text editor.
* Specify the rest of the exemption and download the `.etr` file.
* Approve this file in the [Approval Tool](https://pages.securedna.org/exemption/approve/) using the _exemption cert_ you hold as a provider.
* Save the resulting `.et` file into the directory structure above.
* Save the secret string from your text editor into a `.secret` file with the same base name.

Now, the `add-ets` tool can automatically generate a six-digit OTP for a customer. Pass a synthclient request body on standard input:

```sh
echo '{"fasta": "ACTGACTGACTG", "region": "us"}' | ./add-ets /customers/genedoe
```

The result is a new synthclient request body with the customer's exemption token added:

```json
{
    "fasta": "ACTGACTGACTG",
    "region": "us",
    "ets": [
        {"et": "...", "requestor_otp": "123123"}
    ]
}
```

> [!NOTE]  
> The six-digit OTP is only valid for about a minute! The request should be passed on to synthclient as soon as possible.
