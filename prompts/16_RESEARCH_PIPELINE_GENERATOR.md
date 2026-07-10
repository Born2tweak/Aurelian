# 16_RESEARCH_PIPELINE_GENERATOR -- Prompt For Generating A Complete Research Suite

Use this prompt when a model has only a project idea, an existing repository summary, or both, and must decide what research should happen before implementation begins.

```text
You are operating under Aurelian. Your job is to generate the research pipeline for a project before implementation begins.

Input:
- Project idea: [paste idea, product brief, feature request, or goal]
- Existing repository context: [paste repo link, tree, README, relevant docs, or "none"]
- Constraints: [stack, audience, timeline, budget, deployment, security, privacy, legal, design, accessibility, performance, data, AI/model constraints]
- Available tools/sources: [repo access, web, browser, docs, issue tracker, designs, datasets, domain experts, test/build commands]
- In scope: [what research may cover]
- Out of scope: [what not to research]

Objective:
Given only the project idea, existing repository, or both, determine the complete research suite needed before implementation. Do not implement. Do not answer the research questions. Generate the pipeline: what reports should exist, why they exist, who should produce them, dependencies between them, confidence, implementation impact, and optimal execution order.

Research categories to consider:
- domain knowledge
- technical architecture
- frontend
- backend
- AI/ML
- UX
- UI
- motion
- accessibility
- infrastructure
- DevOps
- testing
- security
- product strategy
- competitive analysis
- legal/privacy
- performance
- scientific validation
- datasets
- APIs
- open-source ecosystem
- resource atlas
- build-vs-buy

Operating rules:
1. First state the implementation decision the research must support.
2. Separate discovery from research. Discovery maps what exists; research answers what is unknown.
3. If repository/product context is too thin to scope research responsibly, make `docs/research/00_PROJECT_DISCOVERY.md` the first report and mark "additional discovery required first."
4. For each research category, classify it as needed, optional, or skip. Include the reason, implementation impact, and confidence.
5. Recommend only reports that feed real implementation decisions. Avoid ceremonial completeness.
6. Consider resource atlas and build-vs-buy before recommending custom implementation research.
7. Put security, privacy, legal, scientific, data, infrastructure, and irreversible architecture risks early when they are relevant.
8. Assign an appropriate specialist to every report.
9. Define dependencies between reports and ensure the graph is acyclic.
10. Give an optimal execution order and identify reports that can run in parallel.
11. Use confidence labels: high, medium, low.
12. Use implementation importance labels: critical, high, medium, low.
13. Use estimated effort labels: quick, moderate, deep.

Specialists you may assign:
- project analyst
- domain researcher
- architect
- frontend engineer
- backend engineer
- AI/ML engineer
- UX researcher
- UI/taste reviewer
- motion designer
- accessibility specialist
- infra/DevOps engineer
- test strategist
- security reviewer
- product strategist
- competitive researcher
- legal/privacy reviewer
- performance engineer
- data scientist
- API integration specialist
- open-source/resource researcher

For every recommended research document include exactly:
- filename
- category
- specialist
- purpose
- why it exists
- required inputs
- expected outputs
- downstream dependencies
- implementation importance
- confidence
- estimated effort
- whether additional discovery is required first

Use stable filenames under `docs/research/`, for example:
- `docs/research/00_PROJECT_DISCOVERY.md`
- `docs/research/01_DOMAIN_ONTOLOGY.md`
- `docs/research/02_PRODUCT_STRATEGY.md`
- `docs/research/03_COMPETITIVE_ANALYSIS.md`
- `docs/research/04_RESOURCE_ATLAS.md`
- `docs/research/05_BUILD_VS_BUY.md`
- `docs/research/06_TECHNICAL_ARCHITECTURE.md`
- `docs/research/07_API_INTEGRATION_RESEARCH.md`
- `docs/research/08_DATASET_RESEARCH.md`
- `docs/research/09_AI_ML_RESEARCH.md`
- `docs/research/10_UX_RESEARCH.md`
- `docs/research/11_UI_SYSTEM_RESEARCH.md`
- `docs/research/12_MOTION_INTERACTION_RESEARCH.md`
- `docs/research/13_ACCESSIBILITY_RESEARCH.md`
- `docs/research/14_BACKEND_RESEARCH.md`
- `docs/research/15_INFRA_DEVOPS_RESEARCH.md`
- `docs/research/16_SECURITY_PRIVACY_THREAT_MODEL.md`
- `docs/research/17_TESTING_STRATEGY.md`
- `docs/research/18_PERFORMANCE_RESEARCH.md`
- `docs/research/19_SCIENTIFIC_VALIDATION.md`

Output format:

Research Pipeline

Project understanding:
- Objective:
- Inputs available:
- Assumptions:
- Highest-risk unknowns:

Category triage:
- Category:
  Decision: needed | optional | skip
  Reason:
  Implementation impact: critical | high | medium | low
  Confidence: high | medium | low

Recommended research documents:
- Filename:
  Category:
  Specialist:
  Purpose:
  Why it exists:
  Required inputs:
  Expected outputs:
  Downstream dependencies:
  Implementation importance: critical | high | medium | low
  Confidence: high | medium | low
  Estimated effort: quick | moderate | deep
  Discovery required first: yes | no

Research Dependency Graph:
Write a readable text graph showing relationships between documents. Also include Mermaid if useful.

Research Execution Order:
1. filename
   Reason:
   Can run in parallel with:

Discovery gate:
- Discovery sufficient | Additional discovery required first | Blocked by user-only input
- Missing discovery, if any:

Implementation readiness:
- Not ready until:
- Earliest safe implementation milestone after research:
- Reports that can be skipped only if:

Quality check before finalizing:
- Every recommended report feeds a named implementation decision.
- Every skipped category has a reason.
- Every critical report has dependencies and expected outputs.
- The dependency graph is acyclic.
- Confidence is based on the available input, not on how polished the report sounds.
- No implementation work is proposed before prerequisite research or discovery.
```
