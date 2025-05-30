# Alignment Prompt

## Purpose

Align each source morpheme (Greek/Hebrew) with its matching English token, supporting:

## Alignment Decision Logic

**Alignments between Source and Translation tokens must be:**
- **1** to **1**
- **1** to **many** / **many** to **1**
- **many** to **many**
- **NEQ** (no equivalent). Words with no relation as:
  - **None** to **1**
  - **1** to **None**
  - **Many** to **None**
  - **None** to **many**

**Roles of each alignment should be:**
1. Primary (direct semantic match; highest Primaries)
2. Secondary (grammatical/supportive)
3. IdiomPrimary / IdiomSecondary (translation with dynamic or functional equivalence)
4. NEQ (no equivalent)

**Other rules:**
- "Primary" tokens works as the core of each alignment.
- Use the smallest amount possible of "Primaries" for each alignment and for each side
- If **many** to **many**, find the core words (Primaries) of each side and leave the others as Secondary
- Make a full first alignment forcing **1** to **1**, in each verse
  - Once done, evaluate if it is better 1⇔many / many⇔1, many⇔many
  - All roles are valuable. If NEQ is better (no equivalence or unclear tokens), use it.
- Each token with its own ID (A & B) must appear exactly once in all alignments.
- Sort output by WN_ID, then Translation_id.

## Input

### Side A: Translation

| Translation_term   |   Translation_id | Verse_ID   |
|:-------------------|-----------------:|:-----------|
| The                |                1 | CJB        |
| earth              |                2 | CJB        |
| was                |                3 | CJB        |
| unformed           |                4 | CJB        |
| and                |                5 | CJB        |
| void               |                6 | CJB        |
| ,                  |                7 | CJB        |
| darkness           |                8 | CJB        |
| was                |                9 | CJB        |
| on                 |               10 | CJB        |
| the                |               11 | CJB        |
| face               |               12 | CJB        |
| of                 |               13 | CJB        |
| the                |               14 | CJB        |
| deep               |               15 | CJB        |
| ,                  |               16 | CJB        |
| and                |               17 | CJB        |
| the                |               18 | CJB        |
| Spirit             |               19 | CJB        |
| of                 |               20 | CJB        |
| God                |               21 | CJB        |
| hovered            |               22 | CJB        |
| over               |               23 | CJB        |
| the                |               24 | CJB        |
| surface            |               25 | CJB        |
| of                 |               26 | CJB        |
| the                |               27 | CJB        |
| water              |               28 | CJB        |
| .                  |               29 | CJB        |

### Side B: Source

|   B_term_id |   WN_ID | Word   |   Verse | Verse ID   | Fast Translation   | Morphology   | Lemma   |
|------------:|--------:|:-------|--------:|:-----------|:-------------------|:-------------|:--------|
|           1 |     8.1 | וְ      |       2 | bhs.1.1.2  | and                | C            | וְ       |
|           2 |     8.2 | הָ      |       2 | bhs.1.1.2  | the                | A            | הַ       |
|           3 |     8.3 | אָ֗רֶץ    |       2 | bhs.1.1.2  | earth              | NC-SA        | אֶ֫רֶץ     |
|           4 |     9   | הָיְתָ֥ה   |       2 | bhs.1.1.2  | be                 | VaP3FS       | היה     |
|           5 |    10   | תֹ֙הוּ֙    |       2 | bhs.1.1.2  | wasteland          | NC-SA        | תֹּ֫הוּ     |
|           6 |    11.1 | וָ      |       2 | bhs.1.1.2  | and                | C            | וְ       |
|           7 |    11.2 | בֹ֔הוּ    |       2 | bhs.1.1.2  | empty              | NC-SA        | בֹּ֫הוּ     |
|           8 |    12.1 | וְ      |       2 | bhs.1.1.2  | and                | C            | וְ       |
|           9 |    12.2 | חֹ֖שֶׁךְ    |       2 | bhs.1.1.2  | darkness           | NC-SA        | חֹ֫שֶׁךְ     |
|          10 |    13   | עַל     |       2 | bhs.1.1.2  | over               | P            | עַל      |
|          11 |    14   | פְּנֵ֣י    |       2 | bhs.1.1.2  | face|surface       | NCMPC        | פָּנֶה     |
|          12 |    15   | תְה֑וֹם   |       2 | bhs.1.1.2  | the_deep           | NC-SA        | תְּהוֹם    |
|          13 |    16.1 | וְ      |       2 | bhs.1.1.2  | and                | C            | וְ       |
|          14 |    16.2 | ר֣וּחַ    |       2 | bhs.1.1.2  | spirit/breath      | NC-SC        | רוּחַ     |
|          15 |    17   | אֱלֹהִ֔ים  |       2 | bhs.1.1.2  | God                | NCMPA        | אֱלֹהִים   |
|          16 |    18   | מְרַחֶ֖פֶת  |       2 | bhs.1.1.2  | hover              | VbR-FSA      | רחף     |
|          17 |    19   | עַל     |       2 | bhs.1.1.2  | over               | P            | עַל      |
|          18 |    20   | פְּנֵ֥י    |       2 | bhs.1.1.2  | face|surface       | NCMPC        | פָּנֶה     |
|          19 |    21.1 | הַ      |       2 | bhs.1.1.2  | the                | A            | הַ       |
|          20 |    21.2 | מָּֽיִם    |       2 | bhs.1.1.2  | waters             | NCMPA        | מַ֫יִם     |

### Tiny Table (stats from other alignments)

| Translation_term   | Source_term   |   Source_wn_id |   Sorting | Source_lemma   | Source_morphology   |   Primaries |   Secondaries |   IdiomPrimaries |   IdiomSecondaries |   NEQs |
|:-------------------|:--------------|---------------:|----------:|:---------------|:--------------------|------------:|--------------:|-----------------:|-------------------:|-------:|
| now                | וְ             |            8.1 |      4    | וְ              | C                   |           8 |             0 |                0 |                  0 |      0 |
| {NEQ}              | וְ             |            8.1 |      7    | וְ              | C                   |           0 |             0 |                0 |                  0 |     10 |
| and                | וְ             |            8.1 |     15    | וְ              | C                   |           4 |             0 |                0 |                  0 |      0 |
| the                | הָ             |            8.2 |      5    | הַ              | A                   |          24 |             0 |                0 |                  0 |      0 |
| earth              | אָ֗רֶץ           |            8.3 |      6    | אֶ֫רֶץ            | NC-SA               |          24 |             0 |                0 |                  0 |      0 |
| hath               | הָיְתָ֥ה          |            9   |      3    | היה            | VaP3FS              |           0 |             0 |                0 |                  0 |      0 |
| existed            | הָיְתָ֥ה          |            9   |      4    | היה            | VaP3FS              |           0 |             0 |                0 |                  0 |      0 |
| was                | הָיְתָ֥ה          |            9   |      7.33 | היה            | VaP3FS              |          24 |             0 |                0 |                  0 |      0 |
| empty              | תֹ֙הוּ֙           |           10   |      9    | תֹּ֫הוּ            | NC-SA               |           0 |             0 |                0 |                  0 |      0 |
| formless           | תֹ֙הוּ֙           |           10   |      9    | תֹּ֫הוּ            | NC-SA               |          11 |             0 |                0 |                  0 |      0 |
| without            | תֹ֙הוּ֙           |           10   |      9    | תֹּ֫הוּ            | NC-SA               |           6 |             2 |                0 |                  0 |      0 |
| chaos              | תֹ֙הוּ֙           |           10   |     10    | תֹּ֫הוּ            | NC-SA               |           1 |             0 |                0 |                  0 |      0 |
| form               | תֹ֙הוּ֙           |           10   |     10    | תֹּ֫הוּ            | NC-SA               |           7 |             0 |                0 |                  0 |      0 |
| shape              | תֹ֙הוּ֙           |           10   |     10    | תֹּ֫הוּ            | NC-SA               |           1 |             0 |                0 |                  0 |      0 |
| waste              | תֹ֙הוּ֙           |           10   |     17    | תֹּ֫הוּ            | NC-SA               |           1 |             0 |                0 |                  0 |      0 |
| {NEQ}              | וָ             |           11.1 |      4    | וְ              | C                   |           0 |             0 |                0 |                  0 |      1 |
| and                | וָ             |           11.1 |      9.5  | וְ              | C                   |          22 |             0 |                0 |                  0 |      0 |
| empty              | בֹ֔הוּ           |           11.2 |      9.67 | בֹּ֫הוּ            | NC-SA               |           8 |             0 |                0 |                  0 |      0 |
| void               | בֹ֔הוּ           |           11.2 |     11.33 | בֹּ֫הוּ            | NC-SA               |          12 |             0 |                0 |                  0 |      0 |
| a                  | בֹ֔הוּ           |           11.2 |     13    | בֹּ֫הוּ            | NC-SA               |           0 |             1 |                0 |                  0 |      0 |
| desolate           | בֹ֔הוּ           |           11.2 |     14    | בֹּ֫הוּ            | NC-SA               |           0 |             1 |                0 |                  0 |      0 |
| emptiness          | בֹ֔הוּ           |           11.2 |     15    | בֹּ֫הוּ            | NC-SA               |           1 |             0 |                0 |                  0 |      0 |
| waste              | בֹ֔הוּ           |           11.2 |     23    | בֹּ֫הוּ            | NC-SA               |           1 |             0 |                0 |                  0 |      0 |
| {NEQ}              | וְ             |           12.1 |      5    | וְ              | C                   |           0 |             0 |                0 |                  0 |      8 |
| and                | וְ             |           12.1 |     11.25 | וְ              | C                   |          15 |             0 |                0 |                  0 |      0 |
| with               | וְ             |           12.1 |     26    | וְ              | C                   |           1 |             0 |                0 |                  0 |      0 |
| darkness           | חֹ֖שֶׁךְ           |           12.2 |     12.17 | חֹ֫שֶׁךְ            | NC-SA               |          24 |             0 |                0 |                  0 |      0 |
| upon               | עַל            |           13   |     13    | עַל             | P                   |           5 |             0 |                0 |                  0 |      0 |
| over               | עַל            |           13   |     15    | עַל             | P                   |          11 |             0 |                0 |                  0 |      0 |
| covered            | עַל            |           13   |     19    | עַל             | P                   |           5 |             0 |                0 |                  0 |      0 |
| on                 | עַל            |           13   |     26    | עַל             | P                   |           2 |             0 |                0 |                  0 |      0 |
| face               | פְּנֵ֣י           |           14   |     15    | פָּנֶה            | NCMPC               |          11 |             0 |                0 |                  0 |      0 |
| of                 | פְּנֵ֣י           |           14   |     16    | פָּנֶה            | NCMPC               |           0 |            19 |                0 |                  0 |      0 |
| the                | פְּנֵ֣י           |           14   |     16.17 | פָּנֶה            | NCMPC               |           0 |            22 |                0 |                  0 |      0 |
| surface            | פְּנֵ֣י           |           14   |     21.5  | פָּנֶה            | NCMPC               |          11 |             0 |                0 |                  0 |      0 |
| waters             | תְה֑וֹם          |           15   |     17    | תְּהוֹם           | NC-SA               |           1 |             0 |                0 |                  0 |      0 |
| deep               | תְה֑וֹם          |           15   |     17.75 | תְּהוֹם           | NC-SA               |          20 |             0 |                0 |                  0 |      0 |
| the                | תְה֑וֹם          |           15   |     19.33 | תְּהוֹם           | NC-SA               |           0 |            22 |                0 |                  0 |      0 |
| ocean              | תְה֑וֹם          |           15   |     20    | תְּהוֹם           | NC-SA               |           0 |             0 |                0 |                  0 |      0 |
| of                 | תְה֑וֹם          |           15   |     22.5  | תְּהוֹם           | NC-SA               |           0 |             2 |                0 |                  0 |      0 |
| watery             | תְה֑וֹם          |           15   |     24.5  | תְּהוֹם           | NC-SA               |           2 |             1 |                0 |                  0 |      0 |
| depths             | תְה֑וֹם          |           15   |     25.5  | תְּהוֹם           | NC-SA               |           2 |             0 |                0 |                  0 |      0 |
| and                | וְ             |           16.1 |     18.17 | וְ              | C                   |          21 |             0 |                0 |                  0 |      0 |
| while              | וְ             |           16.1 |     19    | וְ              | C                   |           1 |             0 |                0 |                  0 |      0 |
| but                | וְ             |           16.1 |     22    | וְ              | C                   |           1 |             0 |                0 |                  0 |      0 |
| the                | ר֣וּחַ           |           16.2 |     19.17 | רוּחַ            | NC-SC               |           0 |            22 |                0 |                  0 |      0 |
| a                  | ר֣וּחַ           |           16.2 |     20    | רוּחַ            | NC-SC               |           0 |             1 |                0 |                  0 |      0 |
| spirit             | ר֣וּחַ           |           16.2 |     20.17 | רוּחַ            | NC-SC               |          21 |             0 |                0 |                  0 |      0 |
| of                 | ר֣וּחַ           |           16.2 |     21.17 | רוּחַ            | NC-SC               |           0 |            21 |                0 |                  0 |      0 |
| from               | ר֣וּחַ           |           16.2 |     22    | רוּחַ            | NC-SC               |           0 |             1 |                0 |                  0 |      0 |
| wind               | ר֣וּחַ           |           16.2 |     27    | רוּחַ            | NC-SC               |           2 |             0 |                0 |                  0 |      0 |
| ruach              | ר֣וּחַ           |           16.2 |     30    | רוּחַ            | NC-SC               |           1 |             0 |                0 |                  0 |      0 |
| god                | אֱלֹהִ֔ים         |           17   |     22.17 | אֱלֹהִים          | NCMPA               |          22 |             0 |                0 |                  0 |      0 |
| elohim             | אֱלֹהִ֔ים         |           17   |     31    | אֱלֹהִים          | NCMPA               |           1 |             0 |                0 |                  0 |      0 |
| fluttering         | מְרַחֶ֖פֶת         |           18   |     18    | רחף            | VbR-FSA             |           0 |             0 |                0 |                  0 |      0 |
| was                | מְרַחֶ֖פֶת         |           18   |     23    | רחף            | VbR-FSA             |           0 |            17 |                0 |                  0 |      0 |
| hovering           | מְרַחֶ֖פֶת         |           18   |     24    | רחף            | VbR-FSA             |          11 |             0 |                0 |                  0 |      0 |
| moved              | מְרַחֶ֖פֶת         |           18   |     24    | רחף            | VbR-FSA             |           3 |             0 |                0 |                  0 |      0 |
| swept              | מְרַחֶ֖פֶת         |           18   |     24    | רחף            | VbR-FSA             |           1 |             0 |                0 |                  0 |      0 |
| moving             | מְרַחֶ֖פֶת         |           18   |     26    | רחף            | VbR-FSA             |           6 |             0 |                0 |                  0 |      0 |
| on                 | עַל            |           19   |     19    | עַל             | P                   |           0 |             0 |                0 |                  0 |      0 |
| over               | עַל            |           19   |     25    | עַל             | P                   |          20 |             0 |                0 |                  0 |      0 |
| upon               | עַל            |           19   |     25    | עַל             | P                   |           4 |             0 |                0 |                  0 |      0 |
| surface            | פְּנֵ֥י           |           20   |     25.5  | פָּנֶה            | NCMPC               |          12 |             0 |                0 |                  0 |      0 |
| the                | פְּנֵ֥י           |           20   |     26.83 | פָּנֶה            | NCMPC               |           0 |            21 |                0 |                  0 |      0 |
| face               | פְּנֵ֥י           |           20   |     28.5  | פָּנֶה            | NCMPC               |           9 |             0 |                0 |                  0 |      0 |
| of                 | פְּנֵ֥י           |           20   |     28.67 | פָּנֶה            | NCMPC               |           0 |            21 |                0 |                  0 |      0 |
| the                | הַ             |           21.1 |     28.67 | הַ              | A                   |          24 |             0 |                0 |                  0 |      0 |
| waters             | מָּֽיִם           |           21.2 |     29.83 | מַ֫יִם            | NCMPA               |          19 |             0 |                0 |                  0 |      0 |
| water              | מָּֽיִם           |           21.2 |     32    | מַ֫יִם            | NCMPA               |           5 |             0 |                0 |                  0 |      0 |

## JSON Output

Structure:

```jsonc
{
  "verse_id": "<Verse_ID>",
  "alignments": [
    {
      "alignment_id": <int>,
      "sides": {
        "A": [
          { "role": "<Role>", "term_id": <int>, "term": "<Translation (eg. English) token>" },
          …
        ],
        "B": [
          { "role": "<Role>", "term_id": <WN_ID>, "term": "<Greek/Hebrew token>" },
          …
        ]
      }
    },
    …
  ]
}
```


- "A": uses Translation_id (Side A)
- "B": uses WN_ID (Side B)
- "role": Primary, Secondary, IdiomPrimary, IdiomSecondary, or NEQ
- If a term on one side has no relationship to any term on the other side, role is NEQ

## Validation Checklist (internal, do not include)

- Each WN_ID and Translation_id used once.
- Roles follow Tiny Table counts.
- Punctuation tokens alone as NEQ.
- Follow schema strictly.

## Edge Cases

- Implicit→explicit pronouns: Secondary
- Definite/indefinite mismatch: unmatched article as Secondary
- Sentence-final punctuation: NEQ

Answer with JSON only, using the schema. No extra explanations.
