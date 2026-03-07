# AGENTS.md -- llm-embed

## Purpose
Single-header C++ text embeddings library. Calls OpenAI /v1/embeddings API
via libcurl, computes cosine/dot/euclidean similarity, and provides a flat
binary-file VectorStore for nearest-neighbor search.

## Architecture
```
llm-embed/
  include/llm_embed.hpp   <- THE ENTIRE LIBRARY. Do not split.
  examples/
    basic_embed.cpp
    vector_store.cpp
  CMakeLists.txt
```

## Build
```bash
cmake -B build && cmake --build build
```

## Rules
- Single header only.
- Only libcurl as external dep.
- All public API in namespace llm.
- Implementation inside #ifdef LLM_EMBED_IMPLEMENTATION guard.

## API Surface
- embed(), embed_batch() — OpenAI embedding API calls
- cosine_similarity(), dot_product(), euclidean_distance()
- VectorStore: add/remove/search/save/load — binary flat file
