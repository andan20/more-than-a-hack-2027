# 030 — Random forest on expanded weak labels + frozen H/A

Полная слабая разметка broadcast обоих таймов, включая первые пять минут и ранее исключавшиеся отступы. D расширен на секунду назад как в 022. Истинные итоговые H/A/D не используются для обучения или отбора; неизвестные/конфликтные автоматические метки исключены. Выборка каждые 5 кадров, до 50 на серию, равные веса серий и классов как раньше. 92 исходных координатных признака; заполнение пропусков и индикаторы обучаются только на train. MLP/logistic дополнительно стандартизируются. / ALL automatic weak-label frames, including the public prefix; no reference-label training; preprocessing fitted on training only.

Архитектуры: `[{"name": "forest_d6_l20", "kind": "forest", "depth": 6, "leaf": 20, "trees": 300}, {"name": "forest_d12_l10", "kind": "forest", "depth": 12, "leaf": 10, "trees": 300}, {"name": "forest_full_l5", "kind": "forest", "depth": null, "leaf": 5, "trees": 300}]`. Пороги: 0.5, 0.6, 0.7, 0.8, 0.9, 0.95, 0.99, 0.995. MLP: ReLU, AdamW lr=.001, batch256, 80 фиксированных эпох, weighted BCE, seed42. LR: lbfgs, max_iter5000. RF: 300 trees, max_features=sqrt. / Fixed models and thresholds, no public early stopping or training selection.

H/A заморожен из 023/020: очищенный трекинг, уверенные/спорные эпизоды, коридор только за штрафной. Порог применяется к D, затем тот же фильтр длительности и полный офлайн H/A. X=0. / Frozen H/A, full offline inference; predictions frozen before public-label access.

Ограничение: H/A исторически выбран по публичным меткам; сравнение всех порогов и выбор лучшего по публичным метрикам — подбор, а не независимая проверка. Качество полного матча неизвестно. / Public-ranked diagnostics, not an independent generalization estimate.

Run All после 022 (expanded_D_candidates.npy) и broadcast_alignment (weak_LIVE_candidates.npy), подготовки признаков 008 и исходных ATD. Используется код H/A из sol/023_weak022_anchors020/experiment.ipynb. tqdm и local_review/experiments/030_allweak_forest_ha/progress.json показывают прогресс. Отчёты, прогнозы, исполненные ноутбуки локальные. В Git — чистый ноутбук, конфигурации и доверенные обученные model.pkl. Не открывайте чужие pickle.

Изменение относительно 027: только состав обучающей выборки. Те же архитектуры, 80 эпох MLP, seed42 и восемь порогов. Это обучение на слабых метках также для оцениваемых входных кадров (transductive setting), а не тест на невиденных кадрах. / Only training-frame selection changes; exact same fixed models and thresholds. Public-input overlap is intentional, not reference-label supervision.
