# Figma Inspector (cv0) — Отчёт инспекции

**Дата:** 25 октября 2025  
**Файл:** M_IN_CENTER (`CvPUKvcPXCz3dulwSrGhkB`)  
**Обработано фреймов:** 8

---

## Обработанные фреймы

| № | Node ID | Название | Размер (w×h) | Выход |
|---|---------|----------|--------------|-------|
| 1 | `682:2` | Home_final | 1920×10285 | `home_final-682-2/` |
| 2 | `724:466` | Catalog | 1920×3699 | `catalog-724-466/` |
| 3 | `198:1991` | Home 2 | 1920×9713 | `home-2-198-1991/` |
| 4 | `530:911` | Direct page_p | 393×5436 | `direct_page_p-530-911/` |
| 5 | `107:11` | Home 2 | 1920×10158 | `home-2-107-11/` |
| 6 | `203:174` | Home 2 | 1920×10168 | `home-2-203-174/` |
| 7 | `217:4` | Home 2 | 1920×10168 | `home-2-217-4/` |
| 8 | `257:3` | Home_final | 1920×10285 | `home_final-257-3/` |

---

## Структура вывода

```
out/figma/CvPUKvcPXCz3dulwSrGhkB/frames/
├── home_final-682-2/
│   ├── frame.json           # Полные данные фрейма и детей
│   ├── issues.json          # Найденные проблемы (аудиты)
│   ├── tokens.min.json      # Токены (цвета, шрифты, тени, радиусы)
│   └── overlay@2x.png       # PNG оверлей @2x для PerfectPixel
├── catalog-724-466/
│   ├── frame.json
│   ├── issues.json
│   ├── tokens.min.json
│   └── overlay@2x.png
└── ... (остальные 6 фреймов)
```

---

## Извлечённые данные

Для каждого фрейма извлечены:

### Геометрия и структура
- ✅ `absoluteBoundingBox` (x, y, w, h)
- ✅ `absoluteRenderBounds` (с учётом теней/свечений)
- ✅ Иерархия детей (глубина 1)

### Auto-layout
- ✅ `layoutMode` (HORIZONTAL/VERTICAL)
- ✅ Паддинги (`paddingTop/Right/Bottom/Left`)
- ✅ `itemSpacing`, `counterAxisSpacing`
- ✅ Sizing modes и alignment

### Текст-стили
- ✅ `fontFamily`, `fontSize`, `lineHeight`, `letterSpacing`
- ✅ `textCase`, `textDecoration`, `textAutoResize`
- ✅ Превью контента (≤120 симв.)

### Визуальные параметры
- ✅ **Fills:** Цвета (HEX), градиенты
- ✅ **Strokes:** Обводки
- ✅ **Effects:** Тени (DROP_SHADOW, INNER_SHADOW), размытие (BLUR)
- ✅ **Radii:** Радиусы скругления (cornerRadius, rectangleCornerRadii)

### Сетки
- ✅ `layoutGrids` (колонки, гаттеры, маргины)

### Constraints
- ✅ Привязки для детей (`constraints`, `resizing`)

---

## Аудиты (Issues)

Для каждого фрейма проверены:

| Аудит | Описание | Найдено проблем |
|-------|----------|-----------------|
| **offGrid** | Элементы с координатами не кратными 4px (8pt-grid) | 0 |
| **gapDrift** | Разные `itemSpacing` у одноуровневых групп (±1px) | 0 |
| **paddingMismatch** | Расхождения паддингов у однотипных контейнеров | 0 |
| **gridMisalign** | Несовпадение краёв контейнеров с layoutGrids | N/A |
| **typoDrift** | Разные lineHeight/letterSpacing в одной типосемье | **4–5 групп** |
| **colorNearDuplicates** | Почти одинаковые HEX (дельта <1 по каналу) | 0 |
| **shadowRadiusInconsistencies** | Близкие тени/радиусы с разными именами | N/A |

### Пример typoDrift (home_final-682-2)

```json
"typoDrift": [
  {
    "family_size": "NT Somic-24.0",
    "lineHeights": [32.496, 31.440],
    "letterSpacings": [0.0]
  },
  {
    "family_size": "Unbounded-64.0",
    "lineHeights": [76.0, 86.0],
    "letterSpacings": [0.0]
  },
  {
    "family_size": "Unbounded-40.0",
    "lineHeights": [40.0, 49.600],
    "letterSpacings": [0.0]
  },
  {
    "family_size": "NT Somic-40.0",
    "lineHeights": [42.0, 52.400],
    "letterSpacings": [0.0]
  }
]
```

**Рекомендация:** Унифицировать `lineHeight` для одинаковых font-family + fontSize комбинаций.

---

## Токены (Design Tokens)

### Цвета (топ-5 по частоте, home_final-682-2)

| HEX | Кол-во использований |
|-----|----------------------|
| `#E7E3DA` | 91 |
| `#261C15` | 63 |
| `#9C4124` | 37 |
| `#26140C` | 3 |
| `#444444` | 1 |

### Типографика (примеры)

- **Unbounded 64px** → lineHeight 76–86 (drift!)
- **NT Somic 24px** → lineHeight 31.4–32.5 (drift!)
- **Unbounded 40px** → lineHeight 40–49.6 (drift!)
- **Caveat 83px** → lineHeight 75

### Тени (уникальные параметры)

- `(0, 0, blur=5, spread=0-1)` — основная тень карточек
- `(0, 4, blur=4, spread=0)` — кнопки
- `(4, 7, blur=11.2, spread=0)` — глубокие тени
- `(0, 0, blur=17.7-19.5, spread=0)` — мягкие свечения
- **Размытие фона:** `blur=70–386.6`

### Радиусы скругления

```json
[0, 12, 18, 26, 30, 34, 35.5, 40, 50, 58, 62]
```

**Рекомендация:** Привести к шагу 4px: `[0, 12, 16, 24, 32, 36, 40, 48, 56, 60]`

---

## PNG Оверлеи @2x

Все 8 фреймов экспортированы как PNG @2x с параметром `use_absolute_bounds=true`:

- ✅ `home_final-682-2/overlay@2x.png` (1920×10285 @2x)
- ✅ `catalog-724-466/overlay@2x.png` (1920×3699 @2x)
- ✅ `home-2-198-1991/overlay@2x.png` (1920×9713 @2x)
- ✅ `direct_page_p-530-911/overlay@2x.png` (393×5436 @2x)
- ✅ `home-2-107-11/overlay@2x.png` (1920×10158 @2x)
- ✅ `home-2-203-174/overlay@2x.png` (1920×10168 @2x)
- ✅ `home-2-217-4/overlay@2x.png` (1920×10168 @2x)
- ✅ `home_final-257-3/overlay@2x.png` (1920×10285 @2x)

**Применение:** Загрузить в PerfectPixel / PixelParallel для pixel-perfect валидации HTML вёрстки.

---

## Метаданные файла

- **Название:** M_IN_CENTER
- **Последнее изменение:** 2025-10-24 10:27:42 UTC
- **Версия:** 2278432305679708706

---

## Обработка сбоев

- ✅ Rate-limiting соблюдён (пауза 0.2с между фреймами)
- ✅ Retry-After заголовки учтены
- ✅ Истечение токена обнаружено и исправлено
- ✅ Отсутствующие узлы добавлены в `issues.missingNodes` (не найдено)

---

## Следующие шаги

1. **Унификация типографики:**
   - Исправить расхождения в `lineHeight` для одинаковых font-family + fontSize
   - Проверить `letterSpacing` на консистентность

2. **Оптимизация радиусов:**
   - Привести к 4px-шагу (8pt-grid)
   - Создать переменные для повторяющихся значений

3. **Pixel-perfect вёрстка:**
   - Использовать `overlay@2x.png` для валидации верстки
   - Проверить соответствие с допуском ±0.5px для геометрии

4. **Design Tokens:**
   - Экспортировать цвета/шрифты/тени в формат CSS Custom Properties
   - Синхронизировать с Figma Tokens / Style Dictionary

---

## Команды для работы с данными

### Просмотр JSON
```bash
# Фрейм целиком
cat out/figma/CvPUKvcPXCz3dulwSrGhkB/frames/home_final-682-2/frame.json | jq .

# Только проблемы
cat out/figma/CvPUKvcPXCz3dulwSrGhkB/frames/home_final-682-2/issues.json | jq .

# Только токены
cat out/figma/CvPUKvcPXCz3dulwSrGhkB/frames/home_final-682-2/tokens.min.json | jq .
```

### Статистика
```bash
# Сколько уникальных цветов
cat out/figma/CvPUKvcPXCz3dulwSrGhkB/frames/*/tokens.min.json | jq -r '.colors[].hex' | sort -u | wc -l

# Сколько детей в фрейме
cat out/figma/CvPUKvcPXCz3dulwSrGhkB/frames/home_final-682-2/frame.json | jq '.children | length'
```

---

**Инспекция завершена.** Все данные в `out/figma/`.
