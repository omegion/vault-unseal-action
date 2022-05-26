# ArgoCD Application Actions

[![GitHub Marketplace](https://img.shields.io/badge/Marketplace-Find%20and%20Replace-blue.svg?colorA=24292e&colorB=0366d6&style=flat&longCache=true&logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAA4AAAAOCAYAAAAfSC3RAAAABHNCSVQICAgIfAhkiAAAAAlwSFlzAAAM6wAADOsB5dZE0gAAABl0RVh0U29mdHdhcmUAd3d3Lmlua3NjYXBlLm9yZ5vuPBoAAAERSURBVCiRhZG/SsMxFEZPfsVJ61jbxaF0cRQRcRJ9hlYn30IHN/+9iquDCOIsblIrOjqKgy5aKoJQj4O3EEtbPwhJbr6Te28CmdSKeqzeqr0YbfVIrTBKakvtOl5dtTkK+v4HfA9PEyBFCY9AGVgCBLaBp1jPAyfAJ/AAdIEG0dNAiyP7+K1qIfMdonZic6+WJoBJvQlvuwDqcXadUuqPA1NKAlexbRTAIMvMOCjTbMwl1LtI/6KWJ5Q6rT6Ht1MA58AX8Apcqqt5r2qhrgAXQC3CZ6i1+KMd9TRu3MvA3aH/fFPnBodb6oe6HM8+lYHrGdRXW8M9bMZtPXUji69lmf5Cmamq7quNLFZXD9Rq7v0Bpc1o/tp0fisAAAAASUVORK5CYII=)](https://github.com/omegion/vault-unseal-action)
[![Actions Status](https://github.com/omegion/vault-unseal-action/workflows/Integration%20Test/badge.svg)](https://github.com/omegion/vault-unseal-action/actions)

This action will unseal your HashiCorp Vault Server.

## Usage

### Example workflow

This example unseals your Vault server periodically every hour.

```yaml
name: Unseal Vault Server Every Hour
on:
  schedule:
    - cron:  '0 * * * *'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Unseal Vault Server
        uses: omegion/vault-unseal-action@v1
        with:
          address: "vault.example.com"
          shard1: ${{ secrets.VAULT_SHARD_1 }}
          shard2: ${{ secrets.VAULT_SHARD_2 }}
          shard3: ${{ secrets.VAULT_SHARD_3 }}
          image: latest
```

### Inputs

| Input     | Description                           |
|-----------|---------------------------------------|
| `address` | Vault server address.                 |
| `shard1`  | Vault shard.                          |
| `shard2`  | Vault shard.                          |
| `shard3`  | Vault shard.                          |
| `image`   | vault-unseal image (default: latest). |

## Examples

### Unseal Vault Server Periodically

You can sync ArgoCD application after building an image etc.

```yaml
name: Unseal Vault Server Every Hour
on:
  schedule:
    - cron:  '0 * * * *'

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Unseal Vault Server
        uses: omegion/vault-unseal-action@v1
        with:
          address:  ${{ secrets.VAULT_ADDR }}
          shard1: ${{ secrets.VAULT_SHARD_1 }}
          shard2: ${{ secrets.VAULT_SHARD_2 }}
          shard3: ${{ secrets.VAULT_SHARD_3 }}
          image: latest
```

## Publishing

To publish a new version of this Action you need to change the `image` input according to `vault-unseal` [releases](https://github.com/omegion/vault-unseal/releases)
