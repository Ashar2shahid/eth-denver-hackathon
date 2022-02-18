# ETHDENVER COINGECKO AIRNODE WEB REQUEST DEMO

This repo contains the config files and parameters to interact with the coingecko airnode.

Each request will use the following parameters:

| Parameter     | Value                                                                                                           | Description                                                              |
|---------------|-----------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
| Airnode Rrp   | 0xC11593B87f258672b8eB02d9A723a429b15E9E03                                                                      | The address of the Airnode Request Response Protocol Contract            |
| Airnode       | 0xDB4d9ED032aDC7261b3f6D670E73251a7A716548                                                                      | The address of the coingecko airnode                                     |
| Airnode Xpub  | xpub6CneVR8ERgungaEsu6LwZo31xqVhvdmvr7VuYDLRW3SKqshok3GajDxxjWUxsbsoAsFmsWvjKfZKSczfc6pNpnUADo3NSTxknBf1d1pWmZk | The extended public key of the coingecko airnode                         |
| EndpointId    | 0xfb87102cdabadf905321521ba0b3cbf74ad09c5d400ac2eccdbef8d6143e78c4                                              | The endpointId of the get latest price endpoint                          |
| Sponsor       | Metamask Wallet address                                                                                         | The sponsor of the the requester contract                                |
| SponsorWallet | Derived from the Metamask Wallet address                                                                        | The wallet derived from the sponsor address using the airnode's mnemonic |
| Parameters    |  -                                                                                                              | "ethereum" encoded as bytes32                                            |


## Deploy the Requester contract

Deploy the requester contract using REMIX and input the Airnode Rrp address into the constructor

## Sponsor the requester contract on AirnodeRRP

Head over to the Airnode RRP page and set yourself as the sponsor of the requester contract

## Derive the sponsorWallet address

```
npx @api3/airnode-admin derive-sponsor-wallet-address \
  --airnode-xpub xpub6CneVR8ERgungaEsu6LwZo31xqVhvdmvr7VuYDLRW3SKqshok3GajDxxjWUxsbsoAsFmsWvjKfZKSczfc6pNpnUADo3NSTxknBf1d1pWmZk
  --airnode-address 0xDB4d9ED032aDC7261b3f6D670E73251a7A716548 
  --sponsor-address metamask address
```

## Encode the parameters

we need to encode the parameters to pass them onto the request, for now we will use 
`0x3162000000000000000000000000000000000000000000000000000000000000636f696e49640000000000000000000000000000000000000000000000000000657468657265756d000000000000000000000000000000000000000000000000` which is 
```
[{ name: 'coinId', type: 'bytes32', value: "ethereum" }]
```
encoded into bytes32 using the `@airnode-abi` library.

## Make the request

Now you can make the request and have it be fullfilled by the airnode.

