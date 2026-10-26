# 025 — MLP on expanded weak labels + frozen H/A

Те же 10597 обучающих примеров и веса серий, что в 022: broadcast D расширен на секунду назад, публичные пять минут и по 20 секунд исключены. 92 исходных координатных признака; заполнение пропусков и индикаторы обучаются только на train. MLP/logistic дополнительно стандартизируются. / EXACT 022 training examples and weights; public window plus guards excluded; preprocessing fitted on training only.

Архитектуры: `[{"name": "mlp16", "kind": "mlp", "hidden": [16], "dropout": 0.0, "epochs": 80, "weight_decay": 0.001}, {"name": "mlp32_16", "kind": "mlp", "hidden": [32, 16], "dropout": 0.1, "epochs": 80, "weight_decay": 0.001}, {"name": "mlp64_32", "kind": "mlp", "hidden": [64, 32], "dropout": 0.1, "epochs": 80, "weight_decay": 0.001}]`. Пороги: 0.5, 0.6, 0.7, 0.8, 0.9, 0.95, 0.99, 0.995. MLP: ReLU, AdamW lr=.001, batch256, 80 фиксированных эпох, weighted BCE, seed42. LR: lbfgs, max_iter5000. RF: 300 trees, max_features=sqrt. / Fixed models and thresholds, no public early stopping or training selection.

H/A заморожен из 023/020: очищенный трекинг, уверенные/спорные эпизоды, коридор только за штрафной. Порог применяется к D, затем тот же фильтр длительности и полный офлайн H/A. X=0. / Frozen H/A, full offline inference; predictions frozen before public-label access.

Ограничение: H/A исторически выбран по публичным меткам; сравнение всех порогов и выбор лучшего по публичным метрикам — подбор, а не независимая проверка. Качество полного матча неизвестно. / Public-ranked diagnostics, not an independent generalization estimate.

Run All после 022 (weak_training_selection.npz и маски), подготовки признаков 008 и исходных ATD. Используется код H/A из sol/023_weak022_anchors020/experiment.ipynb. tqdm и local_review/experiments/025_weak_mlp_ha/progress.json показывают прогресс. Отчёты, прогнозы, исполненные ноутбуки локальные. В Git — чистый ноутбук, конфигурации и доверенные обученные model.pkl. Не открывайте чужие pickle.
