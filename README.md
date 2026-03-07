# llm-embed

Text embeddings + vector search for C++. One header, libcurl dep.

![C++17](https://img.shields.io/badge/C%2B%2B-17-blue.svg)
![License MIT](https://img.shields.io/badge/license-MIT-green.svg)
![Single Header](https://img.shields.io/badge/single-header-orange.svg)
![Requires libcurl](https://img.shields.io/badge/deps-libcurl-yellow.svg)

## Quickstart

```cpp
#define LLM_EMBED_IMPLEMENTATION
#include "llm_embed.hpp"

llm::EmbedConfig cfg;
cfg.api_key    = "sk-...";
cfg.model      = "text-embedding-3-small";
cfg.dimensions = 1536;

auto ea = llm::embed("The cat sat on the mat.", cfg);
auto eb = llm::embed("A feline rested on a rug.", cfg);

float sim = llm::cosine_similarity(ea, eb);
// sim ≈ 0.93 (semantically similar)
```

## Vector Store

```cpp
llm::VectorStore store("my_index.bin");
store.add("doc1", "Photosynthesis converts sunlight...", embedding);
store.save();

auto results = store.search(query_embedding, /*top_k=*/5);
for (auto& r : results)
    std::cout << r.similarity << " " << r.entry.text << "\n";
```

## API Reference

### Free functions

```cpp
Embedding embed(const std::string& text, const EmbedConfig& cfg);
std::vector<Embedding> embed_batch(const std::vector<std::string>& texts, const EmbedConfig& cfg);

float cosine_similarity(const Embedding& a, const Embedding& b);
float dot_product(const Embedding& a, const Embedding& b);
float euclidean_distance(const Embedding& a, const Embedding& b);
```

### VectorStore

```cpp
VectorStore store(filepath);      // Loads existing index from file
store.add(id, text, emb, meta);   // Upserts by id
store.remove(id);
store.search(query_emb, top_k);   // Returns vector<SearchResult> sorted by similarity
store.save();                      // Persist to binary file
store.size();                      // Number of entries
```

## Examples

| File | What it shows |
|------|--------------|
| [`examples/basic_embed.cpp`](examples/basic_embed.cpp) | Embed two sentences, compare cosine similarity |
| [`examples/vector_store.cpp`](examples/vector_store.cpp) | Index 5 docs, search by query |

## Building

Requires libcurl. On Windows with vcpkg: `vcpkg install curl`.

```bash
cmake -B build && cmake --build build
./build/basic_embed
./build/vector_store
```

## Requirements

C++17. Requires libcurl.

## See Also

| Repo | What it does |
|------|-------------|
| [llm-stream](https://github.com/Mattbusel/llm-stream) | Stream OpenAI and Anthropic responses via SSE |
| [llm-cache](https://github.com/Mattbusel/llm-cache) | LRU response cache |
| [llm-cost](https://github.com/Mattbusel/llm-cost) | Token counting and cost estimation |
| [llm-retry](https://github.com/Mattbusel/llm-retry) | Retry and circuit breaker |
| [llm-format](https://github.com/Mattbusel/llm-format) | Structured output / JSON schema |
| [llm-embed](https://github.com/Mattbusel/llm-embed) | Embeddings and vector search |
| [llm-pool](https://github.com/Mattbusel/llm-pool) | Concurrent request pool |
| [llm-log](https://github.com/Mattbusel/llm-log) | Structured JSONL logging |
| [llm-template](https://github.com/Mattbusel/llm-template) | Prompt templating |
| [llm-agent](https://github.com/Mattbusel/llm-agent) | Tool-calling agent loop |
| [llm-rag](https://github.com/Mattbusel/llm-rag) | RAG pipeline |
| [llm-eval](https://github.com/Mattbusel/llm-eval) | Evaluation and consistency scoring |
| [llm-chat](https://github.com/Mattbusel/llm-chat) | Conversation memory manager |
| [llm-vision](https://github.com/Mattbusel/llm-vision) | Multimodal image+text |
| [llm-mock](https://github.com/Mattbusel/llm-mock) | Mock LLM for testing |
| [llm-router](https://github.com/Mattbusel/llm-router) | Model routing by complexity |
| [llm-guard](https://github.com/Mattbusel/llm-guard) | PII detection and injection guard |
| [llm-compress](https://github.com/Mattbusel/llm-compress) | Context compression |
| [llm-batch](https://github.com/Mattbusel/llm-batch) | Batch processing and checkpointing |

## License

MIT -- see [LICENSE](LICENSE).
