# data_block

Провайдер-специфичные данные blockcheckS: проверенные DNS (anti-hijack),
only-pass стратегии, лучшие конфиги и hosts для Windows.

## Структура

```
providers/<provider>/
├── dns.db            # SQLite: правильные IP + tampered-записи
├── strategies.db     # SQLite: only-pass стратегии (approved)
├── best_config.conf  # лучший конфиг nfqws2 для провайдера
├── hosts             # anti-hijack hosts для Windows
└── <provider>.md     # описание проблем с провайдером
```

Провайдер определяется автоматически по `org` из ipinfo.io
(например `AS51369 LLC TRC FIORD` → `llc_fiord`).
