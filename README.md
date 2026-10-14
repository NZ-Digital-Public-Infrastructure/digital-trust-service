# The Digital Credential Digital Trust Service

<span style="color:red">**Tracking notes [to remove]:**<br/>
Updated VICAL URLs added, can't publish until redirects are in place<br/>
Finalise link to the relying party technical guide
</span>


## Purpose
The New Zealand Government Digital Trust Service (DTS) is operated as part of the [Digital Public Infrastructure](https://github.com/NZ-Digital-Public-Infrastructure/.github/blob/main/profile/README.md) (DPI) to provide an authoritative source of credential issuing authorities who are accredited under the [Digital Identify Services Trust Framework (DISTF)](https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation).

In the digital credentials ecosystem, the DTS fulfils the role of the Trust Register. Relying party products that consume digital credentials can refer to the DTS to identify whether a presented credential is DISTF accredited.   

Refer to our [Relying Party technical guide](/Govt.nz%20app%20relying%20party%20guide.md) page for documentation of how to verify credentials held in the Govt.nz app wallet.

![Digital credential ecosystem diagram](/assets/ecosystem-diagram-trust-register-highlight.png "Digital credential ecosystem diagram")

## How does the DTS work?
The DTS provides a Verified Issuer Certificate Authority List (VICAL) that contains all the Issuing Authority Certificate Authority (IACA) certificates used in the issuance of DISTF accredited credentials. A VICAL is defined in the [ISO/IEC 18013-5](https://www.iso.org/standard/69084.html) standard as a means for relying parties to establish trust for mDoc credentials issued by multiple different issuers. It is a cryptographically signed list of IACAs, including details of the issuing authority and applicable credential document types for each IACA.  

Relying party software can automatically download the VICAL on a regular basis to use as a reference for credential validity checks.

A new online register to provide a web-based view of DISTF accreditations will be provided in 2026.

## Who should use the DTS?
The DTS should be used by any organisation that provides products for relying parties to verify digital credentials in New Zealand. The DTS provides assurance that a credential issuer has been independently reviewed and accredited to provide digital identity services that comply with the:

* [Digital Identity Services Trust Framework Act 2023](https://www.legislation.govt.nz/act/public/2023/13/en/latest/#LMS459583)
* [Digital Identity Services Trust Framework Regulations 2024](https://www.legislation.govt.nz/regulation/public/2024/0197/latest/LMS989612.html)
* [Digital Identity Services Trust Framework Rules in place at the time of accreditation](https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation)
* [Identification standards](https://www.digital.govt.nz/standards-and-guidance/identity/identification-management/identification-standards/)

Credentials that have been accredited with an appropriate level of assurance may be used for age verification for the sale and supply of alcohol and other purposes. Refer to the [using digital credentials for age verification](#using-digital-credentials-for-age-verification) section for more details. 

## Using the DTS
### Development
The DTS is provided through the [All of Government Digital Credential Issuance Platform (DCIP)](https://github.com/NZ-Digital-Public-Infrastructure/nz-digital-credential-issuance-platform), hosted on the MATTR VII platform. [MATTR VII](https://learn.mattr.global/docs/digital-trust-service/vical-consumption) documentation provides general instructions for how to consume a VICAL and load IACAs into verification products.

### Testing
A sandbox version of Digital Public Infrastructure products are provided for use during development and testing of digital credentials. See our [DPI Sandbox Guide](https://github.com/NZ-Digital-Public-Infrastructure/.github/blob/main/profile/sandbox/Sandbox%20User%20Guide.md) for details of the test products.

Credential issuers can get their test issuing party details added to the sandbox version of the VICAL to facilitate full end-to-end testing of their credential and its use by relying parties.

## VICAL

### Sandbox
The sandbox VICAL can be downloaded here:

```
https://sandbox.tfa.digital.govt.nz/e0b4fc11-8c0c-4d4d-9615-0b7d0af0661c/vicals/public/latest
```

The sandbox DTS root CA certificate can be retrieved here:

```
https://sandbox.tfa.digital.govt.nz/public/certificates/ca
```

### Production
The production VICAL can be downloaded here:

```
https://tfa.digital.govt.nz/cf4e1b17-b982-4b2e-bbda-b4f32083fd4b/vicals/public/latest
```
The sandbox DTS root CA certificate can be retrieved here:

```
https://tfa.digital.govt.nz/public/certificates/ca
```

## Verification responsibilities
It is the responsibility of the relying party to ensure they are accepting credentials that are legally applicable to their verification purpose.

### Using digital credentials for age verification

The [Sale and Supply of Alcohol Regulations 2013](https://www.legislation.govt.nz/secondary-legislation/pco-drafted/2013/459/en/latest/#LMS1618108) defines the requirements for a digital credential that may be used as an approved evidence of age document. 

> **5A Eligible credential**
> This regulation applies to a credential if—
> 
> (a) it is issued by an accredited digital identity service; and
> 
> (b) it contains a photograph of the person to whom it is issued; and
> 
> (c) it contains information purporting to relate to the person’s age or to be the person’s date of birth; and
> 
> (d) the information referred to in paragraphs (b) and (c) meets the requirements of the standard+, strong+, or very strong level of assurance as determined by the TF authority under the Digital Identity Services Trust Framework Act 2023.

The requirements of the Sale and Supply of Alcohol evidence of age are also referred to in other legislation that require proof of age:

| Act | Context |
|-----|---------|
| [Gambling Act 2003](https://www.legislation.govt.nz/act/public/2003/0051/latest/whole.html) | Applies to age 18+ restriction on instant games (section 301) and gaming machines (class 4 gambling, section 302), and age 20+ restriction on casino gambling areas  |
| [Racing Industry Act 2020](https://www.legislation.govt.nz/act/public/2020/0028/latest/whole.html) | Applies to age verification at TAB and racing venues |
| [Smokefree Environments and Regulated Products Act 1990](https://www.legislation.govt.nz/act/public/1990/0108/latest/whole.html) | Applies to age verification for the sale of tobacco and vaping products (section 40) |
| [Health Act 1956](https://www.legislation.govt.nz/act/public/1956/0065/latest/whole.html) | Applies to age verification for commercial artificial UV tanning (sunbed) services under section 114 |

The DTS content will allow confirmation that a presented credential fulfils the accreditation requirement under regulation 5A(a). The relying party product can confirm that the credential includes claims that satisfy 5A(b) and 5A(c). 

> [!IMPORTANT]
> To preserve user privacy, relying parties should use zero-knowledge proof principles when verifying credentials. For age verification this means checking for `age_over_nn` boolean claim values instead of date of birth.

There is no standardised way for conveying the Level of Assurance (LoA) for an accredited credential in a VICAL. Details of LoA for the accredited credentials will be published in the DTS online register when it is available, to facilitate understanding of whether the credential meets the requirement of regulation 5A(d). The LoA for credentials associated with IACAs in the VICAL will also be published on this page. 

### Costs
There is no fee for use of the DTS.

### Support

Contact the DPI team at [issuance@gdda.govt.nz](mailto:issuance@gdda.govt.nz) for assistance during development and testing, or operational support of production services.

## Links
[Digital Public Infrastructure](https://github.com/NZ-Digital-Public-Infrastructure/.github/blob/main/profile/README.md)

[Digital Identify Services Trust Framework (DISTF)](https://www.publicservice.govt.nz/about-the-commission/government-digital-delivery-agency/trust-framework-for-digital-identity/about-digital-identity-services/trust-framework-legislation)

[DISTF Draft Reference Architecture](https://github.com/nz-trust-framework/DISTF-reference-architecture/blob/main/README.md)
