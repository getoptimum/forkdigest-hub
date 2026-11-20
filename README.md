# ForkDigest Hub

ForkDigest Hub is a lightweight repository for tracking and sharing
blockchain fork metadata in a single, structured place.

It holds digests and datasets for tracking Ethereum forks, network
upgrades, and consensus/execution changes. Right now it contains datasets
only — there are no scripts in the repo yet.

## Layout

```
eth/
  mainnet/
    forks.json                                # current + future fork digests
    peers.json                                # gateway peer list (snapshot)
    optimum_ethereum_mainnet_v0_1_peers.json  # versioned peer list
  hoodi/
    forks.json
    peers.json
    optimum_ethereum_hoodi_v0_1_peers.json
    optimum_hoodi_v0_2_peers.json
  plataberget/
    forks.json
```

## File formats

`forks.json` lists the fork digests seen on that chain, plus the next
expected one (empty when none is scheduled):

```json
{
  "forks": ["8c9f62fe"],
  "future_fork": ""
}
```

Each entry in a `peers.json` file is one gateway, with:

- `gateway_id` — the gateway's id (e.g. `ag_a5eea278753d03d0d7649b62c4511724`)
- `gateway_http_addr` — its HTTP address, port 48123
  (e.g. `34.155.148.124:48123`)
- `mump2p_addr` — a JSON-encoded string holding its libp2p `addrs` and
  `peerID`
- `cluster_id` — e.g. `optimum_ethereum_mainnet_v0_1`
- `chain_id` — `mainnet` or `hoodi`
- `version` / `commit_hash` — the gateway build
- `last_seen` — last time the gateway was seen, in UTC

The versioned peer files come in two forms,
`optimum_ethereum_<chain>_v*_peers.json` and
`optimum_<chain>_v*_peers.json`, and are the current lists per cluster;
`peers.json` is the unversioned snapshot.

## Contributing

Open a pull request that updates the matching `forks.json` or peer file for
the chain and cluster you are reporting on, keeping the existing JSON
shape. Small, verifiable updates beat large ones.

## Links

- Optimum: https://getoptimum.xyz
- Gateway docs: https://docs.getoptimum.xyz
- Optimum Gateway repo: https://github.com/getoptimum/optimum-gateway
