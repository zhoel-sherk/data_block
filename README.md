# data_block

Провайдер-специфичные данные blockcheckS: проверенные DNS (anti-hijack),
only-pass стратегии, лучшие конфиги и hosts для Windows.

## Структура

```
providers/<provider>/
    ├── dns.db            # SQLite: правильные IP + tampered-записи
    ├── strategies.db     # SQLite: only-pass стратегии (approved)
    ├── best_config.conf  # лучший конфиг nfqws2 для провайдера
    ├── triage.toml       # ISP-prior из Preflight (hops, foolings, ECH/HTTP/voice)
    ├── hosts             # anti-hijack hosts для Windows
    └── <provider>.md     # описание проблем с провайдером
```

Провайдер определяется автоматически по `org` из ipinfo.io
(например `AS51369 LLC TRC FIORD` → `llc_trc_fiord`; `normalize_provider_name`
slug-ифицирует все слова через `_`). Персист в `config.toml [provider] name`;
переопределить можно через env `BLOCKCHECKS_PROVIDER` или `--data-block-sync`.
`data_block/` является git-субмодулем (см. `.git` + `store.py:3`).

`triage.toml` — ISP-prior из Preflight (hops, viable foolings/blobs, ECH/HTTP/voice,
`[dead]`). Пишет `ProviderStore.save_triage`; git-коммит только с `--data-block-sync`.
При `--quick` / `--no-preflight` файл поднимается как prior для prune/AQ.
