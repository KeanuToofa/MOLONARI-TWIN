# MOLONARI-TWIN

Jumeaux numériques des points de mesure et virtual labs de MOLONARI.

**Dépôt temporaire pour la démonstration du 2 novembre 2026.** L'admin de MOLONARI créera le dépôt définitif et en gardera le contrôle. Il est public, graine du MCMC comprise (`orx.yaml`).

## Contenu

```text
Point034/
├── twins/
│   ├── twin_direct/twin.yaml
│   └── twin_mcmc/{twin.yaml, orx.yaml}   # son twin.yaml porte la clé report
├── results/<twin_id>/                    # généré, non suivi
└── public_reports/                       # généré, non suivi
virtual_lab/lab_point034/lab.yaml         # le virtual lab de Point034
```

Le dépôt se monte dans un espace de travail avec `cgitsync bootstrap`, avec les données dans `data/`.

## Utilisation

Depuis la racine de l'espace de travail :

```bash
molonari-twin lab build MOLONARI-TWIN/virtual_lab/lab_point034 --point Point034
molonari-twin validate MOLONARI-TWIN/Point034/twins/twin_mcmc
molonari-twin run MOLONARI-TWIN/Point034/twins/twin_direct
molonari-twin run MOLONARI-TWIN/Point034/twins/twin_mcmc
molonari-twin report MOLONARI-TWIN/Point034/twins/twin_mcmc --output MOLONARI-TWIN/Point034/public_reports
```

Les paramètres de sol de `twin_direct` sont ceux de `twin_01`, non calibrés.
