[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/-HC-VniT)

# Week 7: Moonlight Festival Control Booth

## Summary
This week's assignment implements a priority queue system for a festival control booth using Python's `heapq` module. The system manages festival alerts by urgency, supporting ordered processing, stable ordering, top-k retrieval, and non-destructive peeking.

---

## Functions Implemented

### `order_festival_alerts`
Returns alert titles sorted by priority (smallest number = most urgent). Uses `heapq.heapify` and `heapq.heappop` to process alerts in order.

- **Time complexity:** `O(n log n)` — heapify is `O(n)`, each pop is `O(log n)` for `n` items.

### `order_festival_alerts_stable`
Same as above but preserves original input order when two alerts share the same priority. Achieved by inserting the original index as a tiebreaker in the heap tuple `(priority, index, title)`.

- **Time complexity:** `O(n log n)`

### `top_k_festival_alerts`
Returns the titles of the `k` most urgent alerts. Returns an empty list if `k <= 0`, and returns as many as possible if `k` exceeds the number of alerts.

- **Time complexity:** `O(n + k log n)` — `O(n)` to heapify, `O(k log n)` for `k` pops.

### `peek_next_festival_alert`
Returns the title of the most urgent alert without modifying the original input. Makes a copy, heapifies it, and reads `heap[0]`. Returns `None` if the list is empty.

- **Time complexity:** `O(n)` for the heapify on the copy.

---

## Design Choices

- **`heapq` module:** Python's `heapq` implements a min-heap, meaning the smallest element is always at index 0. This maps directly to priority queues where lower numbers = higher urgency.
- **Stable ordering:** Python tuples are compared element by element, so inserting the original index as a middle element `(priority, index, title)` guarantees stable ordering without any extra logic.
- **Non-destructive peek:** Rather than popping from the original list, a copy is made and heapified. The minimum is then read directly from index 0 of the heap without popping.
- **Edge cases handled:**
  - Empty alert lists return `None` or `[]` as appropriate.
  - `k <= 0` returns an empty list immediately.
  - `k` larger than the number of alerts returns all available alerts.

---

## How to Run

```bash
python -m pytest -q
```

---

## Assistance & Sources

- AI used? **Y**
- What it helped with: Code structure and README formatting
- Non-course sources used: Python standard library documentation
- Links:
  - https://docs.python.org/3/library/heapq.html