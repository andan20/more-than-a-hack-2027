# 022 — Broadcast D intervals expanded one second backwards / Расширение D на секунду назад

Controlled follow-up to 009: identical 92 tactical features and fixed boosting parameters; only automatic training D intervals change. / Контрольное продолжение 009: те же 92 признака и фиксированные параметры, меняется только слабая разметка D.

For every ORIGINAL accepted broadcast interval, extend its safe D region one second backwards, clipped to the original invalid-homography interval. This restores the initially discarded first second; it does not add a second before the non-field interval. Extend BEFORE excluding the public window, so exclusion cannot create an artificial expansion boundary. / Каждый ИСХОДНЫЙ безопасный D-интервал расширяем на секунду назад внутри соответствующего участка без гомографии. Это возвращает отброшенную первую секунду. Расширение выполняется ДО исключения публичного окна.

Use both halves outside public [11185,18685) plus 20-second guards. No public labels for sampling, fitting, hyperparameters, thresholds or feature selection. Any overlap with automatic LIVE is dropped from BOTH classes as ambiguous. Final ground truth is opened only after predictions are frozen. No 016 or other public-trained parents are used. / Оба тайма вне публичного окна и защитных отступов. Конфликт D/LIVE исключаем из обоих классов. Публичный эталон открываем только после фиксации прогнозов. Родителей, обученных на публичной разметке, нет.

Run All after preparing 008 features and broadcast alignment (see sol/010_dead_logistic/prepare_broadcast_labels.ipynb). Requires local restricted assets/caches; outputs go to ignored local_review/experiments/022_broadcast_expanded_weak. tqdm and progress.json report progress. / Run All после подготовки признаков 008 и синхронизации broadcast; результаты локальные, прогресс через tqdm и progress.json.

Fixed 150 trees, depth 3, 7 leaves, learning rate .05, leaf size 25, L2 2, seed 42. Threshold .5; bridge LIVE gaps <=10 frames, remove D runs <25 frames. Weak half1→half2 diagnostics do not select settings; final refit uses both halves. Sampling every 5 frames, at most 50 samples per episode, balanced episode/class weights. / Параметры фиксированы как в 009; слабая проверка по таймам не используется для подбора.

Tactical inputs use past windows up to 10 seconds; synchronization, weak labels and duration filtering are offline. Public five minutes have been repeatedly examined historically: this removes direct label use for this fit, not all research-level adaptation. Binary task only: spellF1 and H/A/D macroF1 are not applicable. / Исторически публичный фрагмент уже исследовался: новый запуск не превращает его в независимый тест. Только D/LIVE, без присвоения H/A.

No added library; publish only clean notebook, configuration and trusted fitted model, never cached inputs/predictions. / Новых библиотек нет; данные и прогнозы не публикуются.
