# Caret-it Optimization

This bundle runs Caret-it through multiple rounds so the conversion model can be stress-tested instead of tuned once and frozen too early.

## Workflow

Read:

- `WORKFLOW.md`
- `round-1-summary.md`
- `round-2/README.md`
- `round-3/README.md`

## Overall Results

| Round | Skills | Original Tokens | Rewritten Tokens | Saved | Shorter |
| --- | --- | ---: | ---: | ---: | ---: |
| Round 1 | `memory`, `review`, `intake` | 2543 | 1594 | 949 | 37.3% |
| Round 2 | `coach`, `improve`, `priority` | 3170 | 1767 | 1403 | 44.3% |
| Round 3 | `queue-sync`, `caret-content`, `pattern-draft` | 2889 | 1438 | 1451 | 50.2% |
| **Total** | **9 skills** | **8602** | **4799** | **3803** | **44.2%** |

## Convergence Signal

Three things became clear:

1. Caret^ does not just help tiny operational skills. It also compresses large orchestration files well when schemas and payloads stay literal.
2. Multi-lens reasoning files are a strong fit because hats and scoped review phases map cleanly onto existing structure.
3. The biggest real boundary is stale canon. Some files need semantic normalization before they can be judged as clean Caret-it conversions.

## Current Best Model

The best current model is:

- use Caret^ for flow, gates, hats, routes, and repeated rule blocks
- keep payload schemas, sample templates, and concrete tables literal or plain
- treat stale notation semantics as a separate normalization step
- use adoption calls, not compression alone, to decide whether the rewrite should land
