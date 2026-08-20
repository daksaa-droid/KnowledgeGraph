# KnowledgeGraph
Summary of analysis done till date.

# Knowledge Graphs: What to Build, and How Much to Spend

### Where graphs earn their place in a reporting-led data landscape, and how to size the investment

---

## 1. The questions worth answering

Most writing on knowledge graphs argues about whether the technology is good. That is the wrong argument. Graph databases work, ontologies are a sound modelling discipline, and GraphRAG solves a real problem. None of that settles the decision an organisation actually faces, which is narrower:

1. Should a knowledge graph be built out at all?
2. If yes, how much, and at what point does the spend stop?
3. Is a graph the right thing to build, and is it the only thing that needs building?

The short answers, stated up front so the rest can be checked against them:

**A graph supplements a data landscape. It cannot be the core that solves its data problems.** That holds for any landscape whose primary job is reporting and governed metrics. It does not hold universally, and section 4 marks the exception.

**A graph is one component of about six, and it is not the first one.** Built before the others, it produces an accurate map of a landscape nobody has agreed on.

**A meaningful part of what a graph needs cannot be harvested at all.** Section 10 lists what has to be asserted by people first. That work is neither optional nor automatable.

**The right initial investment is small and evidence-gated.** Section 11 proposes a staged shape with explicit stop conditions, rather than a programme budget agreed once and defended afterwards.

There is a lot of marketing in this space at the moment, and much of it aims at the gap between what a graph demonstrably does and what "solving your data problems" is taken to mean. Most of what follows is about that gap.

---

## 2. Three different things are called "knowledge graph"

| Layer | What it actually is | How contested it is |
|---|---|---|
| Graph database | A storage and traversal engine (Neo4j, TigerGraph, Neptune) | Specialised. Narrow economics. |
| Ontology / semantic model | Entity types, relationships, business meaning. Can be persisted as RDF, as Delta tables, or in a catalog | Broadly valuable. Almost uncontroversial. |
| Graph-shaped application | GraphRAG, lineage explorers, entity resolution, network risk | Depends entirely on the use case |

Most "the graph will unify your data" arguments borrow their credibility from the second row and end up funding the first. An ontology is a modelling discipline, and it can be held without running a graph engine. Conversely, a graph engine delivers nothing if nobody has agreed what a customer is.

Separating these three is the single most useful thing to do before a funding conversation, because the cost, the risk and the payback are different for each.

---

## 3. What a graph does not solve

"Solving our data problems" usually means some mix of the following. A graph touches none of them directly:

- Data quality. A graph will faithfully record the relationships between bad tables.
- Ownership. Nobody becomes accountable because an edge points at their name.
- Duplicate pipelines and duplicate logic. A graph can make duplication visible, which is genuinely useful, but visibility is not removal.
- Cost. A second store adds cost. It does not reduce the first one.
- Trust in numbers. Trust comes from certified definitions and a change process.
- People exporting to spreadsheets and working from there. Unaffected.

What a graph does solve is narrower: relationship discovery, traversal at unknown depth, identity resolution, and supplying structured context to an AI system. Those are real problems and worth money. They are not the problems that usually motivate the programme.

Where the list above is the actual pain, the investment belongs elsewhere first, and the graph question can wait a quarter without loss.

---

## 4. The workload split: BI, ML and AI pull in different directions

A typical product-company estate is mostly BI, with some machine learning and some AI. These three are usually discussed together and should not be.

**BI.** Settled, and not close. Predictable aggregation over a known schema. Columnar engines and a governed semantic layer win on performance, on auditability and on operational maturity. No graph investment is justified by BI alone.

**ML.** Mostly argues against the graph. Training wants a wide, flat feature table. Graph-derived features pay off only when the relationship itself is predictive: fraud rings, recommendation, network-driven churn, risk propagation through a supply chain. For forecasting, propensity, demand planning and ordinary product analytics, tabular features dominate and a graph adds a pipeline for no measurable lift. Unless the ML roadmap contains the first kind, this is a second argument for keeping spend low.

**AI.** The only genuine pull, and it splits in two:

- *Questions over existing metrics and dashboards.* This points at a semantic layer plus text-to-SQL. A graph is the wrong tool here, and worse, it invites the model to compute figures that should come from a governed definition.
- *Reasoning across documents, policies, entities and systems where the connections carry the meaning.* This is where a graph earns its cost. Even then it is scoped to the use case and sized to the entities involved, not built organisation-wide first.

**The question to settle before funding anything** is which of those two the AI work actually is. If it is the first, the problem is a metrics problem rather than a graph problem, and the graph conversation is a distraction from it.

**The exception to the thesis.** For a fraud unit, an AML function, or a business whose product is supply chain risk, the graph genuinely is the core system and reporting is peripheral. That is not the shape of a reporting-led estate, but the claim in section 1 should always be stated with the qualifier attached, or a single counter-example will be used to dismiss it.

---

## 5. Where the tabular model stays undefeated

**Aggregation economics.** Summing 50 million rows of revenue in a columnar engine is a compressed, vectorised scan over a contiguous column. The same operation in a graph is pointer chasing across nodes. Different physics, and the gap is orders of magnitude.

**Determinism and audit.** Net profit must compile identically on every run, versioned and reviewable. Schema flexibility makes definition drift cheap, and cheap drift is a defect in regulated reporting.

**The flattening tax.** BI tools consume rows and columns. Anything a graph returns must be flattened before it reaches a chart, and once flattened what remains is a table with an extra hop in front of it.

**Operational surface.** Incremental refresh, partitioning, row and column level security, workload management, cost attribution, result caching. Warehouses have all of this and it is boring and mature. The gap shows up in year two, not in the pilot.

**In fairness.** "Tables cannot do relationships" is as wrong as "graphs cannot do maths". Recursive CTEs handle moderate hierarchies well, and Spark GraphFrames handles batch graph analytics at scale. The question is cost at a given shape and depth, never capability in the abstract.

---

## 6. The cleaner alternative: a common data model

Before asking what a graph adds, the fair comparison is not the graph against the existing mess. It is the graph against the cheapest thing that would also fix the mess.

**The alternative.** If the goal is one agreed definition of net revenue, a common data model plus certified metric views delivers exactly that with fewer moving parts. One technology, one query language, an artifact BI tools consume natively, no synchronisation problem. A graph adds a second store, a second skillset and a copy of the truth that can drift from the first. On the main question, which is trustworthy numbers, the common data model wins outright.

Three things follow.

*They are not competitors at the same point in the lifecycle.* The metric view is the published artifact. A graph is the working store used to reach agreement across an estate that does not have one yet. Once a metric is certified, its definition belongs in the metric view and the graph's job for it is finished. Anything held in the graph after that point needs a separate justification.

*A common data model encodes a decided state, not a contested one.* During harvesting there are three candidate definitions of net revenue in play, each with a source, a confidence score, an owner and no certification. That state has to be queryable while it is resolved, and a metric view has nowhere to put it. This is scaffolding, and scaffolding is legitimate as long as it is recognised as temporary.

*A common data model assumes agreement is reachable up front.* Where it is, build it and skip the graph entirely. The failure mode of a common data model at scale is not technical: it becomes either rigid, so teams override it silently, or a lowest common denominator nobody uses. That is a governance failure, and a graph does not fix governance failures. It only makes the disagreement visible.

**One concession worth making openly.** A graph model does not require a graph database. If traversal is a small share of the workload, the same relationships can be held as relational metadata with a traversal helper, which removes a system from the estate. This is not a theoretical position: DataHub treats its graph layer as pluggable and can serve relationship queries from a search index rather than a graph database [2]. Choosing a graph engine should be a decision about query shape and volume, and the burden of proof sits with the graph.

Two workloads survive this comparison, and they set up the next section.

---

## 7. What survives: where graphs genuinely win

The two that resist a relational model outright:

**1. Join path inference.** Finding a valid path between tables nobody modelled together is graph search. A common data model has these paths by construction, but only for the tables already inside it, and the hard cases are the ones outside.

**2. Impact analysis at unbounded depth.** Recursive SQL works and then degrades, and becomes unpleasant to maintain long before it becomes slow.

The rest are worth having, but each is defensible on its own use case rather than as a platform:

**3. AI grounding.** Explicit meaning an assistant can traverse instead of inventing: product A is a sub-component of system Y, which is governed by policy Z.

**4. Identity resolution.** The same entity under different keys across CRM, ERP and support logs, modelled as candidates around a canonical node with match confidence on the edge.

**5. Deep supply chain and bill-of-materials traversal.** Which finished goods and open orders are exposed if a tier-3 supplier stops shipping. Depth is unknown, so a fixed set of joins cannot express it.

**6. Variable-depth master data.** Legal entities, org structures, chart-of-accounts mappings, product hierarchies ten levels deep in one market and three in another.

**7. Entitlement and policy propagation.** Who inherits access to what, through which group, via which role, with which exception.

**8. Network risk.** Fraud rings, shared attributes, indirect connections. The pattern is the answer, not the total.

The common signature: unknown depth at design time, sparse and heterogeneous relationships, new relationship types arriving faster than a modelling cycle, and an answer that is a path or a context payload rather than a measure.

### Two documented cases

**LinkedIn's metadata platform.** LinkedIn published an account of three generations of its data catalog architecture, running from WhereHows to DataHub [1]. The graph does not appear at the start. In the first-generation design the primary store is relational with a search index beside it, and a graph index is introduced only once recursive queries exceed what the relational store handles comfortably. In the current architecture the metadata change log sits at the centre, and the search and graph indexes are materialised from it, so either can be rebuilt deterministically after an inconsistency. The graph is a derived index rather than the system of record. The implementation keeps that layer pluggable, and relationship queries can be served from an Elasticsearch index instead of a graph database [2].

Two further points come from the same source. Core entity types have to be governed and agreed before they enter the graph, which is the assertion problem of section 10 stated by a team that hit it. And the closing observation is that putting metadata to work is harder than just putting metadata together, with a trusted knowledge graph positioned as a later stage that follows a reliable inventory rather than substituting for one.

**AstraZeneca's BIKG.** The Biological Insights Knowledge Graph integrates public, licensed and internal sources into a graph used for target identification and drug repurposing, reported at 55 sources, roughly 14 million entities and 136 million edges [3][4]. Two things are worth taking from it. It was built for a discovery and machine learning workload, alongside existing systems rather than in place of them. And its authors are explicit that building a graph to feed machine learning carries different requirements from building one for cross-source querying, since a highly granular model can obscure the relations an algorithm needs when they sit several hops apart. Even inside a single organisation, the graph is designed to a workload rather than as a universal layer, which is section 4's argument from the other direction.

---

## 8. A test to apply per workload

1. Is the depth of the relationship unknown at design time?
2. Does the answer change if the path changes, not just the total?
3. Are the entities heterogeneous and sparsely connected?
4. Do new relationship types appear faster than a schema change can ship?
5. Is the deliverable a path, a network, or context for an agent, rather than a measure?

Mostly yes points to a graph, for that workload only. Mostly no points to a governed semantic layer, and no amount of ontology changes that.

---

## 9. Is a graph the only thing? The dependency stack

No, and the ordering matters more than the list.

1. **Agreed definitions and named owners.** Organisational, not technical. Without this, nothing below pays back.
2. **Certified semantic layer or metric views.** The artifact BI tools and AI agents both consume.
3. **Catalog and ownership metadata.** Discovery, and knowing who to ask.
4. **Relationship metadata.** Join paths, lineage, metric-to-table mapping. Relational first.
5. **Graph engine.** Only if item 4 demonstrates traversal demand that relational storage handles badly.
6. **Retrieval layer for AI.** A separate concern, dependent on items 1 and 2 rather than on 5.

The graph is item 5 of 6, and every item above it is a prerequisite rather than a nice-to-have. That is the answer to whether a graph is the right thing to build: it is *a* right thing, positioned fifth. Funding it first buys an accurate map of a landscape nobody agrees on, which is a real artifact and not a solution.

**The counterweight, stated fairly.** Doing nothing does not hold the position either. AI work proceeds regardless, ungrounded, and each team builds its own mapping. One small, deliberately scoped graph is cheaper than five shadow ones, and that is the honest case for spending something rather than nothing.

---

## 10. What cannot be harvested, and must exist first

Harvesting is the strongest argument for building a graph: point tooling at query history, catalog lineage, notebooks and BI models, and the relationships fall out. That works, and it is why a graph can be stood up quickly. It also has a hard boundary that is usually discovered late.

**Harvesting produces observations. It cannot produce assertions.** Query history shows which joins were written, including the wrong ones, and frequency is not validity. Code shows which filters exist, not why. Neither yields a decision, and the following are all decisions:

- **Ownership.** Who is accountable for a definition, and who signs off a change to it. The commit author is not the owner. No system records this truthfully because no system is asked to.
- **Which candidate is correct.** Harvesting returns three definitions of net revenue with confidence scores. Confidence measures agreement between sources, not correctness, and the most frequently used definition is often the most frequently copied one.
- **Business intent behind logic.** That a filter excludes a region is observable. That it excludes intercompany transfers under a finance policy is not, and that is the part determining whether the definition can be reused anywhere else.
- **Conformed keys and shared vocabulary.** That `customer_id` in one system and `party_no` in another denote the same real-world thing is an assertion. Entity resolution proposes it. Somebody has to decide it, and own the consequences when it is wrong.
- **Join validity and grain.** Two columns matching on values is not evidence that joining them is meaningful, or that the result sits at a grain anyone should aggregate.
- **Sensitivity and policy classification.** Inferable at low accuracy, and low accuracy on this class of metadata is worse than none.
- **Lifecycle state.** Which of forty overlapping datasets is dead, which is authoritative, which is an abandoned experiment. Usage decay hints at it and does not settle it.

**Why this matters for sequencing.** Harvesting amplifies whatever seed of asserted truth already exists. With a good seed it is genuinely powerful, because a small set of certified definitions and conformed keys lets the tooling classify everything it finds against something. With no seed it amplifies noise, and produces a large, well-connected, confidently wrong graph. That failure is expensive precisely because it looks like progress.

**What the seed has to contain, at minimum:**

- A short list of certified metric definitions with named owners. Twenty is enough to start. Two hundred is a programme in its own right and not a prerequisite.
- The conformed keys that cross system boundaries, with a decision recorded on each.
- A shared vocabulary for the handful of entities more than one team uses.
- A change process naming who approves a redefinition and how consumers are told.

None of that is graph work, none of it is automatable, and all of it is useful whether or not a graph is ever built. It is also the slowest part, because it is people agreeing rather than tooling running, which is the real reason it gets skipped in favour of harvesting.

This is not a fringe position. LinkedIn's own account of building DataHub notes that core entity types must be governed and agreed before entering the graph, and closes on the point that putting metadata to work is harder than assembling it in one place, with the trusted knowledge graph treated as a stage that comes after a reliable inventory [1].

**The practical rule:** if the owner of a metric cannot be named today, a graph will not reveal who it is. It will only record that nobody knows, in more detail.

---

## 11. How much to invest: staged funding with stop conditions

Fund stages, not a programme. Each stage carries an exit question, and the answer decides whether the next is released.

**Stage 0. Use what already exists. Weeks, near-zero cost.**
Catalog lineage, BI tool lineage, information schema, query history. Exit question: is the missing thing relationship data, or agreement? Most estates find the second, in which case the money goes to items 1 and 2 of the stack and the graph question defers a quarter with nothing lost.

**Stage 1. The seed, plus relationship metadata as tables. One to two people, one quarter.**
The asserted minimum from section 10, held alongside harvested join paths, metric-to-table mapping, ownership and lineage in the lakehouse. No graph database. Exit question: which real queries did this fail to answer at acceptable cost, and how often were they asked? Log them. That log is the entire business case for stage 2, and if it stays short, stop here permanently. Stopping here is a successful outcome, not a failed programme.

**Stage 2. Graph engine, metadata grain only, one named use case. Funded only against the stage 1 log.**
Sized to metadata, reference and master data. Not instance data. Exit question: is the use case in production and used weekly by a named team?

**Stage 3. Second domain, shared vocabulary, cross-domain entities.**
Released only when two or more domains have independently asked for the same entity. Never in anticipation.

**Rough shape of the spend.** Given ten units of budget for fixing data, something close to four belongs with definitions, ownership and process, three with the semantic layer, two with relationship metadata, and one with the graph. The graph share should be the last funded and the first cut. If it is the largest line in a proposal, the proposal is describing a different problem.

**Stop conditions are worth writing down at the start**, because they are impossible to agree later: the graph duplicates data the semantic layer already governs; nobody outside the platform team has queried it in a month; the ontology has grown faster than the systems it describes; the traversal log from stage 1 stayed short.

---

## 12. What this means in a Power BI and spreadsheet estate

**Reporting tools should never query the graph.** The useful patterns sit upstream:

- **Generating the semantic model.** Certified definitions and validated join paths compile out to TMDL or metric views. Highest-value use in a BI-led estate, because the output is something the tool already understands.
- **Materialising variable-depth hierarchies.** The graph does the recursion once, in batch, and publishes a bridge table. The report consumes an ordinary dimension.
- **Cross-workspace impact analysis.** Power BI lineage stops at the workspace boundary. A graph spans source table to dataset to report to measure.
- **Duplicate metric detection.** Forty datasets each defining net revenue slightly differently is a canonicalisation problem, and canonicalisation needs the relationships.

**On the value of lineage, be sceptical.** It has almost no audience among report consumers. Its users are engineers, stewards and a platform migration. During a migration the value is concrete and measurable, and it also expires when the migration does, so it belongs in a programme budget rather than a permanent capability.

**Spreadsheets break the chain.** Once someone exports, lineage ends at the download. In an estate that runs on exports, effort spent tracing downstream is largely wasted, and the money is in getting the definition right in the model so the number was correct when it left.

**Lineage with no process attached is a diagram.** If nobody is obliged to act on an impact report before shipping a schema change, nothing about behaviour changes.

---

## 13. Scope: how much of an organisation belongs in the graph

The instinct that an organisation-wide graph holds too much is right, but the problem is grain rather than breadth.

**Fix the grain first.** Metadata, reference data and master data belong in the graph. Instance data does not. Transactions and customer rows stay in the lakehouse. Get this wrong and the graph is unusable at any scope. Get it right and an enterprise-wide graph stays surprisingly small.

**Harvest most of it, assert the rest.** Define centrally only the shared vocabulary and conformed keys from section 10, which is a short list. Everything else emerges from what individual teams publish. The distinction is not central versus local, it is decided versus observed.

**Use a promotion test.** An entity earns enterprise scope when two or more teams need to join on it, or when a regulator asks about it. Otherwise it stays local and nobody else carries the cost of understanding it.

**The common failure** is defining enterprise concepts before anyone has published anything, producing an ontology that is complete, agreed by committee, and describes no system that exists.

---

## 14. The architecture that holds

Beside the warehouse, not on top of it.

- **Lakehouse.** Facts, dimensions, governed calculations, the physical truth.
- **Semantic layer.** One definition per metric, versioned and certified, exposed to BI tools and agents through the same contract.
- **Knowledge graph.** Entities, relationships, ontology, lineage, provenance, identity resolution, context for agents.
- **Shared spine.** Conformed keys and shared vocabulary, so both refer to the same things.

One rule matters more than the rest. **When an agent needs a number, it calls the semantic layer, not the graph.** The graph supplies context, constraint and provenance. The metric comes from the governed model. Blur that and the result is a confidently wrong figure with a citation attached, which is worse than no figure.

---

## 15. Questions worth asking before funding a build

- What in this proposal could not be done with relational metadata and certified metric views?
- Which named team asks a traversal question today, how often, and what do they do instead now?
- What is the grain? If the answer includes transactions, the scope is wrong.
- Which facts here are harvested and which are asserted, and who asserted them?
- Can the owner of the top twenty metrics be named today? If not, what is the graph organising?
- What is the cost of the second copy, including reconciliation and the people maintaining both?
- What does success look like in one quarter, and what result would justify stopping?
- If this is for AI, is the AI answering questions about metrics or reasoning over entities? The first needs a semantic layer, not this.

---

## 16. Bottom line

A knowledge graph supplements a data landscape. In a landscape whose primary job is reporting and governed metrics, it cannot be the core that solves the data problems, because that core is not a storage technology at all. It is agreed definitions, named owners and a process that obliges people to use them. A graph sits downstream of that, and so does a common data model, and so does a metric view.

The harvesting argument does not change this. Harvesting produces observations, and the decisions that make observations useful, ownership, correctness, conformed keys, intent, are not sitting in any system waiting to be extracted. They have to be made, and they are the slow part.

Invest, but small and staged. Create the seed. Hold relationship metadata in tables with no new engine. Let a log of real, expensive traversal queries decide whether a graph database gets funded at all, and treat stopping at that point as a good outcome rather than a failure.

What justifies permanent spend is short: join path inference across an unmodelled estate, impact analysis at unbounded depth, identity resolution, and structured context for AI that reasons over entities rather than metrics. Anything longer than that list belongs to someone else's roadmap.

Most failed graph programmes did not fail on technology. They were scoped as the core, discovered eighteen months in that reporting still ran on the old model, and could not answer what the second copy of the data was for.

---

## References

[1] Das, S. "DataHub: Popular metadata architectures explained." LinkedIn Engineering, December 2020. https://engineering.linkedin.com/blog/2020/datahub-popular-metadata-architectures-explained

[2] DataHub storage layer documentation, covering the relational entity store as source of truth and the pluggable graph layer served by Neo4j or Elasticsearch. https://deepwiki.com/datahub-project/datahub/2.4-storage-layer

[3] Geleta, D. et al. "Biological Insights Knowledge Graph: an integrated knowledge graph to support drug development." bioRxiv, November 2021. https://www.biorxiv.org/content/10.1101/2021.10.28.466262v1.full

[4] Middleton, L. et al. "Phenome-wide identification of therapeutic genetic targets, leveraging knowledge graphs, graph neural networks, and UK Biobank data." Science Advances, 2024. https://www.science.org/doi/10.1126/sciadv.adj1424

