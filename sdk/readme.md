# SDK Usage

## How to create a Hyperledger Fabric channel

### steps of a channel create:
- run the configtxgen tool to generate a genesis block
- run the configtxgen tool to generate an initial binary configuration definition
- get a sign-able channel definition in one of two ways
    - use the initial binary channel configuration definition
        - use the fabric-client SDK to extract the sign-able channel definition from the initial binary channel configuration definition
    - build a custom definition
        - use the configtxlator to convert the initial binary channel configuration definition to readable text
        - edit the readable text more info
        - use the configtxlator to convert the edited text to a sign-able channel definition
- use the fabric-client SDK to sign the sign-able channel definition
- use the fabric-client SDK to send the signatures and the sign-able channel definition to the orderer
- use the fabric-client SDK to have the peer join the channel
- then new channel may be used