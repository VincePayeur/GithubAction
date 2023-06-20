# Gihub action - Release-Drafter pour Beneva
## Configuration
Pour appeler ce workflow réutilisable, vous n'avez qu'à appeler le répertoire repertoire@main?vX avec un workflow qui se déclanche comme ceci:

	on:
	 push:
	  branches:
	  - main
	 pull_request:
	  types: [opened, reopened, synchronize]

	jobs:
	  Call_Release-Drafter_reusable_action:
	    permissions:
	      contents: write
	      pull-requests: write
	    uses: org/rep/.github/workflows/release-drafter.yml@main?vX
	    with:
	      is_collection: true

Il faut également avoir un fichier de config nommé release-drafter.yml dans un sous-répertoire nommé .github dans la racine du répertoire github, voici un exemple de configuration:

	name-template: 'v$RESOLVED_VERSION'
	tag-template: 'v$RESOLVED_VERSION'

	categories:
	  - title: 'Features'
	    collapse-after: 3
	    labels:
	      - 'feature'
	      - 'enhancement'
	  - title: 'Bug Fixes'
	    collapse-after: 3
	    labels:
	      - 'fix'
	      - 'bugfix'
	      - 'bug'
	  - title: 'Maintenance'
	    collapse-after: 3
	    label: 'documentation'

	change-template: '- $TITLE @$AUTHOR (#$NUMBER)'

	change-title-escapes: '\<*_&' # You can add # and @ to disable mentions, and add ` to disable code blocks.

	version-resolver:
	  major:
	    labels:
	      - 'major'
	  minor:
	    labels:
	      - 'minor'
	  patch:
	    labels:
	      - 'patch'
	  default: patch

	autolabeler:
	  - label: 'documentation'
	    files:
	      - '*.md'
	  - label: 'bug'
	    title:
	      - '/fix/i'
	    body:
	      - '/fix/i'
	  - label: 'enhancement'
	    title:
	      - '/feat/i'
	    body:
	      - '/feat/i'
	  - label: 'minor'
	    title:
	      - '/minor/i'
	  	body:
	      - '/minor/i'
	  - label: 'major'
	    title:
	      - '/major/i'
	    body:
	      - '/major/i'

	template: |
	  ## Changes

	  $CHANGES

## Paramètres
### Inputs
	Nom: is_collection
	Type: Booléen
	Requis: Non
	Valeur par défaut: false
	Description: Est-ce que le répertoire est une collection ansible qui contient un galaxy.yml?

### Outputs
	N/A