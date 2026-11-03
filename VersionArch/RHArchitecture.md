# «StratifiedVotingArchitecture V. RH»

## Вступление

Управление сообществом и принятие коллективных решений часто сталкивается с рядом проблем, которые без должной системы будут сильно тормозить развитие сообщества или более того его убивать. Одними из таких проблем выходят: импульсивность, эмоциональность, просто мусорные, заведомо злокачественные голосования, которые в последствии тратят время участников. 

Данный документ описывает архитектуру системы голосований, изначально созданной для АСУ сообщества «Горизонт». В связи с тем, что данная версия архитектуры «StratifiedVotingArchitecture», а именно «StratifiedVotingArchitecture Version RevoltHorizon» создана под само сообщество и другие документы, для понимания глубины в так же можете прочесть: https://github.com/headwatch/RevoltHorizonRegulations/blob/main/Regulations.md 

## Создание голосования

Обозначим, что пользователь имеет право использовать для голосования любой текст от любого человека подходящий под стандарт ACI *(Adequacy Check Instructions)*,
позже я более подробно объясню что это, пока просто держите в уме, что ACI — некоторый стандарт и набор правил для проверки легитимности текста голосований и определения тира, про тиры также поговорим чуть позже.

Итак, процесс начинается с того, что пользователь формулирует текст голосования. В нем автор обязан исчерпывающе раскрыть тему, причину обсуждения, желаемую цель и предлагаемый вариант решения.

После пользователь выбирает категорию голосования, к примеру: `роли`, выбранная категория должна напрямую соответствовать обсуждаемой и разрешаемой теме вопроса.

Текст голосования: 

```
Я предлагаю создать новую роль «Объявления» (без административных прав) и добавить её в меню самостоятельного получения ролей.
В данный момент объявления сообщества отправляются с использованием общего тега,
что создает неудобства и отвлекает пользователей, не заинтересованных в их чтении.
Введение данной роли позволит отправлять целевые уведомления только заинтересованным участникам,
что снизит информационную нагрузку на остальных пользователей и повысит структурное удобство сервера.  
```
Для простоты дадим этому тексту следующий номер: `1234567890` 

Для запуска голосования в условном АСУ представим использование такой команды:
> Запустить голосование с текстом номер `1234567890`, категории `роли`

Например в рамках [Discord(а)](https://discord.com/) это может выглядеть так:

`/poll text_id:1234567890 category:role`

А в рамках АСУ на сайте иметь интерактивный интерфейс без необходимости указания какого-либо ID вовсе.

В данной архитектуре я поделил голосования на 4 тира (уровня), к каждому из них относиться некоторое кол-во категорий (к примеру та же категория `роли`. Категория лишь удобный ориентир пользователя, гораздо проще соотнести текст напрямую с буквенной категорией, а соотношение самой категории с тиром оставить за алгоритмом АСУ.

Текущие тиры «StratifiedVotingArchitecture V. RH»:

```
I. Low

Требуется процентов для победы: > 50%
Время на охлаждение: Nope
Кворум по активным пользователям: 15%
Время проведения: 24h

- **`[Косметика]`** — Добавление новых эмодзи, стикеров, смена баннера сервера, изменение цветов ролей.
    
- **`[Ивенты]`** — Предложения собраться поиграть, посмотреть фильм, провести временный конкурс на выходных (с созданием события в Discord).
    
- **`[Опросы]`** — Голосования без последствий для сервера (например: «Какая часть игры лучше?», «Что смотрим на выходных?»).

II. Mid

Требуется процентов для победы: > 55%
Время на охлаждение: 3h
Кворум по активным пользователям: 30%
Время проведения: 2d

- **`[Каналы]`** — Создание, удаление, переименование текстовых или голосовых каналов. Перемещение каналов по категориям.
    
- **`[Роли]`** — Создание новых и удаление *пользовательских* ролей.
    
- **`[Формат]`** — Введение постоянного расписания, утверждение постоянных активностей.

III. High

Требуется процентов для победы: > 60%
Время на охлаждение: 12h
Кворум по активным пользователям: 50%
Время проведения: 3d

- **`[Правосудие]`** — Голосования за бан, кик, пермач или длительный мут конкретного пользователя, а также амнистии (разбан) и публичные апелляции.

    
- **`[Локальные правила]`** — Добавление, изменение и удаление локальных подправил конкретной площадки, изменение тяжести наказаний за локальные нарушения.

    
- **`[Стафф]`** — Выборы новых модераторов, хелперов, админов площадки. Голосования за лишение управленца его прав (импичмент) и изменение локальных правил ротации/анкетирования.

    
- **`[Интеграции]`** — Добавление на площадку ботов и внешних интеграций, которым требуются широкие права (удаление сообщений, выдача ролей, баны).


- **`[Локальное лого]`** — Смена аватара (логотипа) конкретной отдельной площадки, не меняющая основную символику всего сообщества.


IV. Crit

Требуется процентов для победы: > 80%
Время на охлаждение: 24h
Кворум по активным пользователям: 75%
Время проведения: 7d

- **`[Название]`** — Смена официального названия сообщества.


- **`[Лого]`** — Смена основного (общего) логотипа сообщества.


- **`[Система голосования]`** — Изменение работы самой системы голосований (изменение процентов кворума, времени КД, логики АСУ, стандартов ACI).


- **`[Площадки]`** — Принудительное проведение или отмена любого действия от I до III тира на любой отдельной платформе (или нескольких платформах) методом глобального голосования, а также приостановка легитимности или полное отключение площадки.

    
- **`[Фундамент]`** — Изменение основного Регламента или Манифеста, смена основной тематики или идеологического вектора сообщества, передача корневых прав владения инфраструктурой, подключение новых опорных платформ.

```

— В данной таблице есть следующие параметры:

```
Требуется процентов для победы
Время на охлаждение
Кворум по активным пользователям
Время проведения
```

— Давайте я объясню, что это более подробно:

**Требуется процентов для победы** — это минимально допустимое отношение суммарного веса голосов "за" к весу голосов "против", необходимое для утверждения инициативы. Исход голосования определяется процентным соотношением веса положительных голосов к общей массе проголосовавших. Например, если суммарный вес "за" составил 52, а вес "против" — 142, общий пул весов равен 194. В данном сценарии инициатива набрала лишь 26.8% поддержки. Если для текущего типа опроса (тира) правилами установлен минимальный порог одобрения в 50% или 60%, система автоматически признает голосование несостоявшимся (не прошедшим порог).

**Время на охлаждение** — обязательная системная пауза, ограничивающая возможность мгновенного голосования. Данная мера внедрена для защиты от импульсивных решений и эффекта толпы. 
Без периода охлаждения сообщество уязвимо перед эмоциональными манипуляциями, когда участники выносят поспешные приговоры (устраивают "линчевание") под влиянием момента, 
не разобравшись в контексте.

**Кворум по активным пользователям** — необходимый минимум пользователей для того, чтобы голосование вошло в силу. Если мы имеем 100 активных пользователей, для, к примеру, IV тира нужно чтобы проголосовало 75% т.е. 75 человек. Кворум задаёт лишь минимум голосов для вступления в силу предложения, для достижения этого минимума учитываются как активные, так и неактивные пользователи.

Математика подсчёта пользователей:

```
Берётся статистика отправленых сообщений за 30 дней, отбрасываются все пользователи с 0 сообщений за 30 дней, на основе тех, кто остался строится масив, 
а его медиана определяет порог активности. Всё то кол-во участников которое выше порога считается активным кол-во пользователей
```

— Предполагаемые АСУ логируют дату, время и пользователя который отправил сообщение без сохранения контента. На основе этих данных за каждым пользователем в настоящее время закрепляется определённое кол-во сообщений, эти количества представляют из себя масив по которому и находится медиана, все сообщения отправленные 30 днями ранее удаляются.

**Время проведения** — время на протяжении которого длиться голосование, чем выше тир, тем выше важность, тем больше даётся времени подумать и задействовать участников.

Теперь мы определили в каком формате создаётся голосование, как у него определяется параметры по тирам и каким методом они рассчитываются. Поговорим про саму систему голосования: после создания голосования оно более не принадлежит одному человеку, оно является общественным, системным делом под авторством пользователя, при чём автор текста и пользователь инициации
может быть совершенно разным. В голосовании есть 5 вариантов:

```
Полностью согласен (+2)
Согласен (+1)
Воздержусь/Нейтрально (+0)
Не согласен (-1)
Полностью не согласен (-2)
```

— Значения в скобках: "(+-X)" — это вес голоса, он считается отдельно от кол-во самих голосов, к примеру для достижения кворума. В «StratifiedVotingArchitecture V. RH» используется шкала Лайкерта позволяющая при необходимости оценивать степень поляризации, а так же давать неуверенным участникам больший простор выбора.

---

### Защита от конформизма и сторона голосующих

До этого момента мы в большей степени разбирали процесс создания самого голосования, теперь настало время поговорить о пользователе голосующем *(как бы отсылка к человеку разумному)*. Все наши сложные надстройки выше и ниже, защищающие объективность самого голосования, никак не защищают адекватность голосующего. К сожалению, в нашем мире существует он — злополучный конформизм, приносящий в современных реалиях, бывает, больше горя, чем счастья. Человек, видящий, что большинство голосует за вариант в голосовании с тонной текста, скорее прочитает его слишком бегло или даже вовсе не прочитает, оставив галочку за тем самым большинством, формируя своим и другими подобными голосами неосмысленный каскад. Я думаю, не стоит объяснять, что задавать динамику голосам посредством большинства самих же голосов — не очень хорошо.

Анонимность голоса — важная вещь защищающая человека как от склонности проголосовать за большинство, так и от осуждения самого большинства. В данной архитектуре голосования я рекомендую скрывать то, за какой вариант человек проголосовал от большинства участников, не скрывая связь голоса и человека для системы. Увы, ситуация здесь до боли прозаична. Тот, кто контролирует среду выполнения, контролирует и данные. Ранее тут была описана система усложняющая получение доступа к базе голосов, но учитывая текущие реалии «Горизонт» и минусы той системы — это избыточно. 

Вы всегда можете использовать любой доступный метод для уложения связи между человеком и его голосом, хотя зачастую это нерационально. 

---

### Система проверки ACI

Вся выше описанная система определённо не так плоха, но в ней чего-то не хватает, как не пропускать чрезмерно эмоциональные, не логичные и просто токсичные голосования в маcсы? — Нужен максимально объективный способ проверки который был бы доступен каждому пользователю. 

В данной архитектуре им стал:

```
Adequacy Check Instructions (ACI) — это комплексная система стандартов для проверки легитимности предложений на голосование и определения их системного уровня (тира). Термин «инструкции» здесь означает не жесткий текстовый сценарий, а набор граничных значений, оценочных метрик вроде допустимого уровня спама, строгих системных ограничений и иных любых критериев.
```

То есть под ACI понимается набор данных который каким-либо способом может быть использован для проверки текста на структурную (логическую) адекватность.

«StratifiedVotingArchitecture V. RH» ACI:
```
ADEQUACY CHECK INSTRUCTIONS (ACI)

EVALUATION MANDATE AND OUTPUT REQUIREMENT:
The evaluation must culminate in exactly two strictly formatted outputs based on the structural and systemic impact analysis of the submitted text.
- Legitimacy [0 or 1]: Return 1 (TRUE/VALID) if and only if the text unconditionally satisfies ALL criteria outlined in Sections I and II. Return 0 (FALSE/INVALID) if the text violates even a single sub-clause of this protocol.

- Theme of the text [Tier 1, Tier 2, Tier 3, or Tier 4]: The structural intent and maximum technical impact of the text must be definitively classified into one of four systemic Tiers (defined in Section III).


SECTION I: ANTI-SPAM AND BASIC COHERENCE
1. Syntactic and Semantic Integrity: The text must consist of coherent language expressing a recognizable proposal, question, or appeal. Randomized character strings, word salads, flood, or empty messages without a clear subject immediately nullify the proposal (Legitimacy: 0).

2. Actionable Intent: Unless submitted as a casual poll under Tier 1 [Опросы], the text must clearly state what concrete change, action, or decision is being put to a vote, along with its basic reason and expected outcome.


SECTION II: SYSTEMIC PRESERVATION (REGULATION 0.2)
1. Anti-Sabotage Filter: The democratic mechanism shall not be utilized for the intentional destruction of the community. Any vote aimed at deleting the entire community, wiping core infrastructure without an operational transition plan (excluding legitimate cross-platform interventions or platform disconnection under Regulation 0.4.1), mass-banning users without cause, or disabling fundamental security protocols immediately returns Legitimacy: 0.


SECTION III: SYSTEMIC IMPACT AND TIER CLASSIFICATION
Core Classification Principle (Substance Over Form): The text must be classified based on its highest technical impact, permission level required, and reversibility — NOT by the casual wording used by the author. If a proposal combines multiple actions or disguises privileged permissions under a minor request, it MUST be assigned to the highest applicable Tier. When a proposal falls into a gray area between two Tiers, always escalate to the higher Tier.

- TIER 1 (Low — Cosmetic, Social, Non-Structural):

  * Systemic Scope: Zero impact on server structure, rules, permissions, or permanent layout. Easily reversible or purely temporary/informational.
  * [Косметика]: Adding new emojis or stickers, changing the server banner, or modifying existing role colors (strictly excludes changing any local platform logo or the overarching community logo/name).
  * [Ивенты]: Proposals to gather for games, watch movies, or hold temporary weekend contests (including creating temporary event rooms).
  * [Опросы]: Casual polls and discussions with no technical, administrative, or rule-changing consequences for the server.

- TIER 2 (Mid — Workspace Structure and Non-Privileged UX):

  * Systemic Scope: Alters the daily organization, channels, or non-privileged roles of the platform without granting any moderation/administrative permissions or changing behavioral rules. Fully reversible by standard staff.
  * [Каналы]: Creating, deleting, renaming, or moving text and voice channels or categories without restricting base user access rights.
  * [Роли]: Creating, modifying, or deleting standard user roles (notification tags, interest roles, cosmetic badges) that possess ZERO administrative, moderation, or channel-restriction permissions.
  * [Формат]: Establishing permanent schedules, recurring community activities, or standardizing channel templates.

- TIER 3 (High — Local Governance, Justice, Privileged Access, and Local Rules):

  * Systemic Scope: Affects individual user rights/punishments, grants or revokes delegated administrative/moderation privileges (within the bounds of a specific platform), or modifies local platform sub-rules. All actions here remain subordinate to the Core Regulation and can be enforced or reversed by the voting system.
  * [Правосудие]: Votes for banning, kicking, permanently banning, isolating, or issuing a long-term mute to a specific user, as well as amnesties (unbans) and public appeals from Restricted Users.
  * [Локальные правила]: Adding, removing, or modifying local platform sub-rules (under Regulation 0.4) or altering the severity of penalties for local violations (strictly excludes changing the Core Regulation or Manifesto).
  * [Стафф]: Electing or impeaching local moderators, helpers, and standard administrators whose powers are delegated and revocable within the system; modifying local recruitment questionnaires and staff rotation rules.
  * [Интеграции]: Adding, removing, or configuring bots and external webhooks that require privileged permissions (message management, role assignment, moderation).
  * [Локальное лого]: Changing the local avatar (logo) of a specific platform without altering the overarching main logo of the community.

- TIER 4 (Crit — Constitutional, Cross-Platform Sovereignty, and Core Architecture):

  * Systemic Scope: Affects the foundational identity of the community, alters the Core Regulation/Manifesto or voting mechanics, executes global cross-platform interventions, or touches Root-level platform sovereignty (actions that sit technically above standard administrators and local bots, making them irreversible by standard local mechanisms).
  * [Название]: Changing the official name of the community.
  * [Лого]: Changing the official overarching logo (main avatar/emblem) of the entire community.
  * [Система голосования]: Altering the mechanics, code, or parameters of the voting architecture (SVA), RedAdapter/ACS core logic, quorum formulas, cooldowns, or ACI standards.
  * [Площадки]: Executing or overriding any action from Tier 1 to Tier 3 on any specific platform (or multiple platforms) via a global community-wide vote, as well as questioning a platform's legitimacy, suspending its voting rights, or completely disconnecting/revoking its status as a community platform (under Regulation 0.4.1).
  * [Фундамент]: Modifying the Core Regulation (Регламент) or Manifesto; granting official status to a new voting platform; transferring root platform ownership (e.g., Discord Server Owner crown, root bot hosting/database control, domain ownership); migrating or shutting down the core community; shifting the core theme or ideological foundation of the community.

FINAL OUTPUT FORMAT:
Upon processing the text, ONLY the following data structure must be returned:
Legitimacy: [0 or 1]
Theme of the text: [Tier 1, Tier 2, Tier 3, or Tier 4]
```

— Именно по данном тексту проходит проверка легитимности голосования.

В целом, можно реализовать проверку NLP до выхода самого голосования в массы, но в данной версии архитектуры я выбрал именно ручную проверку, а реализовывать её для каждого голосования даже без жалоб, скажем — не рационально. Любой управленец видя репорт на голосовании может проверить его хоть через тот же ИИ, опять же, право проверки сохраняется за каждым участником,
просто именно модератор имеет право отклонить или одобрить голосование по ACI.

Если голосование не проходит ACI т.е. вывод `Legitimacy 0` и/или `Theme of the text: X` не совпадает с действующим тиром (т.е. уровнем категории) оно отменяется.
Если голосование проходит, т.е. вывод `Legitimacy 1` и `Theme of the text: X` совпадает с действующим тиром оно получает защиту от последующих жалоб. Если же голосование было принято или отклонено по ошибке, никому из пользователей не составит труда это заметить путём самоличной проверки

Пример на основе текста:
```
Я предлагаю создать новую роль «Объявления» (без административных прав) и добавить её в меню самостоятельного получения ролей.
В данный момент объявления сообщества отправляются с использованием общего тега,
что создает неудобства и отвлекает пользователей, не заинтересованных в их чтении.
Введение данной роли позволит отправлять целевые уведомления только заинтересованным участникам,
что снизит информационную нагрузку на остальных пользователей и повысит структурное удобство сервера.
```
<img width="814" height="650" alt="изображение" src="https://github.com/user-attachments/assets/df731cdb-6711-47f7-bd11-19832b7f0b9b" />

Конечно, подобный вариант ACI и проверка с помощью популярных ИИ-моделей не лучший вариант, но это лишь пример, на деле, как я уже говорил, ACI может быть чем угодно.

---

## Заключение

В заключение важно подчеркнуть главное: описанная архитектура — это лишь ядро голосования. Каким бы продуманным ни было это ядро, без плотной «внешней обёртки» из социальных правил, регламентов и сформированной культуры сообщества оно неизбежно скатится в хаос.

Вы вряд ли сможете стабильно интегрировать эту модель в стандартное сообщество с правилом активности 1-9-90 (1% создателей, 9% активных участников и 90% наблюдателей) без предварительной подготовки  аудитории. Голая неадаптированная архитектура неспособна решить в одиночку все социальные проблемы. В рамках этого текста я не упоминал защиту от обычной накрутки ботов или конфликта решений, когда голосование B, прямо противоречащее голосованию A, выигрывает одновременно с ним. Настоящую легитимность и стабильность данной архитектуре придает только общественный договор.
