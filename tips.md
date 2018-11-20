# tips

## docker

when docker daemon starting, it will give permission 
to a user group called 'docker'. 

// create user group
> sudo groupadd docker

// add current user to docker group
> sudo usermod -aG docker $USER

// refresh info
> newgrp docker

// restart
> sudo systemctl restart docker

// restart computer...


## shell

> xxx 2>>&1 | tee xxx.output
> xxx |& tee -a xxx.output.log

## Tool

### cryptogen

> cryptogen generate --config=./org4-crypto.yaml

```yaml
OrdererOrgs:
  # ---------------------------------------------------------------------------
  # Orderer
  # ---------------------------------------------------------------------------
  - Name: Orderer
    Domain: example.com
    # ---------------------------------------------------------------------------
    # "Specs" - See PeerOrgs below for complete description
    # ---------------------------------------------------------------------------
    Specs:
      - Hostname: orderer
# ---------------------------------------------------------------------------
# "PeerOrgs" - Definition of organizations managing peer nodes
# ---------------------------------------------------------------------------
PeerOrgs:
  # ---------------------------------------------------------------------------
  # Org4
  # ---------------------------------------------------------------------------
  - Name: Org4
    Domain: org4.example.com
    ## OrganizationalUnitIdentifier
    EnableNodeOUs: true  ## if true, will generate config.yaml under msp folder. 
    Template: 
      Count: 3    ## number of peers: peer0.org4, peer1.org4, ...
    Users: 
      Count: 2    ## number of users, admin, user0, user1.  admin is default account
  # ---------------------------------------------------------------------------
  # Org5
  # ---------------------------------------------------------------------------
  - Name: Org5
    Domain: org5.example.com
    EnableNodeOUs: true
    Template:
      Count: 2
    Users:
      Count: 1
```
this yaml config file will generate:

```
./crypto-config
  -- peerOrganizations
    -- org4.example.com
      -- ca
      -- msp
      -- peers
        -- peer0.org4.example.com
          -- msp
          -- tls
        -- peer1.org4.example.com
        -- peer2.org4.example.com
      -- tlsca
      -- users
        -- Admin@org4.example.com
        -- User1@org4.example.com
    -- org5.example.com
      ...
```

### configtxgen

> configtxgen -printOrg Org4MSP -configPath ./configtx.org4 > ../channel-artifacts/org4.json

in config path, crypto-config files(certs) should be included.

`default`

-configPath -> ./