# Proposed approach to testing
Writer: Eugeniu Rusu (Jolocom)

In order to ensure the developed / proposed SSI stack can be adopted correctly by the various involved agent developers, it is very important to have the correcty interop testing practices established.

In particular, we need to ensure that the agents are interoperable with regards to the following core aspects:
- The DID methods used by the agents need to be interoperable. I.e. regardless of what DID method is used by an agent, the other party must be able to resolve the DID to a spec compliant DID Document.  
- The supported [Verifiable Credential](https://www.w3.org/TR/vc-data-model/) format(s), as well as the outlined signature suites ([proof types](https://w3c-ccg.github.io/ld-cryptosuite-registry/)). Agents should be able to request and verify Verifiable Credentials regardless of the software component / agent implementation used as part of the issuance process.
- The protocols used for issuing and requesting Verifiable Credentials (Aries RFC [0453](https://github.com/hyperledger/aries-rfcs/tree/main/features/0453-issue-credential-v2) and [0454](https://github.com/hyperledger/aries-rfcs/tree/main/features/0454-present-proof-v2)). As well as further pre-requisites (e.g. [RFC 0023](https://github.com/hyperledger/aries-rfcs/tree/main/features/0023-did-exchange), [0434](https://github.com/hyperledger/aries-rfcs/tree/bed4989dd6517f7a9de3696800e57e4c6ef49231/features/0434-outofband) for exchanging DIDs / establishing relationships between DIDs).
- The messaging format used to securely exchange messages between agents ([DIDComm V2](https://identity.foundation/didcomm-messaging/spec/)). Agends should be able to encrypt / decrypt messages exchanged as part of interactions.

Certain layers / building blocks can be tested for compliance to the underlying specification independently, using bespoke / dedicated test suites. More specifically:
- Various Verifiable Credential implementations can be tested for specification compliance using the [VC-test suite](https://github.com/w3c/vc-test-suite) hosted by the W3C ([current reports](https://w3c.github.io/vc-test-suite/implementations/) can be found here).
- Various [DID Method](https://www.w3.org/TR/did-core/) implementations can be tested for compliance to the DID specification using the test suite maintained by the W3C DID Working Group ([current reports](https://w3c.github.io/did-test-suite/) can be found here).

Nontheless, in order to ensure that all relevant building blocks are used / connected correctly, an end to end testing approach is required. The most promising starting point is the AATH initiative, i.e.:
- [Aries Agent Test Harness](https://github.com/hyperledger/aries-agent-test-harness) can be used to test interoperability between different agent implementations across an entire interaction.
    - Allows SSI agents to be integrated, and tested (potentially in combination with other agent implementations) in the context of a specific interaction.
    - A number of existing [SSI agents](https://github.com/hyperledger/aries-agent-test-harness/tree/main/aries-backchannels), including  agents used in the consortium are already integrated with the test harness.
    - A number of RFCs / protocols we intend to use are already defined as part of existing [feature list](https://github.com/hyperledger/aries-agent-test-harness/tree/main/aries-test-harness/features). 

The current intention is to prioritize build on the existing Aries Agent Test Harness. We envision expanding the current test suite to:
- Account for the next iteration of the interoperability profile, i.e.
    - Support for the DIDComm V2 messaging format, and the associated (minor) resulting protocol modifications.
    - Support for the selected revocation approach(es).
