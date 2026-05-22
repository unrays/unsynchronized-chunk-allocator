# Unsynchronized Chunk Allocator

This project is part of the **EXOTIC::memory** library.

## Overview

This project started as a technical challenge I set for myself within the scope of a compiler-related work.

It required a solid understanding of allocators, as they form the foundation of precise lifetime management and efficient data structures in low-level systems.

To approach this, I studied the design of `std::pmr` and related allocator models, taking notes and extracting the core ideas that I found most relevant.

It took me around three weeks to arrive at a functional implementation.

This is not a simple copy of an existing allocator from the internet. While I drew inspiration from established standards and allocator design principles, I implemented the system in a very educational and deliberate way, focusing on clarity and understanding.

I’m genuinely proud of this work, and it will be used as part of a compiler project where it fulfills its original goal.

---

## Purpose

- Explore low-level memory management concepts
- Understand allocator design and lifetime control
- Build a foundation for compiler-related systems

---

## Example Usage

```cpp
// In this case, we use a monotonic atomic buffer as the memory backend
exotic::memory::monotonic_atomic_buffer upstream(1 << 20);

exotic::memory::unsynchronized_chunk_allocator<int> allocator(&upstream);

// Allocate raw memory for 10 ints
int* data = allocator.allocate(10);

// Construct objects in-place
allocator.construct(data, 42);

// High-level allocation helper
auto* obj = allocator.new_object<int>(123);

// Destroy (no-op deallocation model)
allocator.destroy(obj);
```

---

## Notes

This project is intentionally minimal in scope and focused on learning and system-level understanding rather than being a production-ready general-purpose allocator. Also, the very library-like aspect with `exotic::memory` is simply because it looks more professional :)

## License

This project is licensed under the Boost Software License. See the [LICENSE](LICENSE) file for details.

<p align="center"><sub>© Félix-Olivier Dumas 2026</sub></p>
