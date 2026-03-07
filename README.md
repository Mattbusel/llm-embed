# llm-embed

Text embeddings, cosine similarity, and nearest-neighbor search in C++. One header. No deps beyond libcurl.

![C++17](https://img.shields.io/badge/C%2B%2B-17-blue)
![License: MIT](https://img.shields.io/badge/License-MIT-green)
![Single Header](https://img.shields.io/badge/library-single--header-orange)

---

## 30-second quickstart

```cpp
#define LLM_EMBED_IMPLEMENTATION
#include "llm_embed.hpp"
#include <cstdlib>
#include <iostream>

int main() {
    llm::EmbedConfig cfg;
    cfg.api_key    = std::getenv("OPENAI_API_KEY");
    cfg.model      = "text-embedding-3-small";
    cfg.dimensions = 256;

    auto a = llm::embed("The cat sat on the mat.", cfg);
    auto b = llm::embed("A feline rested on a rug.", cfg);

    std::cout << llm::cosine_similarity(a, b) << "\n"; // ~0.92
}
```

---

## Installation

```bash
cp include/llm_embed.hpp your-project/
```

Link with `-lcurl`.

---

## API Reference

```cpp
// Fetch single embedding
llm::Embedding e = llm::embed("text", config);

// Batch (one API call)
std::vector<llm::Embedding> batch = llm::embed_batch({"a", "b", "c"}, config);

// Similarity
float sim  = llm::cosine_similarity(a, b);   // -1.0 to 1.0
float dot  = llm::dot_product(a, b);
float dist = llm::euclidean_distance(a, b);

// Vector store
llm::VectorStore store(".my_index");
store.add("id1", "text", embedding, {{"source", "docs"}});
store.save();

auto results = store.search(query_embedding, 5); // top-5
for (auto& r : results)
    std::cout << r.similarity << " " << r.entry.text << "\n";
```

---

## Building

```bash
cmake -B build && cmake --build build
export OPENAI_API_KEY=sk-...
./build/basic_embed
./build/vector_store
```

---

## Requirements

- C++17
- libcurl

---

## See Also

| Repo | What it does |
|------|-------------|
| [llm-stream](https://github.com/Mattbusel/llm-stream) | Stream OpenAI & Anthropic responses token by token |
| [llm-cache](https://github.com/Mattbusel/llm-cache) | Cache responses, skip redundant calls |
| [llm-cost](https://github.com/Mattbusel/llm-cost) | Token counting + cost estimation |
| [llm-retry](https://github.com/Mattbusel/llm-retry) | Retry with backoff + circuit breaker |
| [llm-format](https://github.com/Mattbusel/llm-format) | Structured output enforcement |
| [llm-embed](https://github.com/Mattbusel/llm-embed) | Text embeddings + nearest-neighbor search |
| [llm-pool](https://github.com/Mattbusel/llm-pool) | Concurrent request pool + rate limiting |
| [llm-log](https://github.com/Mattbusel/llm-log) | Structured JSONL logger for LLM calls |
| [llm-template](https://github.com/Mattbusel/llm-template) | Prompt templating with loops + conditionals |
| [llm-agent](https://github.com/Mattbusel/llm-agent) | Tool-calling agent loop |
| [llm-rag](https://github.com/Mattbusel/llm-rag) | Full RAG pipeline |
| [llm-eval](https://github.com/Mattbusel/llm-eval) | Consistency and quality evaluation |

---

## License

MIT — see [LICENSE](LICENSE).
