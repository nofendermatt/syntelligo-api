# Syntelligo API Documentation

A multilingual semantic knowledge graph API for advanced language understanding. Retrieve definitions, synonyms, antonyms, hypernyms, hyponyms, etymology, example usage, and more. Ideal for AI-powered apps, semantic search, translation workflows, and linguistic research.

The **Syntelligo JSON REST API** provides access to a **structured, multilingual linguistic knowledge graph**, built on graph-database principles for fast, natural exploration of semantic relationships. Perfect for:

- AI-powered apps needing nuanced language understanding  
- Semantic search systems with domain awareness  
- Language tools, translation workflows, and cross-lingual services

Explore definitions, synonyms, antonyms, hypernyms, hyponyms, domain tags, example usage, and more through clean, expressive JSON endpoints.

Get access to the API:
[Available on RapidAPI](https://rapidapi.com/syntelligo-syntelligo-default/api/syntelligo-linguistic-graph-api)

See example:

[Digilex.no](https://digilex.no/345972/bil)

##  Features

- Lookup word definitions\
- Semantic relations (synonyms, antonyms, hypernyms, etc.)\
- Multi-language support (e.g. Norwegian Bokmål `nob`, English `eng`)\
- RESTful JSON responses\
- ...and more (see full table below)


## Supported Languages
Norwegian bokmaal is the main language currently supported. Expansion to English is in progress, and additional languages are planned on the roadmap.

| Language         | Code | Comment
| ---------------- | ---- | ------------ |
| Norsk Bokmål     | nob  | Main         |
| English          | eng  | In progress  |
| Norsk Nynorsk    | nno  | In progress  |
| Nordsamisk       | sme  | In roadmap   |
| Sørsamisk        | sma  | In roadmap   |
| Lulesamisk       | smj  | In roadmap   |
| Danish           | dan  | In roadmap   |
| Swedish          | swe  | In roadmap   |
| Dutch            | nld  | In roadmap   |
| French           | fra  | In roadmap   |
| German           | deu  | In roadmap   |
| Spanish          | spa  | In roadmap   |
| Italian          | ita  | In roadmap   |




## Endpoints

| Endpoint                                | Description                                                        |
|-----------------------------------------|--------------------------------------------------------------------|
| `GET /api/v1/{lang}/{word}`             | Fetch full word data for a word: pronunciation, etymology, tags, examples, and semantic relations |
| `GET /api/v1/{lang}/{word}/definitions` | Retrieve only definitions                                           |
| `GET /api/v1/{lang}/{word}/{relation}`  | Retrieve a specific relation (e.g. synonyms, antonyms, hypernyms) |
| `GET /api/v1/{lang}/{word}/depth/{n}`   | Explore the semantic graph up to *n* levels deep                   |
| `GET /api/v1/{word}/{id}`             | Fetch full word data for an exact word: pronunciation, etymology, tags, examples, and semantic relations |



---

### Word Lookup (all relations)

```
GET /api/v1/{lang}/{word}
```

Returns the word with all definitions and semantic relations.


**Response:**

```json
{
  "word": "bil",
  "lang": "nob",
  "results": [
    {
      "id": "931739",
      "definition": "Et kjøretøy med fire hjul...",
      "partOfSpeech": "noun",
      "synonym": [...],
      "antonym": [...],
      "hypernym": [...],
      "hyponym": [...],
      "meronym_part": [...],
      "holonym_part": [...],
      "related_term": [...],
      "near_synonym": [...],
      "slang_synonym": [...]
    }
  ]
}
```

---

### Definitions Only

```
GET /api/v1/{lang}/{word}/definitions
```

Returns only definitions (including ID per sense).


**Response:**

```json
{
  "word": "slå",
  "lang": "nob",
  "definitions": [
    {
      "id": "1234",
      "definition": "å beseire eller overvinne.",
      "partOfSpeech": "verb"
    },
    {
      "id": "1235",
      "definition": "å slå - Å treffe med kraft;",
      "partOfSpeech": "noun"
    }
  ]
}
```

---

###  Specific Relation Lookup

```
GET /api/v1/{lang}/{word}/{relation}
```

Returns only the requested relation type.

**Available Relations:**

- `synonyms`
- `antonyms`
- `hypernyms`
- `hyponyms`
- `meronyms`
- `holonyms`
- `related_terms`
- `eq_synonyms` (cross-language equivalents)
- ...and more (see full table below)



**Response:**

```json
{
  "word": "bil",
  "lang": "nob",
  "results": [
    {
      "id": "931739",
      "word": "bil",
      "partOfSpeech": "noun",
      "synonym": [
        {
          "id": "914946",
          "name": "automobil",
          "definition": "Et kjøretøy med fire hjul...",
          "partOfSpeech": "noun",
          "lang": "nob"
        }
      ]
    }
  ]
}
```


## Supported Relation Types

| API Relation         | Description                                |
| -------------------- | ------------------------------------------ |
| synonym              | Words with similar meanings                |
| slang\_synonym       | Slang variants                             |
| eqSynonym            | Cross-language equivalents                 |
| antonym              | Words with opposite meanings               |
| hypernym             | More general terms                         |
| hyponym              | More specific terms                        |
| hypernym\_instance   | A specific instance of a broader category  |
| hyponym\_instance    | An instance of the narrower category       |
| holonym\_part        | Whole that includes this part              |
| holonym\_member      | Whole that includes this member            |
| holonym\_substance   | Whole made of this substance               |
| meronym\_part        | Part of the whole                          |
| meronym\_member      | Member of a collection                     |
| meronym\_substance   | Substance making up the whole              |
| related\_form        | Morphological or derived forms             |
| related\_term        | General related concepts                   |
| near\_synonym        | Near-synonyms (not fully identical)        |
| troponym             | More specific ways of performing an action |
| entails              | A implies B                                |
| entailed\_by         | A is implied by B                          |
| instrument           | Tool or means used                         |
| involved\_instrument | Tool involved in the action                |
| causes               | Cause-effect relationships                 |

---

## Field Refefence
| Field / Relation    | Type           | Description                            |
| ------------------- | -------------- | -------------------------------------- |
| `id`                | string         | Unique identifier                      |
| `name`              | string         | Canonical word form                    |
| `ipa`               | string         | Pronunciation (IPA)                    |
| `nameLower`         | string         | Lowercase word form                    |
| `etymology`         | string         | Historical origin                      |
| `definition`        | string         | Core meaning                           |
| `partOfSpeech`      | string         | POS tag (noun, verb, etc.)             |            |
| `genus`             | \[string]      | Grammatical gender(s)                  |

| `tags`              | \[string]      | JSON-encoded thematic labels           |
| `example`           | \[string]      | JSON-encoded usage examples            |
| `type`              | string         | Item type (`"Word"`)                   |
| `lang`              | string         | Language code (e.g. `"nob"`)           |
           |


## 📜 License
This API and its data are offered as a paid commercial service. All rights reserved. Redistribution or commercial use without permission is prohibited.
