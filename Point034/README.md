# Point034

Twin du sampling point Point034, construit sur le virtual lab `lab_point034`, qui écrit `data/processed_data/Point034`.

- `twins/twin_direct` : modèle direct, paramètres de sol non calibrés.
- `twins/twin_mcmc` : inversion MCMC, comparée au modèle direct dans le rapport public.

Les deux modèles lisent `processed_data` (`data: {processed: …}`), sans second nettoyage. σ_T vaut 0,04 °C dans `twin_mcmc`, soit l'erreur totale observée (RMSE de 0,039 °C).
