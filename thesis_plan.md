[200~Yes. This is a sensible base repo for your thesis, but you should treat it as **a platform to dissect first, then bend**, not as a finished thesis engine. The repository is 
publicly visible, is a **fork of HKUDS/LightRAG**, and still exposes the LightRAG structure with folders like `docs`, `examples`, `lightrag`, `scripts`, and `tests`. The README 
also shows that it already supports document insertion, multiple query modes, and Neo4j as a graph backend, which makes it a practical starting chassis for your direction. 
([GitHub][1]) Since your thesis idea is inspired by **Agentic-KGR’s philosophy** rather than its full RL machinery, your plan should be: **understand the existing GraphRAG 
pipeline, identify where graph construction happens, expose its weak points, and then add an iterative graph-refinement layer with explicit graph-quality evaluation**. The repo 
already gives you the mechanical bones: insertion pipeline, query pipeline, and Neo4j support. ([GitHub][1]) Here is a strong **10-phase thesis plan** built around that idea.
## Phase 1: Repository reconnaissance and architecture mapping
Goal: understand the repo before changing anything. What to do: * Clone the repo and run a full directory audit. * Identify what is unchanged from LightRAG and what has been 
customized for your thesis direction. * Read, in order: `README.md`, `examples/`, `tests/`, `lightrag/`, `scripts/`, and any config files. * Create a document called 
`repo_map.md` with:
  * main modules * data flow * entry points * storage backends * where extraction happens * where querying happens * where Neo4j is touched Deliverable: * one architecture 
diagram * one “what this repo already does vs what my thesis must add” note Why first: Because the repo is still fundamentally a LightRAG fork, so you need to separate inherited 
machinery from your contribution. ([GitHub][1])
## Phase 2: Build and run the baseline system unchanged
Goal: get the machine humming before opening the hood. What to do: * Set up the environment exactly as the repo expects. * Run one minimal example end to end. * Verify the basic 
lifecycle:
  * initialize * insert documents * query * inspect outputs * Record required environment variables, packages, and startup sequence. Important repo-grounded details: * The 
README shows a basic async initialization pattern with `initialize_storages()`. * It also shows simple insert and query usage. * By default, storage can persist under a working 
directory, while graph storage can be swapped later. ([GitHub][1]) Deliverable: * `baseline_run.md` * working script that ingests 2 to 5 small documents and answers a few 
questions
## Phase 3: Trace the end-to-end pipeline in code
Goal: go from “it runs” to “I know where every wire goes.” What to do: * Trace the flow for: * document input * chunking * extraction * graph creation * vector storage * 
  retrieval * answer generation
* Add comments or notes on which functions/classes control each step. * Create a “pipeline call graph” note. Focus files: * `lightrag/` core modules * insert pipeline * query 
pipeline * storage abstractions * Neo4j implementation Deliverable: * `pipeline_trace.md` * a table with: stage, file, class/function, role, thesis relevance This phase is where 
the fog stops cosplaying as architecture.
## Phase 4: Isolate graph construction logic
Goal: identify the exact components you will modify for thesis contribution. What to do: * Find how entities and relations are extracted during indexing. * Find how graph 
nodes/edges are represented before storage. * Determine whether extraction is prompt-based, rule-based, or hybrid. * Note what schema is implicit in the code. Questions to 
answer: * What becomes a node? * What becomes an edge? * What metadata survives? * Can you intercept and score extracted triples before they are saved? * Can you re-run graph 
construction for a document? Deliverable: * `graph_construction_audit.md` * a candidate list of insertion hooks for refinement This is the most important transition point, 
because your thesis contribution lives here, not merely in querying.
## Phase 5: Switch to a thesis-specific Neo4j graph design
Goal: move from generic LightRAG graphing to your research-paper KG. The repo already supports **Neo4j** by setting `graph_storage="Neo4JStorage"` and configuring Neo4j 
connection environment variables. ([GitHub][1]) What to do: * Define a minimal thesis graph schema for research papers. * Likely nodes:
  * `Paper` * `Author` * `Venue` * `Topic` or `Method` * optionally `Dataset`, `Task`, `Metric` * Likely relationships: * `AUTHORED` * `PUBLISHED_IN` * `USES_METHOD` * 
  `ADDRESSES_TASK` * `EVALUATED_ON` * `CITES` if available
Keep v1 lean. Do not build an ontology cathedral yet. Build a bicycle that rides. Deliverable: * `thesis_graph_schema.md` * sample Cypher queries * one small Neo4j population 
script or adapter
## Phase 6: Create the thesis dataset and benchmark set
Goal: build the experimental ground your thesis stands on. What to do: * Curate a manageable corpus of research papers. * Prepare clean document inputs: * metadata * abstract * 
  maybe introduction
* Create benchmark questions in categories: * factual graph lookup * multi-hop relation questions * paper comparison * method-task-dataset linkage * author/venue/topic 
  exploration
* Also define extraction evaluation samples: * gold entities * gold relations * graph sanity checks Deliverable: * `dataset_card.md` * `qa_benchmark.json` * 
`extraction_eval_set.json` Without this, your thesis risks becoming a demo with a necktie.
## Phase 7: Implement graph quality evaluation hooks
Goal: operationalize the Agentic-KGR philosophy without full RL. Your thesis idea says graph construction quality should be **explicitly modeled, evaluated, and iteratively 
refined**. This phase turns that from slogan into machinery. What to do: * Add graph quality checks after extraction and before or after Neo4j insertion. * Start with simple 
measurable signals:
  * malformed entities * duplicate entities * relation type validity * missing required node fields * disconnected fragments * unsupported edge patterns * entity normalization 
  consistency
* Optionally add LLM-based critique: * “Are these triples faithful to the source passage?” * “Which triples are uncertain?” * “Which entities should merge?” Deliverable: * 
`graph_quality_metrics.md` * scorer module * logs showing per-document graph quality signals This is where your thesis starts sounding like Agentic-KGR in spirit.
## Phase 8: Implement iterative refinement loop
Goal: move from one-shot extraction to graph improvement. What to do: * Build a lightweight refinement loop: 1. extract initial graph 2. evaluate graph quality 3. identify weak 
  nodes/edges 4. re-prompt extraction or correction 5. merge/update graph 6. store revision metadata
* Keep it simple for v1: * no RL required * prompt-based critique and repair is enough * Add provenance: * which document chunk created a triple * whether triple is original or 
  refined * confidence or quality score
Deliverable: * `iterative_refinement_design.md` * working refinement prototype on a small subset This phase is your main thesis differentiator.
## Phase 9: Integrate graph-grounded QA and Text2Cypher path
Goal: connect refined graph construction to downstream QA. Your repo title suggests a direction around **research paper knowledge graph construction and Text2Cypher-based QA 
using Neo4j**, so this phase should explicitly tie graph quality to answer quality. ([GitHub][1]) What to do: * Build or adapt a natural-language-to-Cypher pipeline for your 
schema. * Route questions into:
  * graph lookup / Cypher * hybrid graph + text retrieval * answer synthesis over retrieved graph facts * Compare outputs using: * baseline graph * refined graph Deliverable: * 
`text2cypher_benchmark.md` * evaluation script * examples of correct and failed Cypher generations This phase lets you test the central thesis claim: **better graph construction 
leads to better downstream QA**.
## Phase 10: Full evaluation, ablations, and thesis packaging
Goal: convert engineering into thesis evidence. What to evaluate: * Graph extraction quality * Graph validity / consistency * QA correctness * Text2Cypher correctness * effect 
of refinement loop Suggested comparisons: * baseline repo unchanged * repo + thesis schema only * repo + schema + quality scoring * repo + schema + iterative refinement 
Suggested ablations: * no refinement * only structural checks * only LLM critique * one refinement round vs multiple rounds Deliverable: * final experiment tables * error 
analysis * “limitations and future work” section * cleaned thesis branch in Git That final branch should clearly separate: * inherited LightRAG components * your modifications * 
your evaluation assets ---
## The clean thesis storyline behind these 10 phases
Your thesis can be framed as:
> Existing GraphRAG pipelines often treat graph construction as a one-pass preprocessing stage. This work argues that graph quality should be explicitly evaluated and 
> iteratively improved. Building on a LightRAG-based repository with Neo4j support, I adapt the system to research paper collections, introduce graph-quality assessment and 
> refinement loops, and evaluate whether better graph construction improves Text2Cypher and graph-grounded question answering.
That is crisp, defensible, and very supervisor-friendly.
## A practical execution order inside the 10 phases
If you want the shortest safe path: * First finish Phases 1 to 4 without changing much. * Then do 5 and 6 to lock schema and dataset. * Then build 7 and 8, because that is your 
actual contribution. * Then do 9 and 10 for evaluation.
## My recommendation
Do **not** begin by rewriting the whole repo. Begin by producing these four files first: * `repo_map.md` * `pipeline_trace.md` * `graph_construction_audit.md` * 
`thesis_graph_schema.md` Those four documents will save you from three weeks of noble confusion. I can turn this next into a **thesis-ready milestone plan with outputs, risks, 
and success criteria for each phase**. [1]: https://github.com/guptaaditya746/GraphRag_RL_db "GitHub - guptaaditya746/GraphRag_RL_db: Adaptive Research Paper Knowledge Graph 
Construction and Text2Cypher-Based Question Answering using Neo4j · GitHub"
