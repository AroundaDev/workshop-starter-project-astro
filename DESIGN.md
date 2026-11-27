# DESIGN.md: Nora, «Ink & Coral»

Єдине джерело правил верстки для сторінок проєкту. Джерело стилю: `design/nora-landing-motion.html`.

- Значення токенів: [`tokens.json`](tokens.json) і [`src/styles/tokens.css`](src/styles/tokens.css). Вони мають збігатися: змінюєш одне, зміни й друге.
- Компоненти: `src/components/ui/`. Усі разом зі станами: сторінка `/components`.

## 1. Характер

Спокійний, «паперовий» інтерфейс: теплий світлий фон, графітовий текст, тонкі серифні заголовки, багато повітря. Корал використовується дуже скупо. Тіні майже немає: її має лише основна кнопка.

## 2. Кольори

| Роль | Токени |
| --- | --- |
| Фон сторінки / плитка / картка інтерфейсу | `--color-bg-page`, `--color-bg-surface`, `--color-bg-raised` |
| Текст основний / другорядний | `--color-text-primary`, `--color-text-secondary` |
| Лінії | `--color-border-default`, `--color-border-strong` |
| Графіт (кнопки, дані) і білий | `--color-ink`, `--color-white` |
| Акцент | `--color-coral`, `--color-peach`, `--color-blush`, `--color-marker` |
| Скло поверх фото | `--color-bg-glass`, `--color-bg-glass-soft`, `--color-bg-glass-panel`, `--color-bg-header` |
| Темні блоки | клас `.is-dark` |

**Корал лише для:** «квітки», виділеного тарифу, фінального блоку, маркера й «живої» крапки. Не для кнопок і не для тексту. Синього в палітрі немає.

## 3. Типографіка

| Стиль | Як застосувати | Шрифт |
| --- | --- | --- |
| H1, H2 | `<h1>`, `<h2>` | Newsreader 300 |
| H3 | `<h3>` | Inter 500 |
| Маніфест / цитата / велика цифра | `.text-manifesto`, `.text-quote`, `.text-metric` | Newsreader 300 |
| Вступ | `.text-lead` | Inter 400 |
| Основний / дрібний | `<p>`, `.text-small` | Inter 400 |
| Мітка | `.text-label` (великі літери) | Geist Mono 500 |
| Ключове слово | `<em class="key">` | курсив, одне-два слова на заголовок |
| Маркер | `.text-marker` | коралова смуга під словами |

Розміри заголовків гнучкі (`--font-size-h1` тощо), окремих значень для екранів не треба.

## 4. Відступи, форма, сітка

- Відступи тільки з шкали `--space-*`. Між секціями: клас `.section` (`--space-section`).
- Картки й плитки: `--radius-8`. Кнопки та пігулки: `--radius-999`.
- Щілина між плитками: `--tile-gap`.
- Контейнер: `.container` (макс. 1280px). 12 колонок: `.grid-12`.
- Mobile-first. Брейкпоінти: 768px, 1024px, 1440px. На 375px без горизонтальної прокрутки.

## 5. Компоненти та стани

| Компонент | Варіанти | Стани |
| --- | --- | --- |
| `Button` | primary, quiet, outline; sm, md; arrow; full | default, hover, focus, pressed, disabled |
| `CircleButton` | за іконкою | default, hover, focus, pressed, disabled |
| `TextLink` | nav, inline | default, hover, focus, current |
| `Tabs` | segmented, pills; badge | default, selected, hover, focus, disabled |
| `Switch` | | off, on, focus, disabled |
| `Accordion` | | closed, open, hover, focus |
| `Card` | surface, raised, dark, blush, glass; lift | default, hover (з lift) |
| `Progress` | value 0–100 | порожній, у процесі, повний |
| `Wave` | | активна, тиша |
| `Bubble` | client, nora | повідомлення, друкує |
| `CalendarSlot` | booked, new, empty | |
| `Chip` | glass, solid, dark; mono | статичний |
| `Tag` | default, ink; icon | статичний |
| `PillLabel`, `SectionHeading` | align start, center | статичні |
| `Avatar` | tone 1–4 | статичний |
| `LiveDot` | | пульсує |
| `Icon` | 11 іконок Phosphor Light; 16, 18, 20 | |
| `Flower` | position | повільно «дихає» |

Атрибут `data-state="hover|focus|active"` показує стан без миші. Він потрібен лише для вітрини.

**Головна дія** на екрані одна: `primary`. Друга поруч: `quiet`. У тарифах невиділені плани: `outline`.

## 6. Прийоми

- **Плитки (bento):** без тіней, щілина `--tile-gap`, суміш фото, сірих і темних плиток.
- **Квітка:** `<Flower>` у блоці з `position: relative`.
- **Скло:** `Card variant="glass"` або `Chip` поверх фото.
- **Темні вставки:** `Card variant="dark"` або `.is-dark`.
- **Футер:** темний, з гігантським словом «Nora» (`--font-size-wordmark`).
- **Шапка:** прилипає вгорі, фон `--color-bg-header`, тонка лінія після прокрутки.

## 7. Рух

- Криві `--ease-out`, `--ease-soft`; тривалості `--duration-*`. Без пружинних відскоків.
- Наведення тільки там, де є миша; на дотикових екранах картки не «залипають».
- `prefers-reduced-motion` вимикає всю анімацію.
- Прокручувальні анімації з макета (GSAP, Lenis) ще не перенесені.

## 8. Доступність

- Фокус видно на кожному інтерактивному елементі.
- Кнопка лише з іконкою має `label`.
- Один `<h1>` на сторінці, рівні заголовків без пропусків.
- Другорядний текст на фоні має контраст 5.6:1 (за коментарем у макеті).

## 9. Чого в системі немає

У макеті немає полів форм, станів помилки й завантаження, спливних вікон і сповіщень. **Не вигадуй їх.** Спочатку погодь із дизайнеркою, потім додай сюди, у токени, у компонент і на `/components`.

## 10. Рішення щодо суперечностей макета

- Де стилі переписували самі себе, діє пізніший варіант (v3).
- Прихована плаваюча шапка, смужки прогресу в табах та інший мертвий код не переносяться.
- Макет спершу робив десктоп; проєкт використовує mobile-first і свої брейкпоінти.

**Відкриті питання по текстах макета:** заглушка `[your business]` у hero; «Thursday, Mar 14» не збігається з 2026/2027 роком; посилання Log in, Contact, Privacy, Terms порожні.
