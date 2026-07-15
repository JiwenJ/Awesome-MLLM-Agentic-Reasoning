# Awesome MLLM Agentic Reasoning, Thinking with Images, and Agentic Generation

> A curated, time-bounded reading list on multimodal agents that **reason with actions**, **learn agentic policies**, **actively inspect video and images**, **use or create visual thoughts**, and **plan–generate–evaluate–refine visual content**.

**Coverage window:** 2025-07-14 to 2026-07-14 (inclusive, based on the first public arXiv version unless noted)  
**Last updated:** 2026-07-15 · **238 papers**

## Contents

- [Scope](#scope)
- [How the areas relate](#how-the-areas-relate)
- [Research threads at a glance](#research-threads-at-a-glance)
- [Agentic post-training and inference](#agentic-post-training-and-inference)
- [Agentic video reasoning](#agentic-video-reasoning)
- [Reliable reasoning](#reliable-reasoning)
- [Tag legend](#tag-legend)
- [Paper timeline](#paper-timeline)
- [Selection notes](#selection-notes)
- [Contributing](#contributing)

## Scope

This list tracks five tightly connected research directions:

1. **MLLM agentic reasoning** — a multimodal model actively plans, searches, uses tools, gathers evidence, verifies, or acts in an environment as part of reasoning.
2. **Thinking with images** — visual information is an intermediate reasoning state rather than only a fixed input. The visual state may come from external tools, code-based manipulation, generated pixels/video, retrieval, or an internal visual latent.
3. **Agentic visual generation** — an agent plans, orchestrates, evaluates, repairs, or learns from feedback around image/video generation; this also includes video/world models used as an agent's simulator or imagination module.
4. **Agentic post-training** — SFT, RL, preference optimization, process rewards, or verifier training explicitly optimize a multimodal model's multi-turn policy for tool use, search, active perception, memory, reflection, or action.
5. **Agentic video reasoning** — an agent decides which frames, clips, views, modalities, memories, or external sources to inspect and iteratively gathers or verifies temporal evidence.

The list excludes ordinary multimodal chain-of-thought, single-pass text-to-image/video generation, and papers where “multi-agent” only describes the generated scene rather than the generation or reasoning process.

## How the areas relate

```mermaid
flowchart LR
    AR["Agentic reasoning<br/>plan · act · observe · verify"]
    TWI["Thinking with images<br/>visual states inside the reasoning loop"]
    AG["Agentic generation<br/>plan · generate · critique · refine"]
    VID["Agentic video reasoning<br/>seek · remember · verify"]
    POST["Agentic post-training<br/>SFT · RL · process rewards"]
    WM["Video / world models<br/>predictive visual imagination"]

    AR -->|"invokes crop, zoom, search, code, segmentation"| TWI
    TWI -->|"creates sketches, images, frames, or latent visuals"| AG
    AG -->|"visual feedback becomes new evidence"| AR
    VID -->|"temporal evidence and memory"| AR
    POST -->|"optimizes the interaction policy"| AR
    AR -->|"selects frames, clips, views, and tools"| VID
    WM -->|"simulates consequences"| AR
    AR -->|"chooses actions and queries"| WM
```

An autonomy-oriented view of **thinking with images** is useful for reading the timeline:

`external visual tools → programmatic visual manipulation → generated visual thoughts → latent/internal visual thoughts`

## Research threads at a glance

These are representative paths through the timeline, not separate rankings:

- **Tool-integrated reasoning:** WebWatcher → DeepEyesV2 → VISTA-R1 → Vision-DeepResearch → OpenSearch-VL → AXPO / MetaForge → Visual-Seeker.
- **Agentic post-training:** WebWatcher / VISTA-R1 → Agent0-VL / VITAL → AdaTooler-V / InSight-o3 → VSearcher / ToolsRL → TAPO / ReGRPO → SearchEyes / UNIBROWSE.
- **Inference-time agency:** Simple o3 → Octopus / ToolScope → TTSP / SpecEyes / SPARC → CVSearch / Pixel-Searcher → PixelEyes.
- **Agentic video reasoning:** StreamAgent / VITAL → CAViAR / AVI → AVP / VideoARM → EGAgent / Weaver → VideoHV-Agent / LensWalk → InternVideo3 / VideoSearcher / VSeek.
- **Computer use and embodied action:** CoAct-1 → OpenCUA → ComputerRL → UI-TARS-2 → UltraCUA → Kimi K2.5; ThinkAct → PhysicalAgent → VLA-Thinker → AgentVLN → VLAs-as-Tools.
- **Thinking-with-images autonomy:** SIFThinker / Simple o3 → Thyme / CodePlot-CoT → MathCanvas / V-Thinker → CoVT / Monet → LanteRn / DeepLatent → Beyond the Eye.
- **Agentic image generation:** Talk2Image / Maestro → ImAgent / MIRA → GenAgent → GEMS / Gen-Searcher → SCOPE / Generation Navigator / InterleaveThinker → Qwen-Image-Agent / CanvasAgent.
- **Agentic video generation and world models:** MAViS → VISTA → Hollywood Town / CoAgent → SPIRAL → Agentic Video Generation → ViMax / VideoAgent.

## Agentic post-training and inference

`POST` and `INF` separate **how an agentic capability is acquired** from papers whose **main contribution is test-time control**. They may overlap when a work both trains the policy and introduces a substantive inference loop; routine execution of an otherwise standard learned policy does not qualify by itself.

| Track | Inclusion rule | Representative papers |
|---|---|---|
| Agentic post-training | The training target is a multi-turn interaction policy, tool/search decision, process reward, verifier, or reflective correction—not ordinary answer-only multimodal RL. | [VISTA-R1](https://arxiv.org/abs/2511.19773) · [Agent0-VL](https://arxiv.org/abs/2511.19900) · [VITAL](https://arxiv.org/abs/2508.04416) · [AdaTooler-V](https://arxiv.org/abs/2512.16918) · [InSight-o3](https://arxiv.org/abs/2512.18745) · [VSearcher](https://arxiv.org/abs/2603.02795) · [ToolsRL](https://arxiv.org/abs/2604.19945) · [TAPO](https://arxiv.org/abs/2606.05784) · [ReGRPO](https://arxiv.org/abs/2606.31392) |
| Agentic inference | The main method introduces active evidence seeking, tool orchestration, test-time scaling, speculative execution, adaptive compute allocation, uncertainty control, verification, or stopping; merely running a standard learned policy is insufficient. | [Simple o3](https://arxiv.org/abs/2508.12109) · [ToolScope](https://arxiv.org/abs/2510.27363) · [Test-time Scaling over Perception](https://arxiv.org/abs/2604.11025) · [SpecEyes](https://arxiv.org/abs/2603.23483) · [SPARC](https://arxiv.org/abs/2602.06566) · [CVSearch](https://arxiv.org/abs/2605.23655) · [PixelEyes](https://arxiv.org/abs/2607.00115) |
| Process and reward reliability | Rewards or critics judge intermediate evidence, tool inputs/outputs, action utility, efficiency, or correction quality rather than only the final answer. | [Deep But Reliable](https://arxiv.org/abs/2512.17306) · [CodeV](https://arxiv.org/abs/2511.19661) · [ARM-Thinker](https://arxiv.org/abs/2512.05111) · [GTR-Turbo](https://arxiv.org/abs/2512.13043) · [ProMMSearchAgent](https://arxiv.org/abs/2604.20486) · [Diversity Over Frequency](https://arxiv.org/abs/2606.00096) |
| Agentic-process evaluation | The benchmark or diagnostic tests whether tools, visual evidence, search, and stopping decisions causally help rather than merely appearing in a trace. | [VisualToolBench](https://arxiv.org/abs/2510.12712) · [Agentic-MME](https://arxiv.org/abs/2604.03016) · [VisualNeedle](https://arxiv.org/abs/2605.26380) · [Do Multimodal Agents Really Benefit from Tool Use?](https://arxiv.org/abs/2606.02357) · [MM-ToolSandBox](https://arxiv.org/abs/2607.11818) |

## Agentic video reasoning

`VID-R` is reserved for **video understanding and reasoning**. It is deliberately separate from `AG-V`, which denotes agentic video generation or production. The table highlights mechanisms; the complete set is the `VID-R`-tagged timeline.

| Video-agent mechanism | Representative papers | Reliability question |
|---|---|---|
| Learned temporal search and tool policies | [Thinking With Videos](https://arxiv.org/abs/2508.04416) · [LongVT](https://arxiv.org/abs/2511.20785) · [SAGE](https://arxiv.org/abs/2512.13874) · [Weaver](https://arxiv.org/abs/2602.05829) · [EVA](https://arxiv.org/abs/2603.22918) · [InternVideo3](https://arxiv.org/abs/2606.12195) · [VSeek](https://arxiv.org/abs/2607.02959) | Does the policy retrieve decisive clips rather than exploit sampling or tool priors? |
| Memory and long-horizon retrieval | [M3-Agent](https://arxiv.org/abs/2508.09736) · [VideoLucy](https://arxiv.org/abs/2510.12422) · [WorldMM](https://arxiv.org/abs/2512.02425) · [VideoARM](https://arxiv.org/abs/2512.12360) · [EGAgent](https://arxiv.org/abs/2601.18157) · [Visual Agentic Memory](https://arxiv.org/abs/2605.16481) | Is the answer traceable to retained temporal evidence rather than lossy summaries? |
| Active perception and adaptive viewing | [Agentic Video Intelligence](https://arxiv.org/abs/2511.14446) · [Active Video Perception](https://arxiv.org/abs/2512.05774) · [LensWalk](https://arxiv.org/abs/2603.24558) · [ReTool-Video](https://arxiv.org/abs/2605.13228) · [Native Active Perception](https://arxiv.org/abs/2606.19341) · [Homer](https://arxiv.org/abs/2607.02588) | Does the agent know what, when, where, and how densely to observe—and when to stop? |
| Critics, verification, and evidence alignment | [CAViAR](https://arxiv.org/abs/2509.07680) · [Perceive, Verify and Understand Long Video](https://arxiv.org/abs/2509.24943) · [VideoHV-Agent](https://arxiv.org/abs/2603.04977) · [VideoSEAL](https://arxiv.org/abs/2605.12571) · [Evidence-Backed Video Question Answering](https://arxiv.org/abs/2607.11862) | Is the hypothesis supported by localized audiovisual evidence, and can a verifier reject unsupported paths? |
| Video deep research and open-world evidence | [VideoDR](https://arxiv.org/abs/2601.06943) · [HAVEN](https://arxiv.org/abs/2601.13719) · [LongVidSearch](https://arxiv.org/abs/2603.14468) · [VideoSearcher](https://arxiv.org/abs/2607.02927) | Can the agent preserve goals and verify evidence across video, audio, memory, and the open web? |

## Reliable reasoning

The `REL` tag marks methods and evaluations that explicitly target reliability, faithfulness, verification, calibrated tool use, evidence alignment, or generalization. Reliability is broader than image-only TWI: it also covers learned agent policies, multimodal search, long-video evidence, and test-time control. This is a cross-cutting index; every paper below appears once in the main timeline.

| Reliability focus | Papers | What is made reliable |
|---|---|---|
| Noisy-trace selection | [Reliable Thinking with Images](https://arxiv.org/abs/2602.12916) | Estimates the reliability of visual cues and textual reasoning, then filters and votes over candidate traces. |
| Reliable post-training and correction | [Agent0-VL](https://arxiv.org/abs/2511.19900) · [Deep But Reliable](https://arxiv.org/abs/2512.17306) · [CodeV](https://arxiv.org/abs/2511.19661) · [GTR-Turbo](https://arxiv.org/abs/2512.13043) · [ReGRPO](https://arxiv.org/abs/2606.31392) | Rewards grounded intermediate actions, supports evidence-based self-repair, stabilizes multi-turn training, and avoids gratuitous reflection. |
| Adaptive verifiers and reward models | [Multimodal Reinforcement Learning with Adaptive Verifier for AI Agents](https://arxiv.org/abs/2512.03438) · [ARM-Thinker](https://arxiv.org/abs/2512.05111) · [What, Whether and How?](https://arxiv.org/abs/2602.08346) | Judges localization, tool use, reasoning steps, and final correctness while reducing reward hacking. |
| Test-time perception scaling and control | [Test-time Scaling over Perception](https://arxiv.org/abs/2604.11025) · [SPARC](https://arxiv.org/abs/2602.06566) · [PixelEyes](https://arxiv.org/abs/2607.00115) | Allocates visual compute, filters uncertain traces, and avoids repeated unproductive inspection. |
| Evidence grounding and faithfulness | [DeFacto](https://arxiv.org/abs/2509.20912) · [Beyond Accuracy](https://arxiv.org/abs/2601.11633) · [VisualNeedle](https://arxiv.org/abs/2605.26380) · [Do Multimodal Agents Really Benefit from Tool Use?](https://arxiv.org/abs/2606.02357) | Tests whether answers causally depend on the claimed visual evidence and whether tools add capability rather than ceremony. |
| Reasoning–action alignment | [Walk the Talk](https://arxiv.org/abs/2604.06777) · [Diversity Over Frequency](https://arxiv.org/abs/2606.00096) · [TAPO](https://arxiv.org/abs/2606.05784) | Aligns reasoning with useful actions while preventing tool-use collapse, indiscriminate calls, and incorrect credit assignment. |
| Reliable video evidence | [CAViAR](https://arxiv.org/abs/2509.07680) · [Perceive, Verify and Understand Long Video](https://arxiv.org/abs/2509.24943) · [Active Video Perception](https://arxiv.org/abs/2512.05774) · [VideoHV-Agent](https://arxiv.org/abs/2603.04977) · [VideoSEAL](https://arxiv.org/abs/2605.12571) · [Evidence-Backed Video Question Answering](https://arxiv.org/abs/2607.11862) | Localizes temporal evidence, separates hypotheses from answer authority, and verifies claims before answering. |
| Search-process reliability | [VideoDR](https://arxiv.org/abs/2601.06943) · [ProMMSearchAgent](https://arxiv.org/abs/2604.20486) · [SimpleSearch-VL](https://arxiv.org/abs/2606.31504) · [VSeek](https://arxiv.org/abs/2607.02959) | Evaluates goal retention and evidence verification and trains search decisions with process-oriented or verifiable rewards. |
| Agentic-process diagnostics | [Agentic-MME](https://arxiv.org/abs/2604.03016) · [MM-ToolSandBox](https://arxiv.org/abs/2607.11818) | Audits stepwise search/tool trajectories and stateful multi-turn execution rather than scoring only final answers. |
| Reward and evaluator integrity | [JarvisEvo](https://arxiv.org/abs/2511.23002) · [Reward as An Agent for Embodied World Models](https://arxiv.org/abs/2606.19990) | Co-evolves evaluators or diversifies reward-guided rollouts while explicitly addressing reward hacking and evaluator collapse. |
| Trace efficiency and generalization | [Revisiting the Necessity of Lengthy Chain-of-Thought](https://arxiv.org/abs/2511.22586) | Tests whether shorter, essential grounding traces generalize better than lengthy visual chains of thought. |

## Tag legend

Tags identify a paper's **core contribution**, not every property its system happens to exhibit.

| Tag | Meaning |
|---|---|
| `AR` | General MLLM agentic reasoning |
| `TOOL` | External visual tool use or active perception |
| `SEARCH` | Multimodal search, retrieval, or evidence gathering |
| `ACT` | Embodied, GUI, or environment action |
| `TWI-E` | Thinking with externally obtained/edited images |
| `TWI-P` | Programmatic or symbolic visual manipulation |
| `TWI-G` | Generated image/video used as a thought |
| `TWI-L` | Latent or internally controlled visual thought |
| `AG-I` | Agentic image generation or editing |
| `AG-V` | Agentic video generation or production |
| `VID-R` | Agentic video understanding, temporal search, memory, or verification |
| `WM` | Video/world model used for prediction or planning |
| `REL` | Reliability, faithfulness, verification, or generalization of multimodal reasoning |
| `TRAIN` | Training, reinforcement learning, or process supervision |
| `POST` | Explicit post-training of a multi-turn agent policy, tool/search policy, or verifier |
| `INF` | Primary contribution in active test-time planning, evidence seeking, tool/compute control, verification, or stopping |
| `BENCH` | Benchmark, evaluation, survey, or diagnostic study |

## Paper timeline

Papers are ordered by **first public release date (newest first)**. Cross-tags expose category overlap without duplicating an entry.

<!-- PAPER_TIMELINE_START -->

### 2026-07

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2026-07-13 | [Beyond the Eye: Efficient Multimodal Reasoning via Self-Regulated Implicit Visual Tools](https://arxiv.org/abs/2607.11106) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Internalizes visual tools and learns when an explicit call is worth its cost. |
| 2026-07-13 | [Evidence-Backed Video Question Answering](https://arxiv.org/abs/2607.11862) | **VID-R · REL · TRAIN · BENCH** | Requires answers to carry human-verifiable temporal segments and tracked masklet evidence, exposing the gap between QA accuracy and true visual grounding. |
| 2026-07-13 | [Beyond the Single Camera: Agentic Multi-View Reasoning in Sports Video Understanding](https://arxiv.org/abs/2607.11844) | **AR · TOOL · VID-R · INF · BENCH** | Introduces SportMV-Bench and an agent that iteratively selects camera views, invokes perception tools, and reasons over complementary evidence. |
| 2026-07-13 | [Vinci2: Providing Proactive Assistance in Continuous Egocentric Videos](https://arxiv.org/abs/2607.11523) | **AR · SEARCH · VID-R · INF · BENCH** | Pairs EgoServe with EgoMemo, which retrieves multi-horizon memory to decide when and how a continuous-video assistant should intervene. |
| 2026-07-13 | [Omni-Decision: A Progressive Evidence-State Agent System for Omni-Modal QA](https://arxiv.org/abs/2607.11433) | **AR · TOOL · SEARCH · VID-R · REL · INF** | Maintains confirmed evidence, conflicts, dependencies, and open needs to control acquisition, repair, validation, and stopping. |
| 2026-07-13 | [MM-ToolSandBox: A Unified Framework for Evaluating Visual Tool-Calling Agents](https://arxiv.org/abs/2607.11818) | **AR · TOOL · REL · BENCH** | Provides a stateful benchmark with 500+ tools across 16 domains for multi-image, multi-turn visual tool calling. |
| 2026-07-12 | [UNIBROWSE: A Data-to-Agent Framework for Multimodal BrowseComp](https://arxiv.org/abs/2607.10557) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Covers text-only, image-to-text, and text-to-image browsing flows, then trains a long-horizon agent with exploration-aware SFT and RL. |
| 2026-07-09 | [OpenCoF: Learning to Reason Through Video Generation](https://arxiv.org/abs/2607.08763) | **TWI-G · AG-V · TRAIN** | Studies Chain-of-Frame reasoning with OpenCoF-17K, a fine-tuned video generator, and visual or textual reasoning tokens. |
| 2026-07-07 | [Segmentation before Answering: Pixel Grounding for MLLM Visual Reasoning](https://arxiv.org/abs/2607.05798) | **AR · TOOL · TWI-E · INF** | Uses mask-level grounding and targeted visual inspection before answering. |
| 2026-07-07 | [SearchEyes: Towards Frontier Multimodal Deep Search Intelligence via Search World Simulation](https://arxiv.org/abs/2607.05943) · [Code](https://github.com/Frostlinx/SearchEyes) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Unifies data, environment, and hop-level rewards in a reproducible graph-backed search world for multimodal agent RL. |
| 2026-07-06 | [CanvasAgent: Enabling Complex Image Creation and Editing via Visual Tool Orchestration](https://arxiv.org/abs/2607.05465) | **AR · TOOL · AG-I · TRAIN · POST · INF** | Learns 140K executable multi-tool creation trajectories and adapts decisions to the evolving canvas. |
| 2026-07-06 | [ReflectWorld-MM: An Entity-Oriented Multi-Media Memory System for Open-Ended Video Streams](https://arxiv.org/abs/2607.09759) | **AR · SEARCH · VID-R · INF** | Organizes unbounded streams around persistent entities using episodic, semantic, and procedural memories instead of flat frame stores. |
| 2026-07-06 | [Light-Omni: Reflex over Reasoning in Agentic Video Understanding with Long-Term Memory](https://arxiv.org/abs/2607.05511) | **AR · SEARCH · VID-R · INF** | Replaces costly iterative search with dual contextual states that drive aligned retrieval and autonomous responses in one pass. |
| 2026-07-03 | [Incentivizing Vision Language Models to Search for Long Video Question Answering](https://arxiv.org/abs/2607.02959) | **AR · SEARCH · VID-R · REL · TRAIN · POST · INF** | VSeek post-trains multi-turn video search with dense, verifiable rewards compiled from temporal-logic grounding requirements. |
| 2026-07-03 | [VideoSearcher: Empowering Video Deep Research with Multi-Tool Agentic Reasoning via Reinforcement Learning](https://arxiv.org/abs/2607.02927) | **AR · TOOL · SEARCH · VID-R · TRAIN · POST · INF · BENCH** | Unifies temporal localization, spatial focusing, and open-web search, while BiSPO separates tool-use and answer-accuracy optimization. |
| 2026-07-01 | [Retrieved Images as Visual Thought: Training-Free Multimodal In-Context Learning for the Open-vs-Closed Gap](https://arxiv.org/abs/2607.00606) | **SEARCH · TWI-E** | Treats retrieved examples as external visual thoughts in a training-free reasoning loop. |
| 2026-07-01 | [Homer: Understanding Long-form Videos with Hierarchical Memory and Agentic Reasoning](https://arxiv.org/abs/2607.02588) | **AR · SEARCH · VID-R · REL · INF** | Explores a temporal-and-causal memory hierarchy through multi-round retrieval with a harness that verifies and corrects every step. |
| 2026-07-01 | [A Cost-Aware, Paired Protocol for Auditing Dynamic Tool Synthesis in Agentic Video Question Answering](https://arxiv.org/abs/2607.01469) | **AR · TOOL · VID-R · REL · INF · BENCH** | Audits Dynamic-SAGE through paired accuracy-and-cost measurements, separating genuine efficiency gains from hidden costs. |
| 2026-07-01 | [EFlow: Learning Evidence Flow for Long-Video Reasoning with Adaptive Reflection](https://arxiv.org/abs/2607.00867) | **AR · TOOL · VID-R · REL · TRAIN · POST · INF** | Separates temporal grounding from answer reasoning and triggers full-video reflection when evidence appears insufficient. |
| 2026-07-01 | [Learning to Watch: Active Video Anomaly Understanding via Interleaved Policy Optimization](https://arxiv.org/abs/2607.00622) | **AR · TOOL · VID-R · TRAIN · POST · INF** | Uses iDPO to learn when to backtrack, expand temporal scope, or sample densely while balancing evidence value against cost. |
| 2026-07-01 | [VideoSearch-R1: Iterative Video Retrieval and Reasoning via Soft Query Refinement](https://arxiv.org/abs/2607.00446) | **AR · SEARCH · VID-R · TRAIN · POST · INF** | Refines search queries in continuous latent space with GRPO, coupling corpus retrieval to temporal grounding. |

### 2026-06

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2026-06-30 | [SimpleSearch-VL: A Simple Recipe for Multimodal Agentic Deep Search](https://arxiv.org/abs/2606.31504) | **AR · TOOL · SEARCH · REL · TRAIN · POST · INF** | Combines efficient rollouts with explicit verification of textual and visual evidence. |
| 2026-06-30 | [PixelEyes: Decoupling Perception and Reasoning for Pinpoint Visual Evidence Seeking](https://arxiv.org/abs/2607.00115) · [Project](https://godx-7.github.io/PixelEyesSite/) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF · BENCH** | Separates what to seek from where to find it through mask-guided search and semantic-region BFS, alongside Pinpoint-Bench. |
| 2026-06-30 | [ReGRPO: Reflection-Augmented Policy Optimization for Tool-Using Agents](https://arxiv.org/abs/2606.31392) · [Code](https://github.com/showlab/ReGRPO) | **AR · TOOL · REL · TRAIN · POST · INF** | Learns grounded failure diagnosis and corrective tool actions from near-miss trajectories rather than successes alone. |
| 2026-06-26 | [ProMSA: Progressive Multimodal Search Agents for Knowledge-Based Visual Question Answering](https://arxiv.org/abs/2606.27974) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Progressively selects image or text search and integrates retrieved evidence instead of relying on a fixed retriever and top-k. |
| 2026-06-25 | [Qwen-Image-Agent: Bridging the Context Gap in Real-World Image Generation](https://arxiv.org/abs/2606.26907) | **AR · SEARCH · AG-I** | Unifies planning, reasoning, search, memory, and feedback to ground underspecified generation requests. |
| 2026-06-23 | [IV-CoT: Implicit Visual Chain-of-Thought for Structure-Aware Text-to-Image Generation](https://arxiv.org/abs/2606.24849) | **TWI-L · AG-I** | Separates implicit structural planning from semantic rendering inside one T2I forward pass. |
| 2026-06-22 | [VideoAgent: All-in-One Framework for Video Understanding and Editing](https://arxiv.org/abs/2606.23327) · [Code](https://github.com/HKUDS/VideoAgent) | **AR · TOOL · AG-V · INF** | Plans shots and optimizes a graph of more than thirty specialized editing agents. |
| 2026-06-18 | [Reward as An Agent for Embodied World Models](https://arxiv.org/abs/2606.19990) | **AR · WM · REL · TRAIN · POST** | Uses an active reward agent and diversified rollouts to verify generated behavior and mitigate reward hacking under distribution shift. |
| 2026-06-17 | [Bridging Creative Intent and Visual Quality: Creator-Driven Recurrent Video Generation with Agentic Feedback Loops](https://arxiv.org/abs/2606.18591) | **AR · AG-V** | Uses persona-conditioned MLLM critics and a refiner agent in a human-directed recurrent loop. |
| 2026-06-17 | [Native Active Perception as Reasoning for Omni-Modal Understanding](https://arxiv.org/abs/2606.19341) | **AR · TOOL · VID-R · TRAIN · POST · INF** | OmniAgent learns a POMDP observation–thought–action policy with agentic SFT and TAURA, exhibiting positive test-time scaling. |
| 2026-06-17 | [VTOS: Learning to Orchestrate Vision Tools by Co-Searching Solutions and Observers](https://arxiv.org/abs/2606.20728) | **AR · TOOL · REL · TRAIN · POST · INF** | Co-searches executable tool pipelines and the visual conditions under which they remain valid, enabling adaptive recovery from brittle plans. |
| 2026-06-15 | [Gen-VCoT: Generative Visual Chain-of-Thought Reasoning via Diffusion-Based RGB Intermediate Representations](https://arxiv.org/abs/2606.16783) | **TWI-G · TRAIN** | Routes through interpretable RGB thoughts such as segmentation and depth before solving. |
| 2026-06-13 | [Visual-Seeker: Towards Visual-Native Multimodal Agentic Search via Active Visual Reasoning](https://arxiv.org/abs/2606.15231) · [Code](https://github.com/ZhengboZhang/Visual-Seeker) | **AR · TOOL · SEARCH · TWI-E · INF** | Actively focuses on fine-grained cues while accumulating visual evidence during search. |
| 2026-06-11 | [InterleaveThinker: Reinforcing Agentic Interleaved Generation](https://arxiv.org/abs/2606.13679) · [Code](https://github.com/zhengdian1/InterleaveThinker) · [Project](https://zhengdian1.github.io/InterleaveThinker-proj/) | **TWI-G · AG-I · TRAIN · POST · INF** | A planner proposes text–image sequences while a critic repairs instructions and triggers step-level regeneration. |
| 2026-06-11 | [Perceive, Interact, Reason: Building Tool-Augmented Visual Agents for Spatial Reasoning](https://arxiv.org/abs/2606.12830) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Turns visual interaction into active evidence acquisition for fine-grained spatial reasoning instead of relying on static encodings. |
| 2026-06-10 | [InternVideo3: Agentify Foundation Models with Multimodal Contextual Reasoning](https://arxiv.org/abs/2606.12195) | **AR · TOOL · VID-R · TRAIN · POST · INF** | Combines closed-loop contextual reasoning, efficient latent attention, staged training, memory, and retrieval tools in a video foundation model. |
| 2026-06-10 | [IAPO: Input Attribution-Aware Policy Optimization for Tool Use in Small Multimodal Agents](https://arxiv.org/abs/2606.11652) | **AR · TOOL · REL · TRAIN · POST · INF** | Uses attribution-aware rewards to teach small agents when visual inputs and tool observations genuinely support their answers. |
| 2026-06-07 | [Thinking Without Images: Internalizing Visual Manipulation with On-Policy Self-Distillation](https://arxiv.org/abs/2606.08719) | **TWI-L · TRAIN · POST** | Distills privileged crop/zoom evidence into internal “where to look” imagination trajectories. |
| 2026-06-05 | [MemDreamer: Decoupling Perception and Reasoning for Long Video Understanding via Hierarchical Graph Memory and Agentic Retrieval Mechanism](https://arxiv.org/abs/2606.07512) | **AR · TOOL · SEARCH · VID-R · INF** | Builds hierarchical causal graph memory and lets an observation–reason–action agent navigate nodes and logical edges on demand. |
| 2026-06-04 | [TAPO: Tool-Aware Policy Optimization via Credit Transfer for Multimodal Search Agents](https://arxiv.org/abs/2606.05784) | **AR · TOOL · SEARCH · REL · TRAIN · POST · INF** | Transfers credit to useful tool steps inside failed trajectories, correcting GRPO’s uniform trajectory-level credit assignment. |
| 2026-06-03 | [GOPAgen: Motion-Aware and Efficient Agentic Long-Video Understanding with Structural Memory and Hierarchical Reasoning](https://arxiv.org/abs/2606.06532) | **AR · SEARCH · VID-R · INF** | Introduces a codec-aware motion agent, GOP-tree reasoning, and coarse-to-fine retrieval over structural video memory. |
| 2026-06-02 | [ViMax: Agentic Video Generation](https://arxiv.org/abs/2606.07649) | **AR · AG-V** | Coordinates narrative, consistency, and VLM monitoring agents for long-form video generation. |
| 2026-06-02 | [MemoGen: Can Past Experience Improve Future Text-to-Image Generation?](https://arxiv.org/abs/2606.03243) | **AR · AG-I** | Reuses successful and failed generation experience through retrieval, evaluation, and memory. |
| 2026-06-01 | [MetaForge: A Self-Evolving Multimodal Agent that Retrieves, Adapts, and Forges Tools On Demand](https://arxiv.org/abs/2606.01801) | **AR · TOOL · TRAIN · POST · INF** | Moves beyond a static toolbox by forging, adapting, recycling, and learning to reuse skills. |
| 2026-06-01 | [Do Multimodal Agents Really Benefit from Tool Use? A Systematic Study of Capability Gains](https://arxiv.org/abs/2606.02357) | **AR · TOOL · TWI-E · REL · BENCH** | Tests whether tool outputs supply answer-critical evidence rather than merely appearing in superficially agentic traces. |

### 2026-05

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2026-05-30 | [DeepLatent: Think with Images via Parallel Latent Visual Reasoning](https://arxiv.org/abs/2606.00562) | **TWI-L · TRAIN** | Generates two-dimensional latent visual states in parallel and optimizes them with continuous-space RL. |
| 2026-05-28 | [GenClaw: Code-Driven Agentic Image Generation](https://arxiv.org/abs/2605.30248) | **TOOL · TWI-P · AG-I** | Follows conceptualize–sketch–color, using executable SVG/HTML/3D code as a controllable canvas. |
| 2026-05-28 | [Train the Agent, Not the Expert: Learning to Harness Heterogeneous Experts for Multi-Turn Visual Reasoning](https://arxiv.org/abs/2605.29894) | **AR · TOOL · TRAIN · POST · INF** | Trains an agent to select, sequence, and interpret heterogeneous visual experts across multi-turn reasoning trajectories. |
| 2026-05-27 | [Agent Explorative Policy Optimization for Multimodal Agentic Reasoning](https://arxiv.org/abs/2605.28774) · [Project](https://byungkwanlee.github.io/AXPO-page/) | **AR · TOOL · TRAIN · POST** | Targets the thinking–acting gap by resampling failed tool calls under fixed reasoning prefixes. |
| 2026-05-27 | [Agentic Active Omni-Modal Perception for Multi-Hop Audio-Visual Reasoning](https://arxiv.org/abs/2605.28192) | **AR · TOOL · VID-R · REL · INF · BENCH** | Introduces MOV-Bench and a training-free observe–reflect–replan agent over hierarchical audio-visual memory. |
| 2026-05-27 | [Self-Prophetic Decoding to Unlock Visual Search in LVLMs](https://arxiv.org/abs/2605.28741) | **AR · TOOL · TWI-E · INF** | Coordinates intrinsic reasoning and active visual search during decoding without overwriting separately post-trained capabilities. |
| 2026-05-27 | [Mags-RL: Wearing Multimodal LLMs a Magnifying Glass via Agentic Reinforcement Learning for Complex Scene Reasoning](https://arxiv.org/abs/2605.27960) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Reinforces iterative magnification and evidence inspection for visually dense scenes without requiring box-annotated reasoning traces. |
| 2026-05-26 | [How and What to Imagine? Visual Thinking in Unified Multimodal Models for Cross-View Spatial Reasoning](https://arxiv.org/abs/2605.27310) | **TWI-G · TRAIN** | Forces answers to depend on model-generated views and compares alternative imagination strategies. |
| 2026-05-25 | [Diversity Over Frequency: Rethinking Tool Use in Visual Chain-of-Thought Agents](https://arxiv.org/abs/2606.00096) · [Project](https://scaffolded-exploration.github.io/) | **AR · TOOL · TWI-E · REL · TRAIN · POST · BENCH** | Shows that diverse, task-relevant visual operations matter more than simply increasing tool-call frequency. |
| 2026-05-25 | [VisualNeedle: Benchmarking Active Visual Search in Information-Dense Scenes](https://arxiv.org/abs/2605.26380) | **AR · TOOL · TWI-E · REL · BENCH** | Removes linguistic and location shortcuts to test whether agents faithfully locate visual evidence in dense scenes. |
| 2026-05-22 | [CVSearch: Empowering Multimodal LLMs with Cognitive Visual Search for High-Resolution Image Perception](https://arxiv.org/abs/2605.23655) · [Code](https://github.com/liliupeng28/ICML26-CVSearch) | **AR · TOOL · TWI-E · INF** | Combines efficient expert proposals with coverage-preserving search to avoid both perceptual blind spots and redundant scans. |
| 2026-05-20 | [GenEvolve: Self-Evolving Image Generation Agents via Tool-Orchestrated Visual Experience Distillation](https://arxiv.org/abs/2605.21605) · [Code](https://github.com/MeiGen-AI/GenEvolve) · [Project](https://ephemeral182.github.io/GenEvolve/) | **AR · TOOL · AG-I · TRAIN · POST · INF** | Distills contrasts between strong and weak tool trajectories into reusable visual experience. |
| 2026-05-19 | [Semantic-Enriched Latent Visual Reasoning](https://arxiv.org/abs/2605.19342) | **TWI-L · TRAIN** | Adds attribute supervision and multi-query RL to make region-centric visual latents semantically stable. |
| 2026-05-19 | [ParaVT: Taming the Tool Prior Paradox for Parallel Tool Use in Agentic Video Reinforcement Learning](https://arxiv.org/abs/2605.20342) | **AR · TOOL · VID-R · REL · TRAIN · POST · INF** | Parallelizes temporal crops and uses PARA-GRPO to prevent format collapse and skip-tool reward shortcuts. |
| 2026-05-19 | [Are Tools Always Beneficial? Learning to Invoke Tools Adaptively for Dual-Mode Multimodal LLM Reasoning](https://arxiv.org/abs/2605.19852) · [Code](https://github.com/MQinghe/AutoTool) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF** | Learns whether a task benefits from visual tools, reducing harmful or unnecessary calls while retaining direct reasoning. |
| 2026-05-18 | [Generation Navigator: A State-Aware Agentic Framework for Image Generation](https://arxiv.org/abs/2605.17969) | **AR · AG-I · TRAIN · POST · INF** | Learns a state-conditioned next-action policy with trajectory rewards for quality, retention, and efficiency. |
| 2026-05-18 | [Starve to Perceive: Taming Lazy Perception in VLMs with Constrained Visual Bandwidth](https://arxiv.org/abs/2605.18603) · [Code](https://github.com/WhuanY/Starve2Perceive) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF** | Restricts visual bandwidth so agents must functionally depend on active crop, zoom, and pan observations. |
| 2026-05-16 | [PyraVid: Hierarchical Multimodal Memory for Long-Horizon Video Reasoning](https://arxiv.org/abs/2605.17065) | **AR · SEARCH · VID-R · INF** | Organizes video memory as a coarse-to-fine pyramid and retrieves causally connected events through expansion with pruning. |
| 2026-05-15 | [Visual Agentic Memory: Enabling Online Long Video Understanding via Online Indexing, Hierarchical Memory, and Agentic Retrieval](https://arxiv.org/abs/2605.16481) | **AR · SEARCH · VID-R · REL · INF** | Makes streaming visual evidence selectively retained, inspectable, searchable, and verifiable. |
| 2026-05-14 | [From Plans to Pixels: Learning to Plan and Orchestrate for Open-Ended Image Editing](https://arxiv.org/abs/2605.15181) | **AR · TOOL · AG-I · TRAIN · POST · INF** | Trains a planner and tool orchestrator from successful atomic editing trajectories and VLM outcome rewards. |
| 2026-05-14 | [Unlocking Complex Visual Generation via Closed-Loop Verified Reasoning](https://arxiv.org/abs/2605.14876) | **TWI-G · AG-I · TRAIN · POST · INF** | Uses stepwise visual verification and trajectory-level credit assignment for closed-loop generation. |
| 2026-05-14 | [Breaking Dual Bottlenecks: Evolving Unified Multimodal Models into Self-Adaptive Interleaved Visual Reasoners](https://arxiv.org/abs/2605.14709) · [Code](https://github.com/WeChatCV/Interleaved_Visual_Reasoner) | **TWI-G · AG-I · TRAIN · POST · INF** | Learns to switch among direct generation, reflection, and multi-step visual planning. |
| 2026-05-13 | [Towards Long-horizon Embodied Agents with Tool-Aligned Vision-Language-Action Models](https://arxiv.org/abs/2605.13119) | **AR · TOOL · ACT · TRAIN · POST · INF** | A high-level VLM plans and recovers while specialized VLA tools execute and report progress. |
| 2026-05-13 | [EvoGround: Self-Evolving Video Agents for Video Temporal Grounding](https://arxiv.org/abs/2605.13803) | **AR · VID-R · TRAIN · POST** | Couples proposer and solver agents in a self-reinforcing RL loop that learns temporal grounding from unlabeled videos. |
| 2026-05-13 | [ReTool-Video: Recursive Tool-Using Video Agents with Meta-Augmented Tool Grounding](https://arxiv.org/abs/2605.13228) | **AR · TOOL · VID-R · REL · INF** | Grounds high-level intents recursively into 134 tools, repairing parameters or decomposing unsupported actions at runtime. |
| 2026-05-12 | [UniVLR: Unifying Text and Vision in Visual Latent Reasoning for Multimodal LLMs](https://arxiv.org/abs/2605.11856) | **TWI-L · TRAIN** | Compresses text traces and auxiliary renderings into a shared latent visual workspace. |
| 2026-05-12 | [VideoSEAL: Mitigating Evidence Misalignment in Agentic Long Video Understanding by Decoupling Answer Authority](https://arxiv.org/abs/2605.12571) | **AR · TOOL · VID-R · REL · INF** | Separates planning from answer authority and gates final responses on pixel-level inspection. |
| 2026-05-12 | [From Web to Pixels: Bringing Agentic Search into Visual Perception](https://arxiv.org/abs/2605.12497) | **AR · TOOL · SEARCH · TWI-E · INF** | Chains open-web evidence gathering with pixel-level localization for objects whose identity cannot be resolved from the image alone. |
| 2026-05-11 | [WorldReasonBench: Human-Aligned Stress Testing of Video Generators as Future World-State Predictors](https://arxiv.org/abs/2605.10434) | **AG-V · WM · REL · BENCH** | Tests whether generated futures preserve physical, social, logical, and informational state with process-aware verification. |
| 2026-05-11 | [Towards On-Policy Data Evolution for Visual-Native Multimodal Deep Search Agents](https://arxiv.org/abs/2605.10832) · [Code](https://github.com/JoeYing1019/ODE) · [Project](https://on-policy-data-evolution.github.io/) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Evolves search training data from current-policy failures while preserving visual artifacts for reuse across later tool calls. |
| 2026-05-08 | [SCOPE: Structured Decomposition and Conditional Skill Orchestration for Complex Image Generation](https://arxiv.org/abs/2605.08043) · [Code](https://github.com/nopnor/SCOPE) · [Project](https://nopnor.github.io/SCOPE/) | **AR · TOOL · AG-I · INF** | Evolves a semantic specification and uses verifier-attributed failures to select repair skills. |
| 2026-05-08 | [Bridging Modalities, Spanning Time: Structured Memory for Ultra-Long Agentic Video Reasoning](https://arxiv.org/abs/2605.08271) | **AR · SEARCH · VID-R · INF** | MAGIC-Video combines a multimodal memory graph with narrative chains for retrieval across modalities and days-long timelines. |
| 2026-05-08 | [HyperEyes: Dual-Grained Efficiency-Aware Reinforcement Learning for Parallel Multimodal Search Agents](https://arxiv.org/abs/2605.07177) · [Code](https://github.com/DeepExperience/HyperEyes) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Reinforces parallel grounded queries so independent evidence can be gathered wider rather than through longer sequential traces. |
| 2026-05-06 | [OpenSearch-VL: An Open Recipe for Frontier Multimodal Search Agents](https://arxiv.org/abs/2605.05185) · [Code](https://github.com/shawn0728/OpenSearch-VL) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Open-sources the data, tool environment, and failure-aware RL recipe for multimodal search. |
| 2026-05-02 | [Action Agent: Agentic Video Generation Meets Flow-Constrained Diffusion](https://arxiv.org/abs/2605.01477) | **ACT · AG-V · WM** | Iteratively generates and validates goal videos, then converts them into robot navigation controls. |
| 2026-05-01 | [Scaling Video Understanding via Compact Latent Multi-Agent Collaboration](https://arxiv.org/abs/2605.00444) | **AR · VID-R · TRAIN · POST · INF** | Lets segment-level agents exchange compact task-sufficient latent tokens with a coordinator through a progressive curriculum. |

### 2026-04

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2026-04-27 | [See Further, Think Deeper: Advancing VLM's Reasoning Ability with Low-level Visual Cues and Reflection](https://arxiv.org/abs/2604.24339) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF** | ForeSight combines low-level visual cues with reflective feedback to correct perceptual mistakes during interleaved reasoning. |
| 2026-04-26 | [CineAGI: Character-Consistent Movie Creation through LLM-Orchestrated Multi-Modal Generation and Cross-Scene Integration](https://arxiv.org/abs/2604.23579) | **AR · AG-V** | Orchestrates narrative blueprints, character consistency, cross-scene integration, and audiovisual synchronization. |
| 2026-04-23 | [S1-VL: Scientific Multimodal Reasoning Model with Thinking-with-Images](https://arxiv.org/abs/2604.21409) | **AR · TOOL · TWI-P · INF** | Writes and executes image-processing code in a sandbox to obtain scientific visual evidence. |
| 2026-04-22 | [IMPACT-CYCLE: A Contract-Based Multi-Agent System for Claim-Level Supervisory Correction of Long-Video Semantic Memory](https://arxiv.org/abs/2604.20136) | **AR · VID-R · REL · INF** | Maintains versioned claims, dependencies, and provenance under explicit authority contracts, escalating unresolved evidence to humans. |
| 2026-04-22 | [ProMMSearchAgent: A Generalizable Multimodal Search Agent Trained with Process-Oriented Rewards](https://arxiv.org/abs/2604.20486) | **AR · TOOL · SEARCH · REL · TRAIN · POST · INF** | Uses simulated search and process rewards for knowledge-boundary recognition and search-decision learning before real-world deployment. |
| 2026-04-21 | [Visual Reasoning through Tool-supervised Reinforcement Learning](https://arxiv.org/abs/2604.19945) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | ToolsRL first optimizes tool-specific rewards, then answer accuracy, separating tool mastery from downstream task learning. |
| 2026-04-21 | [DR-MMSearchAgent: Deepening Reasoning in Multimodal Search Agents](https://arxiv.org/abs/2604.19264) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Uses trajectory-structure advantages and calibrated interaction rewards to prevent premature search collapse and redundant context. |
| 2026-04-19 | [Waking Up Blind: Cold-Start Optimization of Supervision-Free Agentic Trajectories for Grounded Visual Perception](https://arxiv.org/abs/2604.17475) · [Code](https://github.com/ab-iitd/spectra) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | SPECTRA bootstraps grounded visual-tool trajectories through supervision-free cascaded rollouts and cold-start reinforcement learning. |
| 2026-04-15 | [POINTS-Seeker: Towards Training a Multimodal Agentic Search Model from Scratch](https://arxiv.org/abs/2604.14029) · [Project](https://code-kunkun.github.io/POINTS-Seeker/) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Trains an end-to-end multimodal search policy rather than attaching search as a fixed external workflow. |
| 2026-04-14 | [Towards Long-horizon Agentic Multimodal Search](https://arxiv.org/abs/2604.12890) · [Code](https://github.com/RUCAIBox/LMM-Searcher) | **AR · TOOL · SEARCH · TWI-E · INF** | Stores visual assets by identifier and fetches them on demand across search traces up to one hundred turns. |
| 2026-04-14 | [Don't Show Pixels, Show Cues: Unlocking Visual Tool Reasoning in Language Models via Perception Programs](https://arxiv.org/abs/2604.12896) · [Code](https://github.com/AISmartPerception/perception-programs) | **AR · TOOL · TWI-P · INF** | Converts dense visual-tool outputs into language-aligned perception programs that are easier to compose and reason over. |
| 2026-04-13 | [Test-time Scaling over Perception: Resolving the Grounding Paradox in Thinking with Images](https://arxiv.org/abs/2604.11025) · [Code](https://github.com/jiangzheng2024/TTSP) | **AR · TOOL · TWI-E · REL · INF** | Samples exploratory perception traces, filters them by confidence, and iteratively resolves remaining visual uncertainty. |
| 2026-04-11 | [Agentic Video Generation: From Text to Executable Event Graphs via Tool-Constrained LLM Planning](https://arxiv.org/abs/2604.10383) | **AR · TWI-P · AG-V** | Builds validated event graphs with director, scene-builder, and relation agents before deterministic rendering. |
| 2026-04-08 | [Walk the Talk: Bridging the Reasoning-Action Gap for Thinking with Images via Multimodal Agentic Policy Optimization](https://arxiv.org/abs/2604.06777) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF** | Aligns tool observations with reasoning advantages so visual actions become useful rather than decorative. |
| 2026-04-07 | [MTA-Agent: An Open Recipe for Multimodal Deep Search Agents](https://arxiv.org/abs/2604.06376) · [Code](https://github.com/SalesforceAIResearch/MTA-Agent) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Builds verified multi-hop multimodal search data and an open training recipe for evidence-grounded deep-search agents. |
| 2026-04-06 | [SVAgent: Storyline-Guided Long Video Understanding via Cross-Modal Multi-Agent Collaboration](https://arxiv.org/abs/2604.05079) | **AR · VID-R · REL · INF** | Builds an evolving storyline from past failures and uses a meta-agent to reconcile visual and textual predictions. |
| 2026-04-06 | [Graph-to-Frame RAG: Visual-Space Knowledge Fusion for Training-Free and Auditable Video Reasoning](https://arxiv.org/abs/2604.04372) | **AR · SEARCH · VID-R · REL · INF** | Retrieves a minimal knowledge subgraph and renders it as an inspectable reasoning frame with a concrete evidence trail. |
| 2026-04-03 | [Progressive Video Condensation with MLLM Agent for Long-form Video Understanding](https://arxiv.org/abs/2604.02891) | **AR · TOOL · VID-R · INF** | Progressively narrows a video from segments to snippets to keyframes under a small frame budget. |
| 2026-04-03 | [Agentic-MME: What Agentic Capability Really Brings to Multimodal Intelligence?](https://arxiv.org/abs/2604.03016) · [Code](https://github.com/ChoS3nE11ven/Agentic-MME) · [Project](https://agenticmme.github.io/) | **AR · TOOL · SEARCH · REL · BENCH** | Audits visual and web-search trajectories with more than 2,000 stepwise checkpoints instead of scoring final answers alone. |

### 2026-03

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2026-03-31 | [Unify-Agent: A Unified Multimodal Agent for World-Grounded Image Synthesis](https://arxiv.org/abs/2603.29620) | **AR · SEARCH · AG-I** | Searches multimodal evidence, produces a grounded recaption, and then synthesizes the requested image. |
| 2026-03-30 | [Gen-Searcher: Reinforcing Agentic Search for Image Generation](https://arxiv.org/abs/2603.28767) · [Code](https://github.com/tulerfeng/Gen-Searcher) · [Project](https://gen-searcher.vercel.app/) | **SEARCH · AG-I · TRAIN** | Learns multi-hop web/image search and generation with text- and image-level rewards. |
| 2026-03-30 | [GEMS: Agent-Native Multimodal Generation with Memory and Skills](https://arxiv.org/abs/2603.28088) · [Code](https://github.com/lcqysl/GEMS) · [Project](https://gems-gen.github.io/) | **AR · TOOL · AG-I** | Combines a structured agent loop, trajectory memory, and on-demand generation skills. |
| 2026-03-26 | [LanteRn: Latent Visual Structured Reasoning](https://arxiv.org/abs/2603.25629) | **TWI-L · TRAIN** | Interleaves language with compact continuous visual thoughts aligned to task utility. |
| 2026-03-25 | [LensWalk: Agentic Video Understanding by Planning How You See in Videos](https://arxiv.org/abs/2603.24558) | **AR · TOOL · VID-R · INF** | Lets a reasoner choose temporal scope and sampling density in a reason–plan–observe loop that gathers and verifies evidence on demand. |
| 2026-03-24 | [EVA: Efficient Reinforcement Learning for End-to-End Video Agent](https://arxiv.org/abs/2603.22918) | **AR · TOOL · VID-R · TRAIN · POST · INF** | Learns planning-before-perception through summary–plan–action–reflection trajectories using SFT, KTO, and GRPO. |
| 2026-03-24 | [SpecEyes: Accelerating Agentic Multimodal LLMs via Speculative Perception and Planning](https://arxiv.org/abs/2603.23483) · [Code](https://github.com/MAC-AutoML/SpecEyes) | **AR · TOOL · TWI-E · INF** | Speculates upcoming perception actions, then uses cognitive gating and self-verification to shorten sequential visual-tool loops. |
| 2026-03-20 | [VideoSeek: Long-Horizon Video Agent with Tool-Guided Seeking](https://arxiv.org/abs/2603.20185) | **AR · TOOL · VID-R · INF** | Follows video logic flow in a think–act–observe loop to seek answer-critical evidence with far fewer frames. |
| 2026-03-18 | [AgentVLN: Towards Agentic Vision-and-Language Navigation](https://arxiv.org/abs/2603.17670) · [Code](https://github.com/Allenxinn/AgentVLN) | **AR · TOOL · ACT · TWI-E** | Uses a VLM brain, a skill library, active exploration, and self-correction for navigation. |
| 2026-03-18 | [Symphony: A Cognitively-Inspired Multi-Agent System for Long-Video Understanding](https://arxiv.org/abs/2603.17307) | **AR · VID-R · REL · INF** | Combines fine-grained task decomposition, reflective agent collaboration, and VLM grounding for long-chain video reasoning. |
| 2026-03-16 | [VTC-Bench: Evaluating Agentic Multimodal Models via Compositional Visual Tool Chaining](https://arxiv.org/abs/2603.15030) · [Code](https://github.com/zhuzil/VTC-Bench) | **AR · TOOL · BENCH** | Evaluates whether agents can correctly execute and compose diverse visual tools across non-trivial multi-step chains. |
| 2026-03-15 | [VLA-Thinker: Boosting Vision-Language-Action Models through Thinking-with-Image Reasoning](https://arxiv.org/abs/2603.14523) · [Project](https://cywang735.github.io/VLA-Thinker/) | **AR · ACT · TWI-E · TRAIN · POST · INF** | Models “look again” as a callable reasoning action and optimizes the full reasoning–action trajectory. |
| 2026-03-15 | [LongVidSearch: An Agentic Benchmark for Multi-hop Evidence Retrieval Planning in Long Videos](https://arxiv.org/abs/2603.14468) | **AR · TOOL · SEARCH · VID-R · BENCH** | Enforces exact multi-hop evidence requirements behind a standardized interface, isolating retrieval planning from answer generation. |
| 2026-03-14 | [A Multi-Agent Perception-Action Alliance for Efficient Long Video Reasoning](https://arxiv.org/abs/2603.14052) | **AR · VID-R · REL · INF** | Uses cue-guided perception, peer cross-review, consensus checks, pruning, and renewed exploration across VLM agents. |
| 2026-03-09 | [SPIRAL: Self-Evolving Action-Conditioned Video Generation via Reflective Planning Agents](https://arxiv.org/abs/2603.08403) | **ACT · AG-V · WM · TRAIN** | A planning agent decomposes actions while a video critic and long-horizon memory guide iterative world-model generation. |
| 2026-03-05 | [Think, Then Verify: A Hypothesis-Verification Multi-Agent Framework for Long Video Understanding](https://arxiv.org/abs/2603.04977) | **AR · TOOL · VID-R · REL · INF** | Converts candidate answers into testable hypotheses, derives discriminative clues, and grounds each clue before synthesis. |
| 2026-03-03 | [VSearcher: Long-Horizon Multimodal Search Agent via Reinforcement Learning](https://arxiv.org/abs/2603.02795) · [Code](https://github.com/Ruiyang-061X/VSearcher) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Reinforces long-horizon multimodal search policies that iteratively gather and integrate external textual and visual evidence. |
| 2026-03-02 | [Generative Visual Chain-of-Thought for Image Editing](https://arxiv.org/abs/2603.01893) · [Project](https://pris-cv.github.io/GVCoT/) | **TWI-G · AG-I · TRAIN** | Generates native spatial visual cues before applying an edit in one jointly optimized model. |
| 2026-03-02 | [From Verbatim to Gist: Distilling Pyramidal Multimodal Memory via Semantic Information Bottleneck for Long-Horizon Video Agents](https://arxiv.org/abs/2603.01455) | **AR · SEARCH · VID-R · TRAIN · POST · INF** | Trains pyramidal memory with SIB-GRPO and retrieves top-down by entropy, balancing compression against evidence retention. |
| 2026-03-01 | [MM-DeepResearch: A Simple and Effective Multimodal Agentic Search Baseline](https://arxiv.org/abs/2603.01050) · [Code](https://github.com/HJYao00/MM-DeepResearch) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Creates tool-use trajectories with experts and tree search, then applies agentic RL offline. |
| 2026-03-01 | [MC-Search: Evaluating and Enhancing Multimodal Agentic Search with Structured Long Reasoning Chains](https://arxiv.org/abs/2603.00873) · [Project](https://mc-search-project.github.io/) | **AR · TOOL · SEARCH · TRAIN · POST · INF · BENCH** | Couples a long-chain multimodal search benchmark with structured trajectories for training more persistent search agents. |

### 2026-02

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2026-02-28 | [RAISE: Requirement-Adaptive Evolutionary Refinement for Training-Free Text-to-Image Alignment](https://arxiv.org/abs/2603.00483) · [Code](https://github.com/LiyaoJiang1998/RAISE) | **AR · AG-I · INF** | Discovers requirements, evolves candidates with multiple repair actions, and stops when its checklist is satisfied. |
| 2026-02-27 | [Thinking with Images as Continuous Actions: Numerical Visual Chain-of-Thought](https://arxiv.org/abs/2602.23959) · [Code](https://github.com/kesenzhao/NV-CoT) | **AR · TWI-L · TRAIN** | Treats coordinates as continuous actions and directly optimizes precise visual grounding. |
| 2026-02-26 | [PhotoAgent: Agentic Photo Editing with Exploratory Visual Aesthetic Planning](https://arxiv.org/abs/2602.22809) · [Code](https://github.com/mdyao/PhotoAgent) · [Project](https://mdyao.github.io/PhotoAgent/) | **AR · TOOL · AG-I** | Searches an aesthetic edit tree with memory and iterative visual feedback. |
| 2026-02-26 | [AgentVista: Evaluating Multimodal Agents in Ultra-Challenging Realistic Visual Scenarios](https://arxiv.org/abs/2602.23166) · [Code](https://github.com/hkust-nlp/AgentVista) · [Project](https://agentvista-bench.github.io/) | **AR · TOOL · SEARCH · BENCH** | Tests long-horizon workflows that combine web and image search, page navigation, code execution, and visual processing. |
| 2026-02-26 | [OmniGAIA: Towards Native Omni-Modal AI Agents](https://arxiv.org/abs/2602.22897) · [Code](https://github.com/RUC-NLPIR/OmniGAIA) | **AR · TOOL · SEARCH · VID-R · TRAIN · POST · INF · BENCH** | Introduces an image–audio–video agent benchmark and trains OmniAtlas with hindsight tree trajectories and OmniDPO. |
| 2026-02-24 | [PyVision-RL: Forging Open Agentic Vision Models via RL](https://arxiv.org/abs/2602.20739) · [Code](https://github.com/agents-x-project/PyVision-RL) | **AR · TOOL · TWI-E · VID-R · TRAIN · POST · INF** | Preserves multi-turn tool interaction and supports on-demand video frame inspection. |
| 2026-02-24 | [LongVideo-R1: Smart Navigation for Low-cost Long Video Understanding](https://arxiv.org/abs/2602.20913) | **AR · TOOL · VID-R · TRAIN · POST · INF** | Learns hierarchical clip navigation and early stopping from tool trajectories through SFT followed by efficiency-aware RL. |
| 2026-02-17 | [EventMemAgent: Hierarchical Event-Centric Memory for Online Video Understanding with Adaptive Tool Use](https://arxiv.org/abs/2602.15329) | **AR · TOOL · VID-R · TRAIN · POST · INF** | Combines event-level short- and long-term memory with adaptive perception tools internalized through agentic RL. |
| 2026-02-16 | [TikArt: Stabilizing Aperture-Guided Fine-Grained Visual Reasoning with Reinforcement Learning](https://arxiv.org/abs/2602.14482) · [Code](https://github.com/TikArt-Team/TikArt) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF** | Reinforces sequential aperture selection while stabilizing the policy against localization drift and sparse visual rewards. |
| 2026-02-13 | [Reliable Thinking with Images](https://arxiv.org/abs/2602.12916) · [Code](https://github.com/XLearning-SCU/Reliable_TWI) | **TWI-E · REL · TRAIN · INF · BENCH** | Filters and votes over noisy visual thoughts to improve reliability. |
| 2026-02-12 | [IMAGAgent: Orchestrating Multi-Turn Image Editing via Constraint-Aware Planning and Reflection](https://arxiv.org/abs/2603.29602) · [Code](https://github.com/hackermmzz/IMAGAgent) | **AR · TOOL · AG-I** | Decomposes constraints, orchestrates heterogeneous editors, aggregates multiple critics, retries, and retains the best state. |
| 2026-02-11 | [Chatting with Images for Introspective Visual Thinking](https://arxiv.org/abs/2602.11073) | **TWI-L · TRAIN** | Uses language-guided feature modulation and multi-region re-encoding instead of pixel tools. |
| 2026-02-09 | [What, Whether and How? Unveiling Process Reward Models for Thinking with Images Reasoning](https://arxiv.org/abs/2602.08346) · [Code](https://github.com/siruihan2024/Process-Reward-Models-Thinking-Images) | **TWI-E · REL · TRAIN · BENCH** | Studies process rewards over annotated visual-tool trajectories and seven error types. |
| 2026-02-09 | [Agent Banana: High-Fidelity Image Editing with Agentic Thinking and Tooling](https://arxiv.org/abs/2602.09084) · [Project](https://agent-banana.github.io/) | **AR · AG-I** | Uses a planner–executor hierarchy, folded long-context memory, and image-layer decomposition. |
| 2026-02-08 | [VideoTemp-o3: Harmonizing Temporal Grounding and Video Understanding in Agentic Thinking-with-Videos](https://arxiv.org/abs/2602.07801) | **AR · TOOL · VID-R · REL · TRAIN · POST · INF · BENCH** | Jointly learns grounding and QA with revisable clipping, exploration-aware masking, and rewards designed to resist reward hacking. |
| 2026-02-06 | [SPARC: Separating Perception And Reasoning Circuits for Test-time Scaling of VLMs](https://arxiv.org/abs/2602.06566) | **AR · TOOL · TWI-E · REL · INF** | Separates visual search from reasoning so perception can be scaled independently under uncertainty or distribution shift. |
| 2026-02-05 | [M3: High-fidelity Text-to-Image Generation via Multi-Modal, Multi-Agent and Multi-Round Visual Reasoning](https://arxiv.org/abs/2602.06166) | **AR · AG-I** | Planner, checker, refiner, editor, and verifier agents repair constraints over multiple rounds. |
| 2026-02-05 | [Weaver: End-to-End Agentic System Training for Video Interleaved Reasoning](https://arxiv.org/abs/2602.05829) | **AR · TOOL · VID-R · TRAIN · POST · INF** | Trains a policy end to end to combine visual tools and construct interleaved multimodal reasoning trajectories from trajectory-free RL data. |
| 2026-02-05 | [V-Retrver: Evidence-Driven Agentic Reasoning for Universal Multimodal Retrieval](https://arxiv.org/abs/2602.06034) · [Code](https://github.com/chendy25/V-Retrver) | **AR · TOOL · SEARCH · TWI-E · REL · TRAIN · POST · INF** | Alternates hypothesis formation with targeted visual verification and trains the policy with evidence-aligned objectives. |
| 2026-02-04 | [VideoBrain: Learning Adaptive Frame Sampling for Long Video Understanding](https://arxiv.org/abs/2602.04094) | **AR · TOOL · VID-R · REL · TRAIN · POST · INF** | Learns semantic-retrieval and temporal-sampling agents with a behavior-aware reward that discourages gratuitous calls. |
| 2026-02-02 | [Kimi K2.5: Visual Agentic Intelligence](https://arxiv.org/abs/2602.02276) · [Code](https://github.com/MoonshotAI/Kimi-K2.5) · [Blog](https://www.kimi.com/blog/kimi-k2-5) | **AR · TOOL · ACT · TRAIN · POST · INF** | A native multimodal agent model spanning visual tool use, computer use, and parallel sub-agent orchestration. |
| 2026-02-02 | [Mind-Brush: Integrating Agentic Cognitive Search and Reasoning into Image Generation](https://arxiv.org/abs/2602.01756) | **AR · SEARCH · AG-I** | Researches multimodal evidence before generating images with implicit or knowledge-heavy constraints. |
| 2026-02-02 | [ViThinker: Active Vision-Language Reasoning via Dynamic Perceptual Querying](https://arxiv.org/abs/2602.02873) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Actively requests task-relevant visual detail during reasoning instead of relying on a fixed pre-computed image representation. |

### 2026-01

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2026-01-29 | [Vision-DeepResearch: Incentivizing DeepResearch Capability in Multimodal Large Language Models](https://arxiv.org/abs/2601.22060) · [Code](https://github.com/Osilly/Vision-DeepResearch) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Supports long-horizon, multi-entity, and multi-scale visual/text retrieval inside an MLLM. |
| 2026-01-28 | [Shape of Thought: Progressive Object Assembly via Visual Chain-of-Thought](https://arxiv.org/abs/2601.21081) · [Code](https://github.com/yuhuo03/Shape-of-Thought) | **TWI-G · AG-I · TRAIN** | Interleaves textual plans with progressively rendered object-assembly states. |
| 2026-01-26 | [GenAgent: Scaling Text-to-Image Generation via Agentic Multimodal Reasoning](https://arxiv.org/abs/2601.18543) | **AR · TOOL · AG-I · TRAIN · POST · INF** | Learns reason–invoke–judge–reflect loops around interchangeable image generators. |
| 2026-01-26 | [Agentic Very Long Video Understanding](https://arxiv.org/abs/2601.18157) | **AR · TOOL · SEARCH · VID-R · INF** | EGAgent plans structured searches over entity scene graphs and combines visual with audio retrieval for days- or weeks-long video. |
| 2026-01-26 | [AdaReasoner: Dynamic Tool Orchestration for Iterative Visual Reasoning](https://arxiv.org/abs/2601.18631) · [Code](https://github.com/ssmisya/AdaReasoner) · [Project](https://adareasoner.github.io/) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Learns which visual tools to invoke, when to invoke them, and how to compose unfamiliar tools over iterative reasoning. |
| 2026-01-25 | [The Script is All You Need: An Agentic Framework for Long-Horizon Dialogue-to-Cinematic Video Generation](https://arxiv.org/abs/2601.17737) · [Code](https://github.com/Tencent/digitalhuman/tree/main/ScriptAgent) | **AR · AG-V** | Splits long-form production across scripter, director, and critic agents. |
| 2026-01-22 | [VideoThinker: Building Agentic VideoLLMs with LLM-Guided Tool Reasoning](https://arxiv.org/abs/2601.15724) | **AR · TOOL · VID-R · REL · TRAIN · POST · INF** | Synthesizes tool trajectories in caption space, grounds them back to frames, and triggers retrieval or zoom under low confidence. |
| 2026-01-21 | [Iterative Refinement Improves Compositional Image Generation](https://arxiv.org/abs/2601.15286) · [Code](https://github.com/shantanuj/Iterative-Image-Gen) · [Project](https://iterative-img-gen.github.io/) | **AR · AG-I** | A VLM critic, editor, and verifier iteratively repair unmet compositional constraints. |
| 2026-01-20 | [Hierarchical Long Video Understanding with Audiovisual Entity Cohesion and Agentic Search](https://arxiv.org/abs/2601.13719) | **AR · SEARCH · VID-R · INF** | HAVEN preserves cross-modal entity cohesion in a hierarchical index and searches across global, scene, segment, and entity levels. |
| 2026-01-14 | [Beyond Accuracy: Evaluating Grounded Visual Evidence in Thinking with Images](https://arxiv.org/abs/2601.11633) · [Code](https://github.com/Xuchen-Li/ViEBench) | **TWI-E · REL · BENCH** | Evaluates whether visual intermediate evidence is grounded, not just whether answers are correct. |
| 2026-01-14 | [M³Searcher: Modular Multimodal Information Seeking Agency with Retrieval-Oriented Reasoning](https://arxiv.org/abs/2601.09278) · [Code](https://github.com/Alibaba-NLP/OmniSearch) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Decomposes multimodal information seeking into specialized retrieval modules coordinated by retrieval-oriented reasoning. |
| 2026-01-11 | [Watching, Reasoning, and Searching: A Video Deep Research Benchmark on Open Web for Agentic Video Reasoning](https://arxiv.org/abs/2601.06943) | **AR · SEARCH · VID-R · REL · BENCH** | VideoDR tests cross-frame anchors, open-web retrieval, and multi-hop verification while diagnosing goal drift over long search chains. |
| 2026-01-05 | [Agentic Retoucher for Text-To-Image Generation](https://arxiv.org/abs/2601.02046) | **AR · TOOL · AG-I** | Uses specialized agents to locate, diagnose, and locally repair image defects. |
| 2026-01-01 | [CPPO: Contrastive Perception for Vision Language Policy Optimization](https://arxiv.org/abs/2601.00501) · [Code](https://github.com/vbdi/cppo) | **AR · REL · TRAIN · POST** | Contrasts task-relevant and distractor perception to improve grounding robustness before perceptual errors propagate into agent actions. |

### 2025-12

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2025-12-30 | [SenseNova-MARS: Empowering Multimodal Agentic Reasoning and Search via Reinforcement Learning](https://arxiv.org/abs/2512.24330) · [Code](https://github.com/OpenSenseNova/SenseNova-MARS) | **AR · TOOL · SEARCH · TWI-E · TRAIN · POST · INF** | Dynamically interleaves image search, text search, cropping, and reasoning. |
| 2025-12-30 | [RSAgent: Learning to Reason and Act for Text-Guided Segmentation via Multi-Turn Tool Invocations](https://arxiv.org/abs/2512.24023) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Trains a segmentation agent with SFT and agentic RL to inspect visual feedback, revise hypotheses, and refine masks. |
| 2025-12-27 | [CoAgent: Collaborative Planning and Consistency Agent for Coherent Video Generation](https://arxiv.org/abs/2512.22536) | **AR · AG-V** | Plans storyboards, maintains entity memory, verifies intermediate shots, and selectively regenerates failures. |
| 2025-12-26 | [VideoZoomer: Reinforcement-Learned Temporal Focusing for Long Video Reasoning](https://arxiv.org/abs/2512.22315) | **AR · TOOL · VID-R · TRAIN · POST · INF** | Learns to invoke temporal zoom from a coarse overview through reflection-trajectory SFT followed by reinforcement learning. |
| 2025-12-23 | [CRAFT: Continuous Reasoning and Agentic Feedback Tuning for Multimodal Text-to-Image Generation](https://arxiv.org/abs/2512.20362) | **AR · AG-I** | Decomposes constraints, verifies outputs with a VLM, repairs failures, and stops explicitly. |
| 2025-12-23 | [LongVideoAgent: Multi-Agent Reasoning with Long Videos](https://arxiv.org/abs/2512.20618) | **AR · TOOL · VID-R · TRAIN · POST · INF · BENCH** | Trains a master agent to coordinate grounding and vision agents efficiently and introduces episode-scale LongTVQA benchmarks. |
| 2025-12-21 | [InSight-o3: Empowering Multimodal Foundation Models with Generalized Visual Search](https://arxiv.org/abs/2512.18745) · [Code](https://github.com/m-Just/InSight-o3) | **AR · TOOL · TWI-E · TRAIN · POST · INF · BENCH** | Introduces O3-Bench and trains generalized interleaved visual search for documents, maps, diagrams, and real-world images. |
| 2025-12-19 | [Deep But Reliable: Advancing Multi-turn Reasoning for Thinking with Images](https://arxiv.org/abs/2512.17306) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF** | Trains reflective, self-correcting multi-turn visual-tool behavior with redundancy penalties. |
| 2025-12-19 | [CodeDance: A Dynamic Tool-integrated MLLM for Executable Visual Reasoning](https://arxiv.org/abs/2512.17312) · [Project](https://codedance-vl.github.io/) | **AR · TOOL · TWI-E · TWI-P · REL · TRAIN · POST · INF** | Uses executable code as a dynamic visual solver with runtime feedback and adaptive multi-step tool composition. |
| 2025-12-18 | [AdaTooler-V: Adaptive Tool-Use for Images and Videos](https://arxiv.org/abs/2512.16918) · [Code](https://github.com/CYWang735/AdaTooler-V) | **AR · TOOL · TWI-E · VID-R · REL · TRAIN · POST · INF** | Uses tool-benefit-aware rewards to invoke visual tools only when they improve image, multi-image, or video reasoning. |
| 2025-12-15 | [SAGE: Training Smart Any-Horizon Agents for Long Video Reasoning with Reinforcement Learning](https://arxiv.org/abs/2512.13874) | **AR · TOOL · VID-R · TRAIN · POST · INF · BENCH** | Learns when to answer directly or iteratively skim through RL post-training and evaluates flexibility with SAGE-Bench. |
| 2025-12-15 | [GTR-Turbo: Merged Checkpoint is Secretly a Free Teacher for Agentic VLM Training](https://arxiv.org/abs/2512.13043) | **AR · TOOL · REL · TRAIN · POST** | Merges intermediate policy checkpoints into a free teacher for dense guidance, reducing cost and entropy collapse in multi-turn RL. |
| 2025-12-13 | [VideoARM: Agentic Reasoning over Hierarchical Memory for Long-Form Video Understanding](https://arxiv.org/abs/2512.12360) | **AR · TOOL · VID-R · INF** | Runs an observe–think–act–memorize loop that builds hierarchical multimodal memory while exploring video coarse to fine. |
| 2025-12-09 | [Thinking with Images via Self-Calling Agent](https://arxiv.org/abs/2512.08511) · [Code](https://github.com/YWenxi/think-with-images-through-self-calling) | **AR · TWI-E · INF** | Decomposes a task into calls to parameter-shared virtual sub-agents. |
| 2025-12-08 | [DART: Leveraging Multi-Agent Disagreement for Tool Recruitment in Multimodal Reasoning](https://arxiv.org/abs/2512.07132) · [Code](https://github.com/nsivaku/dart) | **AR · TOOL · REL · INF** | Uses disagreement among visual agents to recruit expert tools and ground the subsequent debate in external evidence. |
| 2025-12-05 | [Active Video Perception: Iterative Evidence Seeking for Agentic Long Video Understanding](https://arxiv.org/abs/2512.05774) | **AR · TOOL · VID-R · REL · INF** | Treats video as an environment in which planner, observer, and reflector decide what, when, and where to inspect until evidence is sufficient. |
| 2025-12-05 | [Training Multi-Image Vision Agents via End2End Reinforcement Learning](https://arxiv.org/abs/2512.08980) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | IMAgent learns multi-image tool use through pure end-to-end RL with reflection tools and action–trajectory masking. |
| 2025-12-04 | [ARM-Thinker: Reinforcing Multimodal Generative Reward Models with Agentic Tool Use and Visual Reasoning](https://arxiv.org/abs/2512.05111) | **AR · TOOL · REL · TRAIN · POST · INF · BENCH** | Trains a reward model to crop images and retrieve document pages before judging, and introduces ARMBench-VL. |
| 2025-12-03 | [Thinking with Programming Vision: Towards a Unified View for Thinking with Images](https://arxiv.org/abs/2512.03746) · [Code](https://github.com/ByteDance-BandAI/CodeVision) | **AR · TOOL · TWI-P · INF** | Uses code as a universal visual-tool interface with composition and runtime error recovery. |
| 2025-12-03 | [EEA: Exploration-Exploitation Agent for Long Video Understanding](https://arxiv.org/abs/2512.03500) | **AR · SEARCH · VID-R · REL · INF** | Balances hierarchical tree exploration with semantic anchors and uncertainty-aware segment evaluation. |
| 2025-12-03 | [Multimodal Reinforcement Learning with Adaptive Verifier for AI Agents](https://arxiv.org/abs/2512.03438) | **AR · REL · TRAIN · POST** | Argos adaptively selects answer, localization, and process scorers for SFT curation and online RL, reducing reward hacking. |
| 2025-12-02 | [Skywork-R1V4: Toward Agentic Multimodal Intelligence through Interleaved Thinking with Images and DeepResearch](https://arxiv.org/abs/2512.02395) · [Code](https://github.com/SkyworkAI/Skywork-R1V) | **AR · TOOL · SEARCH · TWI-E · INF** | Unifies image operations and web research in long, planning-consistent tool trajectories. |
| 2025-12-02 | [WorldMM: Dynamic Multimodal Memory Agent for Long Video Reasoning](https://arxiv.org/abs/2512.02425) | **AR · SEARCH · VID-R · INF** | Iteratively chooses among episodic, semantic, and visual memories at multiple temporal scales until enough evidence is collected. |

### 2025-11

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2025-11-28 | [JarvisEvo: Towards a Self-Evolving Photo Editing Agent with Synergistic Editor-Evaluator Optimization](https://arxiv.org/abs/2511.23002) · [Code](https://github.com/LYL1015/JarvisEvo) · [Project](https://jarvisevo.vercel.app/) | **AR · TOOL · AG-I · REL · TRAIN · POST · INF** | Co-evolves editor and evaluator through tool selection, critique, reflection, and interleaved reasoning. |
| 2025-11-27 | [Revisiting the Necessity of Lengthy Chain-of-Thought in Vision-centric Reasoning Generalization](https://arxiv.org/abs/2511.22586) · [Code](https://github.com/RUCAIBox/Revisiting-Visual-CoT) | **TWI-E · REL · TRAIN · BENCH** | Finds that concise essential grounding traces can generalize better than lengthy textual or visual chains of thought. |
| 2025-11-26 | [Monet: Reasoning in Latent Visual Space Beyond Images and Language](https://arxiv.org/abs/2511.21395) · [Code](https://github.com/NOVAglow646/Monet) | **TWI-L · TRAIN** | Treats continuous embeddings as visual thoughts and directly optimizes the latent policy. |
| 2025-11-26 | [MIRA: Multimodal Iterative Reasoning Agent for Image Editing](https://arxiv.org/abs/2511.21087) | **AR · TOOL · AG-I · TRAIN · POST · INF** | Learns atomic editing loops whose next action is conditioned on visual feedback. |
| 2025-11-25 | [Agent0-VL: Exploring Self-Evolving Agent for Tool-Integrated Vision-Language Reasoning](https://arxiv.org/abs/2511.19900) · [Code](https://github.com/aiming-lab/Agent0) | **AR · TOOL · TWI-E · REL · TRAIN · POST · INF** | Unifies solver and verifier roles for tool-grounded self-evaluation, repair, and evolution. |
| 2025-11-25 | [LongVT: Incentivizing “Thinking with Long Videos” via Native Tool Calling](https://arxiv.org/abs/2511.20785) | **AR · TOOL · VID-R · REL · TRAIN · POST · INF · BENCH** | Trains native global-to-local video cropping through SFT, agentic RL, and RFT so answers remain grounded in revisited clips. |
| 2025-11-24 | [Chain-of-Visual-Thought: Teaching VLMs to See and Think Better with Continuous Visual Tokens](https://arxiv.org/abs/2511.19418) · [Code](https://github.com/Wakals/CoVT) · [Project](https://wakalsprojectpage.github.io/covt-website/) | **TWI-L · TRAIN** | Distills depth, edge, and segmentation experts into a short sequence of continuous visual tokens. |
| 2025-11-24 | [Scaling Agentic Reinforcement Learning for Tool-Integrated Reasoning in VLMs](https://arxiv.org/abs/2511.19773) · [Code](https://github.com/Lucanyc/VISTA-Gym) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Introduces an executable visual-tool gym and trains VISTA-R1 with multi-turn agentic RL. |
| 2025-11-24 | [CodeV: Code with Images for Faithful Visual Reasoning via Tool-Aware Policy Optimization](https://arxiv.org/abs/2511.19661) · [Code](https://github.com/RenlyH/CodeV) | **AR · TOOL · TWI-E · TWI-P · REL · TRAIN · POST · INF** | Rewards whether executable visual-tool outputs actually contain the required evidence rather than only rewarding final answers. |
| 2025-11-19 | [Octopus: Agentic Multimodal Reasoning with Six-Capability Orchestration](https://arxiv.org/abs/2511.15351) | **AR · TOOL · TWI-E · TWI-G · INF** | Dynamically selects among direct reasoning, visual tools, programming, and visual imagination. |
| 2025-11-18 | [Agentic Video Intelligence: A Flexible Framework for Advanced Video Exploration and Understanding](https://arxiv.org/abs/2511.14446) | **AR · TOOL · VID-R · REL · INF** | AVI uses a training-free Retrieve–Perceive–Review process, an entity-graph knowledge base, and multi-granular video tools. |
| 2025-11-15 | [GCAgent: Long-Video Understanding via Schematic and Narrative Episodic Memory](https://arxiv.org/abs/2511.12027) | **AR · VID-R · REL · INF** | Represents causal and temporal event structure in episodic memory and reasons through a perception–action–reflection cycle. |
| 2025-11-14 | [ImAgent: A Unified Multimodal Agent Framework for Test-Time Scalable Image Generation](https://arxiv.org/abs/2511.11483) | **AR · TWI-G · AG-I · INF** | Lets one model choose among reasoning, generation, and self-evaluation actions at test time. |
| 2025-11-07 | [DeepEyesV2: Toward Agentic Multimodal Model](https://arxiv.org/abs/2511.05271) · [Code](https://github.com/Visual-Agent/DeepEyesV2) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Learns to combine code execution and web search inside a unified reasoning loop. |
| 2025-11-06 | [Thinking with Video: Video Generation as a Promising Multimodal Reasoning Paradigm](https://arxiv.org/abs/2511.04570) · [Code](https://github.com/tongjingqi/Thinking-with-Video) | **TWI-G · AG-V · BENCH** | Frames generated video and frame sequences as dynamic reasoning media. |
| 2025-11-06 | [V-Thinker: Interactive Thinking with Images](https://arxiv.org/abs/2511.04460) · [Code](https://github.com/We-Math/V-Thinker) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Uses a data-evolution flywheel and progressive RL for long interactive visual reasoning. |
| 2025-11-03 | [TIR-Bench: A Comprehensive Benchmark for Agentic Thinking-with-Images Reasoning](https://arxiv.org/abs/2511.01833) | **AR · TOOL · TWI-E · BENCH** | Tests thirteen categories that require novel image-tool operations. |

### 2025-10

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2025-10-31 | [ToolScope: An Agentic Framework for Vision-Guided and Long-Horizon Tool Use](https://arxiv.org/abs/2510.27363) · [Code](https://github.com/dengmengjie/ToolScope) | **AR · TOOL · SEARCH · TWI-E · INF** | Separates global navigation, agentic tool execution, and response synthesis for long-horizon vision-guided workflows. |
| 2025-10-30 | [ThinkMorph: Emergent Properties in Multimodal Interleaved Chain-of-Thought Reasoning](https://arxiv.org/abs/2510.27492) · [Project](https://thinkmorph.github.io/) | **TWI-E · TWI-G · TRAIN · INF** | Shows progressive image manipulation, adaptive modality switching, and multimodal test-time scaling. |
| 2025-10-26 | [Open Multimodal Retrieval-Augmented Factual Image Generation](https://arxiv.org/abs/2510.22521) · [Project](https://tyangjn.github.io/orig.github.io/) | **AR · SEARCH · AG-I** | Iteratively plans text/image queries, filters evidence, checks sufficiency, and produces a generation-ready prompt. |
| 2025-10-25 | [Hollywood Town: Long-Video Generation via Cross-Modal Multi-Agent Orchestration](https://arxiv.org/abs/2510.22431) | **AR · AG-V** | Uses hierarchical graph orchestration, group discussion, bounded retries, and reflection. |
| 2025-10-20 | [UltraCUA: A Foundation Model for Computer Use Agents with Hybrid Action](https://arxiv.org/abs/2510.17790) | **AR · TOOL · ACT · TRAIN · POST · INF** | Learns when to switch between low-level GUI control and high-level programmatic tools. |
| 2025-10-19 | [VAGEN: Reinforcing World Model Reasoning for Multi-Turn VLM Agents](https://arxiv.org/abs/2510.16907) · [Code](https://github.com/mll-lab-nu/VAGEN) | **AR · ACT · WM · TRAIN · POST · INF** | Reinforces explicit visual world-model reasoning for partially observable, multi-turn agents acting in interactive environments. |
| 2025-10-17 | [VISTA: A Test-Time Self-Improving Video Generation Agent](https://arxiv.org/abs/2510.15831) · [Project](https://g-vista.github.io/) | **AR · AG-V** | Plans, generates, tournament-selects, critiques, and rewrites prompts across video iterations. |
| 2025-10-16 | [MathCanvas: Intrinsic Visual Chain-of-Thought for Multimodal Mathematical Reasoning](https://arxiv.org/abs/2510.14958) · [Code](https://github.com/shiwk24/MathCanvas) · [Project](https://mathcanvas.github.io/) | **TWI-G · TRAIN · BENCH** | Strategically generates and edits intermediate diagrams inside a unified model. |
| 2025-10-14 | [VideoLucy: Deep Memory Backtracking for Long Video Understanding](https://arxiv.org/abs/2510.12422) | **AR · SEARCH · VID-R · REL · INF · BENCH** | Backtracks through progressively finer memory until evidence is sufficient, while EgoMem evaluates fine-grained extreme-duration recall. |
| 2025-10-14 | [Beyond Seeing: Evaluating Multimodal LLMs on Tool-Enabled Image Perception, Transformation, and Reasoning](https://arxiv.org/abs/2510.12712) · [Data](https://huggingface.co/datasets/ScaleAI/VisualToolBench) | **AR · TOOL · TWI-E · BENCH** | VisualToolBench tests single- and multi-turn perception, image transformation, general tool use, and reasoning across 1,204 tasks. |
| 2025-10-13 | [CodePlot-CoT: Mathematical Visual Reasoning by Thinking with Code-Driven Images](https://arxiv.org/abs/2510.11718) · [Code](https://github.com/HKU-MMLab/Math-VR-CodePlot-CoT) | **TOOL · TWI-P · TRAIN** | Writes executable plotting code and feeds the rendering back as a visual thought. |
| 2025-10-06 | [VChain: Chain-of-Visual-Thought for Reasoning in Video Generation](https://arxiv.org/abs/2510.05094) · [Project](https://eyeline-labs.github.io/VChain/) | **TWI-G · AG-V** | Generates sparse consequence snapshots as a visual plan for video generation. |
| 2025-10-01 | [Training-free Uncertainty Guidance for Complex Visual Tasks with MLLMs](https://arxiv.org/abs/2510.00705) · [Code](https://github.com/ExplainableML/ug-framework) | **AR · TOOL · TWI-E · REL · INF** | Uses intrinsic uncertainty to decide where and when to acquire additional visual evidence without task-specific fine-tuning. |

### 2025-09

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2025-09-30 | [DeepSketcher: Internalizing Visual Manipulation for Multimodal Reasoning](https://arxiv.org/abs/2509.25866) | **TWI-L · TRAIN** | Produces native visual thoughts in embedding space without repeated external rendering. |
| 2025-09-29 | [Perceive, Verify and Understand Long Video: Multi-Granular Perception and Active Verification via Interactive Agents](https://arxiv.org/abs/2509.24943) | **AR · TOOL · VID-R · REL · INF** | CogniGPT couples adaptive perception granularity with multi-perspective visual verification to suppress hallucinated clues. |
| 2025-09-25 | [DeFacto: Counterfactual Thinking with Images for Enforcing Evidence-Grounded and Faithful Reasoning](https://arxiv.org/abs/2509.20912) · [Code](https://github.com/tinnel123666888/defacto) | **TWI-E · REL · TRAIN** | Trains answer consistency against relevant regions and counterfactual image edits. |
| 2025-09-17 | [PhysicalAgent: Towards General Cognitive Robotics with Foundation World Models](https://arxiv.org/abs/2509.13903) | **ACT · TWI-G · AG-V · WM** | Generates candidate trajectory videos, executes them, and replans after failure. |
| 2025-09-12 | [Maestro: Self-Improving Text-to-Image Generation via Agent Orchestration](https://arxiv.org/abs/2509.10704) | **AR · AG-I** | Orchestrates specialized critics, a verifier, and a judge for iterative prompt evolution and candidate selection. |
| 2025-09-09 | [Mini-o3: Scaling Up Reasoning Patterns and Interaction Turns for Visual Search](https://arxiv.org/abs/2509.07969) · [Code](https://github.com/Mini-o3/Mini-o3) · [Project](https://mini-o3.github.io/) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Scales visual search to dozens of turns with explicit exploration, backtracking, and goal retention. |
| 2025-09-09 | [CAViAR: Critic-Augmented Video Agentic Reasoning](https://arxiv.org/abs/2509.07680) | **AR · TOOL · VID-R · REL · INF** | Adds a critic that distinguishes successful from unsuccessful adaptive sequences of video-module calls. |
| 2025-09-08 | [Interleaving Reasoning for Better Text-to-Image Generation](https://arxiv.org/abs/2509.06945) · [Code](https://github.com/Osilly/Interleaving-Reasoning-Generation) | **TWI-G · AG-I · TRAIN** | Alternates text thought, initial generation, reflection, and image refinement. |
| 2025-09-02 | [UI-TARS-2 Technical Report: Advancing GUI Agent with Multi-Turn Reinforcement Learning](https://arxiv.org/abs/2509.02544) · [Code](https://github.com/bytedance/UI-TARS) | **AR · TOOL · ACT · TRAIN · POST · INF** | Unifies perception, reasoning, action, memory, and hybrid GUI/terminal interaction with multi-turn RL. |

### 2025-08

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2025-08-24 | [An LLM-LVLM Driven Agent for Iterative and Fine-Grained Image Editing](https://arxiv.org/abs/2508.17435) | **AR · TOOL · AG-I** | RefineEdit-Agent combines LVLM feedback with LLM planning and tool selection. |
| 2025-08-19 | [ComputerRL: Scaling End-to-End Online Reinforcement Learning for Computer Use Agents](https://arxiv.org/abs/2508.14040) · [Code](https://github.com/THUDM/ComputerRL) | **AR · TOOL · ACT · TRAIN · POST** | Scales online desktop RL and alternates RL/SFT to prevent policy-entropy collapse. |
| 2025-08-16 | [Simple o3: Towards Interleaved Vision-Language Reasoning](https://arxiv.org/abs/2508.12109) | **AR · TOOL · TWI-E · INF** | Encodes crop, zoom, and observation reuse inside interleaved observe–reason–act traces. |
| 2025-08-15 | [Thyme: Think Beyond Images](https://arxiv.org/abs/2508.11630) · [Code](https://github.com/yfzhang114/Thyme) · [Project](https://thyme-vl.github.io/) | **AR · TOOL · TWI-P · INF** | Autonomously writes and runs visual/computational code and reasons from sandbox feedback. |
| 2025-08-13 | [Seeing, Listening, Remembering, and Reasoning: A Multimodal Agent with Long-Term Memory](https://arxiv.org/abs/2508.09736) | **AR · VID-R · TRAIN · POST · INF · BENCH** | M3-Agent learns multi-turn reasoning over entity-centric episodic and semantic memory with RL and introduces M3-Bench. |
| 2025-08-13 | [Video-EM: Event-Centric Episodic Memory for Long-Form Video Understanding](https://arxiv.org/abs/2508.09486) | **AR · SEARCH · VID-R · REL · INF** | Constructs coherent event memories and self-reflects on evidence sufficiency, consistency, redundancy, and granularity. |
| 2025-08-12 | [OpenCUA: Open Foundations for Computer-Use Agents](https://arxiv.org/abs/2508.09123) · [Code](https://github.com/xlang-ai/OpenCUA) · [Project](https://opencua.xlang.ai/) | **AR · TOOL · ACT · TRAIN · POST · INF** | Builds end-to-end computer agents from reflective, long-horizon visual state–action trajectories. |
| 2025-08-11 | [MAViS: A Multi-Agent Framework for Long-Sequence Video Storytelling](https://arxiv.org/abs/2508.08487) | **AR · AG-V** | Coordinates script, shot, character, keyframe, animation, and audio agents with staged review. |
| 2025-08-09 | [Talk2Image: A Multi-Agent System for Multi-Turn Image Generation and Editing](https://arxiv.org/abs/2508.06916) | **AR · AG-I** | Decomposes intent and iteratively evaluates and revises generated images from multiple viewpoints. |
| 2025-08-08 | [SIFThinker: Spatially-Aware Image Focus for Visual Reasoning](https://arxiv.org/abs/2508.06259) · [Code](https://github.com/bytedance/SIFThinker) | **AR · TOOL · TWI-E · TRAIN · POST · INF** | Learns to propose, inspect, and correct spatial focus regions during reasoning. |
| 2025-08-07 | [WebWatcher: Breaking New Frontier of Vision-Language Deep Research Agent](https://arxiv.org/abs/2508.05748) | **AR · TOOL · SEARCH · TRAIN · POST · INF** | Uses synthetic multimodal trajectories and RL to bootstrap autonomous visual deep research. |
| 2025-08-06 | [Thinking With Videos: Multimodal Tool-Augmented Reinforcement Learning for Long Video Reasoning](https://arxiv.org/abs/2508.04416) | **AR · TOOL · VID-R · REL · TRAIN · POST · INF** | VITAL learns on-demand dense frame sampling and multimodal tool reasoning with multitask SFT and difficulty-aware GRPO. |
| 2025-08-06 | [TSPO: Temporal Sampling Policy Optimization for Long-form Video Language Understanding](https://arxiv.org/abs/2508.04369) | **AR · VID-R · TRAIN · POST · INF** | Jointly optimizes event-aware keyframe selection and answer generation with accuracy and temporal-localization rewards. |
| 2025-08-05 | [CoAct-1: Computer-using Multi-Agent System with Coding Actions](https://arxiv.org/abs/2508.03923) · [Code](https://github.com/SalesforceAIResearch/CoAct) | **AR · TOOL · ACT** | An orchestrator delegates subtasks between a visual GUI operator and a code programmer. |
| 2025-08-03 | [StreamAgent: Towards Anticipatory Agents for Streaming Video Understanding](https://arxiv.org/abs/2508.01875) | **AR · VID-R · INF** | Anticipates where and when future evidence will appear, adjusts perception proactively, and recalls history through hierarchical streaming memory. |

### 2025-07

| Date | Paper and resources | Tags | Why it matters |
|---|---|---|---|
| 2025-07-22 | [ThinkAct: Vision-Language-Action Reasoning via Reinforced Visual Latent Planning](https://arxiv.org/abs/2507.16815) · [Project](https://jasper0314-huang.github.io/thinkact-vla/) | **AR · ACT · TWI-L · TRAIN · POST · INF** | Learns a visually rewarded embodied plan, compresses it into latents, and uses it to drive action. |
| 2025-07-22 | [Zebra-CoT: A Dataset for Interleaved Vision Language Reasoning](https://arxiv.org/abs/2507.16746) · [Data](https://huggingface.co/datasets/multimodal-reasoning-lab/Zebra-CoT) | **TWI-G · TRAIN** | Provides 182K interleaved text–image reasoning trajectories across science, space, robotics, and games. |

<!-- PAPER_TIMELINE_END -->

## Selection notes

- Dates refer to the first public arXiv version (`v1`), not the latest revision date.
- A paper must make agency or visual intermediate states part of the method, training objective, or evaluation target—not merely mention agents or multimodal reasoning.
- `POST` requires explicit optimization of an interaction, tool/search, active-perception, memory, reflection, or verifier policy; ordinary answer-only multimodal fine-tuning is not enough.
- `INF` requires a primary contribution in active test-time planning, evidence seeking, tool orchestration, scaling, speculative execution, adaptive compute allocation, verification, or stopping; ordinary execution of a learned policy is not enough.
- `VID-R` covers active video understanding and evidence seeking. Generated video used as simulation or imagination remains under `TWI-G`/`WM`; `VID-R · AG-V` is reserved for systems that both reason over video evidence and generate or edit video.
- Application papers are included only when they introduce a reusable agentic/visual-reasoning mechanism.
- Withdrawn papers are excluded from the main timeline. In particular, [MATRIX](https://arxiv.org/abs/2510.08567) is not listed because the arXiv record was withdrawn over attribution and comparison concerns.
- Important foundations released before the window—such as [Visual Agentic Reinforcement Fine-Tuning](https://arxiv.org/abs/2505.14246), [Agent-X](https://arxiv.org/abs/2505.24876), [Active-O3](https://arxiv.org/abs/2505.21457), and [VideoDeepResearch](https://arxiv.org/abs/2506.10821)—are intentionally not counted.
- The list is curated rather than claimed to be mathematically exhaustive. Please open an issue or pull request for a missing paper that meets the scope and date window.

## Contributing

Please include the title, first-public date, paper link, optional project/code link, a one-sentence contribution summary, and the relevant tags. Keep entries sorted by date and avoid links to secondary paper aggregators when a primary source is available.
