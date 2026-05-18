# WellSpot Cosmos Client

This repository now uses nbdev so the source of truth can stay in notebooks while the importable module remains in `wellspot_cosmos_client`.

## Development Workflow

- Edit `nbs/00_client.ipynb`
- Export code with `nbdev_export`
- Keep `Cosmos_Wellspot_Client.ipynb` as a manual smoke-test only

## Hardcoded Inputs To Review

These values were previously embedded in notebook cells and are now isolated so they can be replaced cleanly:

- Key Vault URL passed to `SecretClientManager`
- Secret names in `SecretNames`
- Environment-to-container mapping created by the caller

## Example

```python
from wellspot_cosmos_client import (
    CosmosEnvironmentConfig,
    CosmosGraphClient,
    GremlinClientManager,
    SecretClientManager,
)

environment = CosmosEnvironmentConfig(
    database_name="<database-name>",
    container_name="<container-name>",
)

secret_client_manager = SecretClientManager(
    key_vault_url="https://<your-key-vault>.vault.azure.net/",
)

gremlin_manager = GremlinClientManager(
    environment=environment,
    secret_client_manager=secret_client_manager,
)

client = CosmosGraphClient(gremlin_manager)
info = client.endpoints.get_info()
```