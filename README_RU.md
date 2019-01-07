🇬🇧 [English version](README.md)  |   🇵🇱 [Polska wersja](README_PL.md)  

# Atomic Threat Coverage

Автоматически генерируемая база аналитических данных, предназначенная для противодействия угрозам, описанным в MITRE ATT&CK.

![](images/logo_v1.png)
<!-- ![](images/atc_description_v01.png) -->

Atomic Threat Coverage это утилита которая позволяет автоматически сгенерировать базу аналитических данных, предназначенную для противодействия угрозам, описанным в [MITRE ATT&CK](https://attack.mitre.org/) с позиций Обнаружения, Реагирования, Предотвращения и Имитации угроз:

- **Detection Rules** — правила обнаружения основанные на [Sigma](https://github.com/Neo23x0/sigma) — общем формате описания правил корреляции для SIEM систем
- **Data Needed** — данные, которые необходимо собирать для обнаружения конкретной угрозы
- **Logging Policies** — настройки логирования, которые необходимо произвести на устройстве для сбора данных, необходимых для обнаружения конкретной угрозы
- **Triggers** — сценарии имитации атак основанные на [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team) — атомарных тестах/сценариях реализации угроз из MITRE ATT&CK
- **Response Playbooks** — сценарии реагирования на инциденты, сгенерированные в ходе обнаружения конкретной угрозы
- **Hardening Policies** — настройки систем, которые позволяют нивелировать конкретную угрозу
- **Mitigation Systems**  — системы и технологии, которые позволяют нивелировать конкретную угрозу

Atomic Threat Coverage является автоматизированным фреймворком для сохранения, разработки, анализа и распространения практической, действенной аналитики.

## Описание

### Предпосылки

Существует много достойных проектов, которые реализуют функциональность (или предоставляют аналитику) конкретной направленности ([Sigma](https://github.com/Neo23x0/sigma), [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team), [MITRE CAR](https://car.mitre.org)). Их объединяет один недостаток — они существуют в вакууме свой области. В реальности же все очень тесно взаимосвязанно — данные для обнаружения угроз не берутся из ниоткуда, и генерируемые Алерты не уходят в никуда. Каждая функция, будь то сбор данных, администрирование систем защиты, обнаружение угроз или реагирование на них — это составная часть большого и сложного процесса, завязанного на несколько подразделений, требующая их плотного взаимодействия. 

Проблемы одной функции зачастую проще, дешевле и эффективнее решать методами другой. Многие задачи не решаются в рамках одной функции в принципе. Каждая из функций базируется на возможностях и качеству другой. Не получится эффективно детектировать угрозы и реагировать на инциденты без сбора и обогащения необходимых данных. Не получится эффективно реагировать на инциденты без понимания того, какими средствами/системами/технологиями можоно блокировать угрозу. Крайне неэффективно проводить тестирование на проникновениве или Red Team exercises без представления о возможностях процессов, персонала и систем по блокированию, обнаружению и реагированию на инциденты. Все это требует тесного взаимодействия и взаимопонимания между подразделениями.

На практике наблюдается сложность во взаимодействии, обусловленная следующими факторами:

- Отсутствие общей модели/классификации угроз, общей терминологии
- Отсутствие понимания общих целей
- Отсутствие простого метода выражения своих потребностей
- Разница в компетенциях (как в плане глубины, так и в плане различия предметных областей)

Именно поэтому мы решили разработать Atomic Threat Coverage — проект, который призван связать разные функции под единой "Threat Centric" методологией ([Lockheed Martin Intelligence Driven Defense®](https://www.lockheedmartin.com/en-us/capabilities/cyber/intelligence-driven-defense.html) aka [MITRE Threat-based Security](https://mitre.github.io/unfetter/about/)), моделью угроз ([MITRE ATT&CK](https://attack.mitre.org/)) и предоставить подразделениям информационной безопасности эффективный инструмент для совместной работы над одной задачей — противодействию угрозам.

### Почему Atomic Threat Coverage

Работа с существующими <sup>[\[1\]](https://car.mitre.org)[\[2\]](https://eqllib.readthedocs.io/en/latest/)[\[3\]](https://github.com/palantir/alerting-detection-strategy-framework)[\[4\]](https://github.com/ThreatHuntingProject/ThreatHunting)</sup> репозиторями аналитики выглядит как бесконечное клацание CTRL+C/CTRL+V, ручная адаптация информации под собственные нужды, модель данных, сопоставление с внутренними метриками и так далее. 

Мы решили пойти иным путем. 

Atomic Threat Coverage это фреймворк для создания **вашей собственной** базы знаний, импорта аналитики из других проектов (таких как [Sigma](https://github.com/Neo23x0/sigma), [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team), а также **ваших** приватных форков этих проектов с **вашей** аналитикой) и экспорта этой аналитики в удобные для восприятия человеком статьи в две (на текущий момент) платформы:

1. [Atlassian Confluence](https://www.atlassian.com/software/confluence) ([здесь](https://atomicthreatcoverage.atlassian.net/wiki/spaces/DEMO/pages/10944874/win+susp+powershell+hidden+b64+cmd) можно посмотреть автоматически сгенерированную базу знаний)
2. [В текущий репозиторий](Atomic_Threat_Coverage) — автоматически сгенерированные статьи в вики-формате на языке Markdown

Другими словами, вам не нужно работать с уровнем представления данных вручную, вы работаете только с осмысленными атомарными кусочками информации (такими как Sigma правила), и Atomic Threat Coverage автоматически создаст базу аналитики со всеми сущностями, связанными со всеми важными, действенными метриками, готовую к использованию, распространению, презентации руководству, заказчикам и коллегам.

### Как это работает

Все начинается с Sigma правила и заканчивается удобными для восприятия человеком статьями. Atomic Threat Coverage парсит Sigma правило, после чего:

1. Привязывает Detection Rule к тактике ATT&CK, используя  `tags` Sigma правила
2. Привязывает Detection Rule к технике ATT&CK, используя `tags` Sigma правила
3. Привязывает Detection Rule к Data Needed, используя `logsource` и `detection` Sigma правила
4. Привязывает Detection Rule к Trigger, (Atomic Red Team тест), используя  `tags` Sigma правила
5. Привязывает Logging Policies к Data Needed используя существующую в Data Needed ссылку
6. Конвертирует все в Confluence и Markdown вики-подобные статьи используя шаблоны jinja (`scripts/templates`)
7. Создает статьи в локальном репозитории и в Confluence (согласно конфигурации в `scripts/config.py`)
8. Создает `analytics.csv` файл для простой аналитики имеющихся данных

### Под капотом

Типы аналитических данных в репозитории:

```
├── analytics.csv
├── dataneeded
│   ├── DN_0001_windows_process_creation_4688.yml
│   ├── DN_0002_windows_process_creation_with_commandline_4688.yml
│   ├── DN_0003_windows_sysmon_process_creation_1.yml
│   ├── DN_0004_windows_account_logon_4624.yml
│   └── dataneeded_template.yml
├── detectionrules
│   └── sigma
├── enrichments
│   ├── EN_0001_cache_sysmon_event_id_1_info.yml
│   ├── EN_0002_enrich_sysmon_event_id_1_with_parent_info.yaml
│   └── EN_0003_enrich_other_sysmon_events_with_event_id_1_data.yml
├── loggingpolicies
│   ├── LP_0001_windows_audit_process_creation.yml
│   ├── LP_0002_windows_audit_process_creation_with_commandline.yml
│   ├── LP_0003_windows_sysmon_process_creation.yml
│   ├── LP_0004_windows_audit_logon.yml
│   └── loggingpolicy_template.yml
└── triggering
    └── atomic-red-team
```

#### Detection Rules

Detection Rules — Правила Обнаружения — оригинальные, не модифицированные [Sigma правила](https://github.com/Neo23x0/sigma/tree/master/rules). По умолчанию Atomic Threat Coverage использует правила из официального репозитория, но вы можете (*вам следует*) использовать ваши собственные Sigma правила из приватного форка, с внутренней аналитикой, релевантной для вас.

<details>
  <summary>Detection Rule yaml (to expand)</summary>
  <img src="images/sigma_rule.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Confluence (кликните чтобы раскрыть)</summary>
  <img src="images/dr_confluence_v1.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Markdown (кликните чтобы раскрыть)</summary>
  <img src="images/dr_markdown_v1.png" />
</details>

<br>
Ссылка на Data Needed, Trigger, и статьи в ATT&CK сгенерированы автоматически.  
Sigma правило, запросы для Kibana, X-Pack Watcher и запрос GrayLog сгенерированны и добавлены автоматически (этот список может быть расширен и зависит от поддерживаемых Sigma [платформах для экспорта правил](https://github.com/Neo23x0/sigma#supported-targets)).

#### Data Needed

<details>
  <summary>Data Needed yaml (кликните чтобы раскрыть)</summary>
  <img src="images/dataneeded_v1.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Confluence (кликните чтобы раскрыть)</summary>
  <img src="images/dn_confluence_v1.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Markdown (кликните чтобы раскрыть)</summary>
  <img src="images/dn_markdown_v1.png" />
</details>

<br>
Эта сущность в первую очередь призвана упростить коммуникацию с SIEM/LM/Data Engineering подразделениями.
Она влючает в себя следующие данные:

- Детальное описание данных (Platform/Type/Channel/etc) необходимо для вычисления связи с Правилами Обнаружения (Detection Rules)
- Sample — пример лога, описание того как выглядят оригинальные данные, которые необходимо собирать для Обнаружения конкретных угроз и Реагирования на инциденты
- Лист доступных полей необходим для вычисления связи с Правилами Обнаружения (Detection Rules), для генерации сценариев реагирования на инциденты (Response Playbooks), а также для генерации `analytics.csv`

#### Logging Policies

<details>
  <summary>Logging Policy yaml (кликните чтобы раскрыть)</summary>
  <img src="images/loggingpolicy.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Confluence (кликните чтобы раскрыть)</summary>
  <img src="images/lp_confluence_v1.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Markdown (кликните чтобы раскрыть)</summary>
  <img src="images/lp_markdown_v1.png" />
</details>

<br>
Эта сущность в первую очередь призвана упростить коммуникацию с SIEM/LM/Data Engineering подразделениями.
Она влючает в себя описание конфигурации, которую необходимо реализовать на источнике данных, чтобы собирать данные (Data Needed), необходимые для Обнаружения конкретных угроз и Реагирования на инциденты.

#### Triggers

сценарии имитации атак основанные на [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team) — атомарных тестах/сценариях реализации угроз из MITRE ATT&CK

Triggers — сценарии имитации атак — оригинальные, не модифицированные [Atomic Red Team тесты](https://github.com/redcanaryco/atomic-red-team/tree/master/atomics). По умолчанию Atomic Threat Coverage использует тесты из официального репозитория, но вы можете (*вам следует*) использовать ваши собственные Atomic Red Team тесты из приватного форка, с внутренней аналитикой, релевантной для вас.

<details>
  <summary>Trigger yaml (кликните чтобы раскрыть)</summary>
  <img src="images/trigger.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Confluence (кликните чтобы раскрыть)</summary>
  <img src="images/trigger_confluence_v1.png" />
</details>

<details>
  <summary>Автоматически сгенерированная страница в Markdown (кликните чтобы раскрыть)</summary>
  <img src="images/tg_markdown_v1.png" />
</details>

<br>
Эта сущность позволяет тестировать возможности по обнаружению конкретных угроз, а также систем/механизмов/технологий обеспечения безопасности. Полное описание можно посмотреть на официальном [сайте](https://atomicredteam.io).

#### analytics.csv

Atomic Threat Coverage генерирует [analytics.csv](analytics.csv) — список данных со всеми зависимостями для простой анатилики посредством фильтров. Этот файл позволяет ответить на следующие вопросы:

- Какой источник данных может предоставить мне данные конкретного типа? (например, в ходе Реагирования на инцидент (Identification), необходимо выяснить какие источники данных могут предоставить domain name/username/hash/etc)
- Какие данные нужно собирать чтобы детектировать конкретную угрозу?
- Какие настройки логирования необходимо произвести чтобы собирать данные, необходимые для обнаружения конкретной угрозы?
- Какие настройки логирования можно произвести на всех хостах (объем данных (event volume) low/medium), а какие исключительно на критичных хостах (объем данных high/extremely high)
- Какие источники данных предоставляют возможность производить бОльшую часть Алертов с высоким уровнем критичности? (позволяет приоритизировать подключение источников)
- И так далее

В идеале, этот файл может предоставить организациям возможность выразить возможности обнаружения конкретного набора угроз **в денежном эквиваленте**. Например:

- Если мы собираем все Data Needed со всех хостов для реализации всех Detection Rules которые у нас на текущий момент есть, это будет X событий в секунду (Events Per Second, EPS) с Y ресурсов (HDD/SSD, RAM, CPU) для хранения и обработки данных (для рассчета количества данных необходимо провести ~2 недельный тест). Необходимые мощности легко выражаются в деньгах, с более-менее конкретной цифрой
- Если мы собираем Data Needed только с критичных хостов для реализации Detection Rules исключительно с высоким уровнем критичности, это будет X событий в секунду (Events Per Second, EPS) с Y ресурсов (HDD/SSD, RAM, CPU) для хранения и обработки данных (для рассчета количества данных необходимо провести ~2 недельный тест). Необходимые мощности легко выражаются в деньгах, с более-менее конкретной цифрой
- И так далее

## Цели проекта

1. Стимулировать сообщество использовать Sigma правила (больше разработчиков, больше конверторов хорошего качества)
2. Стимулировать сообщество использовать Atomic Red Team тесты (больше разработчиков, больше фреймворков исполнения хорошего качества)
3. Евангелизация распространения Cyber Threat Intelligence
4. Автоматизация ручной работы
5. Предостиавление сообщуству фреймворка для улучшения коммуникации с смежными департаментами, сохранения, разработки, анализа и распространения практической, действенной аналитики

## Алгоритм использования

1. Скопируйте ваши [Sigma](https://github.com/Neo23x0/sigma) правила (если у вас таковые есть) в директорию `detectionrules`
2. Скопируйте ваши [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team) тесты (если у вас таковые есть) в директорию `triggering`
3. Создайте Data Needed в соответствии с вашими Sigma правилами в директории `dataneeded`, используя шаблон `dataneeded/dataneeded_template.yml`
4. Создайте Logging Policies в соответствии с вашими Data Needed в директории `loggingpolicies`, используя шаблон `loggingpolicies/loggingpolicy_template.yml`
5. Настройте экспорт в Confluence используя файл `scripts/config.py`
6. Исполните команду `make` в корне репозитория

## Текущая стадия разработки: Proof Of Concept

Этот проект на текущий момент находится в стадии Proof Of Concept. Он был разработан за несколько вечеров. Он не работает со всеми Sigma правилами. Мы перепишем кодовую базу, разработаем все необходимые для Sigma правил из официального репозитория Data Needed и Logging Policies, а также добавим новые сущности (Playbooks, Enrichments). На текущий момент мы хотим показать рабочий прототип для обсуждения с сообществом, получения обратной связи, комментариев и предложений по улучшению.

## Системные требования

- Unix-подобная ОС или [Windows Subsystem for Linux (WSL)](https://en.wikipedia.org/wiki/Windows_Subsystem_for_Linux) (для исполнения `make`)
- Python 3.7.1
- Библиотека [jinja2](https://pypi.org/project/Jinja2/)
- Приложение для Confluence [Render Markdown](https://marketplace.atlassian.com/apps/1212654/render-markdown) (free open source)

## Авторы

- Daniil Yugoslavskiy, [@yugoslavskiy](https://github.com/yugoslavskiy)
- Jakob Weinzettl, [@mrblacyk](https://github.com/mrblacyk)
- Mateusz Wydra, [@sn0w0tter](https://github.com/sn0w0tter)
- Mikhail Aksenov, [@AverageS](https://github.com/AverageS)

## TODO

- [ ] Исправить генерацию `analytics.csv`
- [ ] Разработать Польскую и Русскую версии README
- [ ] Переписать `make` и все bash скрипты на python для совместимости с Windows
- [ ] Переписать основную кодовую базу
- [ ] Добавить contribution guide
- [ ] Создать developer guide (как добавлять кастомные поля и сущности)
- [ ] Реализовать консистентную модель данных (наименование полей)
- [ ] Добавить оставшиеся Data Needed для правил Sigma из официального репозитория
- [ ] Добавить оставшиеся Logging Policies для всех Data Needed 
- [ ] Реализовать новую схему наименования Detection Rule (разделить Events и Alerts)
- [ ] Разработать docker контейнер для утилиты
- [ ] Разработать генератор [MITRE ATT&CK Navigator](https://mitre.github.io/attack-navigator/enterprise/) профилей для каждой сущности
- [ ] Создать сущность "Enrichments", которая будет описывать процесс обогащения Data Needed
- [ ] Создать сущность "Visualisation" с визуализациями/дашбордами Kibana, сохраненными в yaml файлах и возможностью их конвертации в curl команды для загрузки в Elasticsearch
- [ ] Создать сущность "Playbook" (вычисление на базе Detection Rule и Data Needed) с автоматическим созданием TheHive Case Templates (actionable Playbook)

## Ссылки

[\[1\]](https://car.mitre.org) MITRE Cyber Analytics Repository  
[\[2\]](https://eqllib.readthedocs.io/en/latest/) Endgame EQL Analytics Library  
[\[3\]](https://github.com/palantir/alerting-detection-strategy-framework) Palantir Alerting and Detection Strategy Framework  
[\[4\]](https://github.com/ThreatHuntingProject/ThreatHunting) The ThreatHunting Project  

## Лицензия

Смотри файл [LICENSE](LICENSE).
