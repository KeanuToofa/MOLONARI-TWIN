# MOLONARI-TWIN

Jumeaux numériques des points de mesure et virtual labs de MOLONARI.

**Dépôt temporaire pour la démonstration du 2 novembre 2026.** L'admin de MOLONARI créera le dépôt définitif et en gardera le contrôle. Il est public, graine du MCMC comprise (`Point034/orx/twin_mcmc.yaml`).

## Disposition

La disposition suit celle des sous-dépôts prévus (spec MOLONARI à 4 niveaux, section 1) : chaque dossier ci-dessous deviendra un dépôt, avec son niveau de lecture. Ici ils sont réunis dans un seul dépôt, et le chemin de chacun est le même une fois séparés, donc le code n'a pas à s'adapter.

```text
Point034/                              opx    parent : graine, README
├── orx/twin_mcmc.yaml                        graine de référence du MCMC (OPX seul)
├── public_reports/                    public rapport publié et chains.npz (suivi)
└── twins/
    ├── twin_direct/                   user   twin.yaml, generation.yaml ; results/ non suivi
    └── twin_mcmc/                     dev    twin.yaml (porte la clé report) ; results/ non suivi
virtual_lab/lab_point034/              opx    parent
└── description/                       dev    lab.yaml, README
```

`results/` et `registry.csv` de chaque twin sont générés par `molonari-twin run` et restent hors du dépôt. `public_reports/` et `generation.yaml` sont suivis : ce sont les fichiers que lit le public, écrits à l'issue de `molonari-twin report`.

Le dépôt se monte dans un espace de travail avec `cgitsync bootstrap`, avec les données dans `data/`.

## Utilisation

Depuis la racine de l'espace de travail, à l'OPX (qui a la graine) :

```bash
molonari-twin lab build MOLONARI-TWIN/virtual_lab/lab_point034/description --point Point034
molonari-twin validate MOLONARI-TWIN/Point034/twins/twin_mcmc
molonari-twin run MOLONARI-TWIN/Point034/twins/twin_direct
molonari-twin run MOLONARI-TWIN/Point034/twins/twin_mcmc
molonari-twin report MOLONARI-TWIN/Point034/twins/twin_mcmc --output MOLONARI-TWIN/Point034/public_reports
```

`report` écrit aussi `Point034/twins/twin_direct/generation.yaml` (couches et bornes des paramètres, pour `generate`).

À un niveau moindre :

```bash
molonari-twin reports show MOLONARI-TWIN/Point034                # user : lire le rapport publié
molonari-twin generate MOLONARI-TWIN/Point034 --output mon_etat  # user : générer un état par le modèle direct
molonari-twin ask mon_etat water_flux --level user
molonari-twin run MOLONARI-TWIN/Point034/twins/twin_mcmc --sigma-temperature 0.08 --space mon_space --seed 7   # dev
molonari-twin report mon_space/twin_mcmc_sigmaT0.08 --forward MOLONARI-TWIN/Point034/twins/twin_direct --output mon_rapport   # dev : rapport local
```

Un dev lance son propre twin avec sa graine, dans son espace de travail : il ne reçoit jamais la graine de référence, et son rapport local n'est jamais écrit dans `public_reports/`.

Les paramètres de sol de `twin_direct` sont ceux de `twin_01`, non calibrés.
