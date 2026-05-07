# SolidSessionBench

This is the paper repository for **SolidSessionBench**, a benchmark that generates realistic query sequences for evaluating client-side query optimization in decentralized environments such as [Solid](https://solidproject.org/).

SolidSessionBench extends [SolidBench](https://github.com/SolidBench/SolidBench.js) to simulate three empirically grounded usage patterns, logical query sessions, user interest-based data locality, and iterative query refinement, that isolated single-query benchmarks fail to capture.
To demonstrate the benchmark's utility, the paper evaluates three baseline client-side HTTP caching strategies in [Link Traversal-based Query Processing (LTQP)](https://linkeddatafragments.org/in-depth/link-traversal/).

This repository serves as a central hub linking to the source code, experiment setups, and raw data associated with the paper.

---

## Reproducible Experiments

The experiments producing the paper's main results are available at:
> https://github.com/RubenEschauzier/experiments-link-traversal-caching

Each experiment lives on a dedicated branch with a self-contained README requiring minimal setup.

| Branch | Description |
|---|---|
| `experiment/cache` | **Unindexed Cache**: produces data for all three cache sizes |
| `experiment/query-cache` | **Indexed Cache**: produces data for all three cache sizes |
| `experiment/query-cache-estimate` | **Indexed Cache + Cardinality Estimation**: produces data for all three cache sizes |
| `experiment/synthetic-cache-hitrate` | Synthetic hit rate data for the **Unindexed Cache** |
| `experiment/synthetic-query-cache-hitrate` | Synthetic hit rate data for the **Indexed Cache** |

For the comparison experiments using **random query sequences** (Section 4.4 of the paper):
> https://github.com/RubenEschauzier/experiments-link-traversal-caching-random-query-sequences

These use the same three cache branches listed above (`experiment/cache`, `experiment/query-cache`, `experiment/query-cache-estimate`).

**Raw data** from all experiments is archived on Zenodo:
> https://zenodo.org/records/20056413

**Data processing and figure/table generation** is handled by:
> https://github.com/RubenEschauzier/process-raw-caching-jbr-output

---

## Benchmark Source Code

SolidSessionBench extends four components of the SolidBench ecosystem and is added to the [jbr.js](https://github.com/rubensworks/jbr.js) benchmark runner. The changes are integrated into the upstream repositories as new versions:

| Component | Description | Repository |
|---|---|---|
| **jbr.js** | A ready-to-use benchmark runner which handles the initializiation, generation, and running of SolidSessionBench | [jbr.js](https://github.com/rubensworks/jbr.js/tree/master/packages/experiment-solid-session-bench) |
| **SolidBench.js** | Centralized runner integrating all changes; includes sensible default configurations used throughout the paper | [SolidBench/SolidBench.js](https://github.com/SolidBench/SolidBench.js) |
| **sparql-query-parameter-instantiator** | Main updated codebase; implements the correlated query sequence generation logic (logical sessions, interest-based instantiation, and refinement patterns) | [SolidBench/sparql-query-parameter-instantiator.js#query-sequence-instantiator](https://github.com/SolidBench/sparql-query-parameter-instantiator.js#query-sequence-instantiator) |
| **ldbc-snb-enhancer** | Updated to compute and export interest-based similarity scores between users and their posts, enabling realistic data locality in generated sequences | [SolidBench/ldbc-snb-enhancer.js#similarity-configuration](https://github.com/SolidBench/ldbc-snb-enhancer.js#similarity-configuration) |
| **rdf-dataset-fragmenter** | Updated to output both original and transformed terms within a quad, enabling fragmented query strings to be mapped back to executable queries over the original SNB dataset | [SolidBench/rdf-dataset-fragmenter.js#transform-callbacks](https://github.com/SolidBench/rdf-dataset-fragmenter.js#transform-callbacks) |

---

## Caching Implementation

The three caching strategies evaluated in the paper are implemented in a fork of the Comunica LTQP engine:

- **Feature branch:** https://github.com/RubenEschauzier/comunica-feature-link-traversal/tree/feature/http-caching-adaptive-join
- **Updated Comunica core:** https://github.com/RubenEschauzier/comunica/tree/feature/caching-adaptive-join

To run these locally, follow the [official Comunica documentation on linking a local version](https://comunica.dev/docs/modify/advanced/linking_local_version/#yarn-workspaces).

The Docker image used in all experiments:
```
rubeneschauzier/comunica-feature-link-traversal-caching:dev
```
Index digest of the exact experiment version:
```
sha256:9cacaab6409ec5abd289675ff5db83b08508cfc407c51bac4ef8de2b2bb711c8
```
