# Gihub action - Release-Drafter pour Beneva
## Configuration
Pour appeler ce workflow réutilisable, vous n'avez qu'à appeler le répertoire X@main?vY avec un workflow qui se déclanche lors de:

	on:
		push:
			branches:
			- main
		pull_request:
			types: [opened, reopened, synchronize]

## Paramètres
### Inputs
	Nom: is_collection
	Type: Booléen
	Requis: Non
	Valeur par défaut: false
	Description: Est-ce que le répertoire est une collection ansible qui contient un galaxy.yml?

### Outputs
	N/A