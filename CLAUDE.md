# CLAUDE.md -- llm-embed

## Build
```bash
cmake -B build && cmake --build build
```

## THE ONE RULE: SINGLE HEADER
`include/llm_embed.hpp` is the entire library. Never split it.

## API Surface
```cpp
namespace llm {
    using Embedding = std::vector<float>;
    struct EmbedConfig { api_key, model, dimensions };
    Embedding embed(text, config);
    std::vector<Embedding> embed_batch(texts, config);
    float cosine_similarity(a, b);
    float dot_product(a, b);
    float euclidean_distance(a, b);
    class VectorStore {
        VectorStore(filepath);
        void add(id, text, embedding, metadata);
        void remove(id);
        std::vector<SearchResult> search(query, top_k);
        void save(); void load();
        size_t size() const;
    };
}
```

## Notes
- VectorStore format: binary (not JSONL) — faster for large stores
- Embeddings are stored as float arrays
- search() uses cosine_similarity, sorts descending
