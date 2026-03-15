# HistoryChat RAG

## Rozmowy z awatarami postaci historycznych

## Opis projektu

HistoryChat RAG to interaktywny system czatowy umożliwiający prowadzenie rozmów z wybranymi postaciami historycznymi. System wykorzystuje architekturę Retrieval-Augmented Generation (RAG), dzięki czemu odpowiedzi generowane przez model językowy opierają się na rzeczywistych źródłach historycznych, takich jak biografie, listy, publikacje naukowe czy dokumenty epoki.

Dodatkowo system może generować wizualny awatar postaci, dopasowany stylistycznie do epoki historycznej.

Projekt ma charakter edukacyjny i demonstracyjny — pokazuje, jak można połączyć:

- modele językowe (LLM),
- wyszukiwanie semantyczne,
- bazę wektorową,
- generowanie obrazów,

w jedną spójną aplikację.

## Diagram architektury RAG

Sekcja odnosi się do diagramu architektury systemu RAG z dokumentu źródłowego.

## Cel projektu

Celem projektu jest stworzenie systemu umożliwiającego:

- prowadzenie rozmów z postaciami historycznymi w formie czatu,
- generowanie odpowiedzi opartych na rzeczywistych źródłach historycznych,
- zachowanie stylu wypowiedzi dopasowanego do epoki,
- wizualizację rozmówcy w postaci awatara.

Projekt stanowi demonstrację zastosowania architektury RAG (Retrieval-Augmented Generation) w kontekście edukacyjnym i eksploracyjnym.

## Architektura systemu

System składa się z czterech głównych warstw:

### 1. Warstwa danych (Knowledge Base)

Dla każdej postaci historycznej przygotowywana jest oddzielna baza wiedzy zawierająca:

- biografie,
- listy,
- publikacje,
- artykuły naukowe,
- inne dokumenty historyczne.

Dokumenty są:

- dzielone na fragmenty (chunking),
- zamieniane na embeddingi,
- indeksowane w bazie wektorowej.

### 2. Retrieval (wyszukiwanie kontekstu)

Po zadaniu pytania przez użytkownika:

- pytanie zamieniane jest na embedding,
- system przeszukuje bazę wektorową,
- wybierane są najbardziej podobne fragmenty dokumentów.

Te fragmenty stanowią kontekst dla modelu językowego.

### 3. Generowanie odpowiedzi (LLM)

Na podstawie znalezionych fragmentów budowany jest prompt w stylu:

> Jesteś [POSTAĆ HISTORYCZNA].  
> Odpowiadasz w pierwszej osobie, zachowując styl wypowiedzi charakterystyczny dla swojej epoki.  
> Odpowiedz na pytanie użytkownika korzystając wyłącznie z poniższych informacji:  
> [KONTEKST Z RAG]  
> Pytanie użytkownika:  
> [PYTANIE]

Model językowy generuje odpowiedź symulując wypowiedź danej postaci.

Jeśli baza wiedzy nie zawiera informacji potrzebnych do odpowiedzi, system może zwrócić komunikat w stylu:

> „Nie przypominam sobie, abym zajmował się tym zagadnieniem.”

### 4. Generowanie awatara

System może generować wizualny portret postaci historycznej.

Przykładowy prompt:

`Realistic historical portrait of [POSTAĆ], oil painting style, historical accuracy, period clothing`

Możliwe modele:

- DALL-E,
- Stable Diffusion.

## Flow programu

### 1. Wybór postaci

Użytkownik wybiera postać historyczną z listy dostępnych osobowości, np.:

- Mikołaj Kopernik,
- Maria Skłodowska-Curie,
- Jan III Sobieski.

System ładuje odpowiadającą jej bazę wektorową.

### 2. Zadanie pytania

Użytkownik wpisuje pytanie, np.:

> „Co sądzisz o teorii heliocentrycznej?”

System wyszukuje w bazie wiedzy najbardziej trafne fragmenty dokumentów.

### 3. Generowanie odpowiedzi

Model językowy generuje odpowiedź:

- w pierwszej osobie,
- z zachowaniem stylu epoki,
- na podstawie fragmentów źródeł historycznych.

### 4. Prezentacja

Wynik prezentowany jest w formie:

- tekstowej odpowiedzi,
- opcjonalnego awatara postaci.

Interfejs może być:

- terminalowy (CLI),
- prostą aplikacją webową.

## Stack technologiczny

Projekt wykorzystuje następujące technologie:

- **Język:** Python,
- **Framework RAG:** LangChain,
- **Baza wektorowa:** FAISS (lokalna baza embeddingów),
- **Embeddingi:** sentence-transformers lub OpenAI embeddings,
- **LLM:** OpenAI lub lokalny model (np. Llama / Mistral),
- **Generowanie obrazów:** DALL-E lub Stable Diffusion.

## Struktura projektu

Przykładowa struktura katalogów:

```text
historychat-rag/
│
├── data/
│   ├── documents/
│   │   ├── copernicus/
│   │   ├── curie/
│   │   └── sobieski/
│   │
│   └── chat_history.jsonl
│
├── vector_store/
│   ├── copernicus_index
│   ├── curie_index
│   └── sobieski_index
│
├── src/
│   ├── rag_pipeline.py
│   ├── retriever.py
│   ├── llm_client.py
│   ├── avatar_generator.py
│   └── chat_interface.py
│
├── logs/
│   └── retrieval.log
│
├── requirements.txt
│
└── README.md
```

## Logowanie i historia rozmów

System zapisuje informacje pomocne do analizy działania RAG.

### Historia rozmów

`data/chat_history.jsonl`

Zawiera zapis dialogów użytkownika z postacią historyczną.

### Logi retrieval

`logs/retrieval.log`

Zawierają informacje:

- które fragmenty dokumentów zostały użyte,
- jakie było dopasowanie semantyczne,
- jakie źródła zostały przywołane w odpowiedzi.

## Możliwe rozszerzenia projektu

Potencjalne kierunki rozwoju:

- webowy interfejs użytkownika (FastAPI + frontend),
- dodanie większej liczby postaci historycznych,
- weryfikacja źródeł w odpowiedzi (cytowanie dokumentów),
- ocena jakości odpowiedzi (RAG evaluation),
- tryb rozmowy między postaciami historycznymi.