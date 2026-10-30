# Point034

Twins du point de mesure Point034, avec les données de `data/SamplingPoints/Point034`.

- `twins/twin_direct` : modèle direct, paramètres de sol non calibrés.
- `twins/twin_mcmc` : inversion MCMC, comparée au modèle direct dans le rapport public.

Les twins lisent pour l'instant le brut (`data: {lab, point}`) ; ils passeront à `processed_data` avec la commande `lab build`.
