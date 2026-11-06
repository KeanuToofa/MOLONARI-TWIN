# Point034

Twin du sampling point Point034, construit sur le virtual lab `lab_point034`, qui écrit `data/processed_data/Point034`.

- `orx/twin_mcmc.yaml` : graine de référence du MCMC, lue par l'OPX seul.
- `twins/twin_direct` : modèle direct, paramètres de sol non calibrés. Son `generation.yaml` donne les couches et les bornes de `generate`.
- `twins/twin_mcmc` : inversion MCMC, comparée au modèle direct dans le rapport public.
- `public_reports/` : le rapport public et `chains.npz` (sous-échantillon des chaînes, sans graine ni champs T et q), à lire directement.

Les deux modèles lisent `processed_data` (`data: {processed: …}`), sans second nettoyage. σ_T vaut 0,04 °C dans `twin_mcmc`, soit l'erreur totale observée (RMSE de 0,039 °C).
