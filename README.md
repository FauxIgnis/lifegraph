# lifegraph
# LifeGraph OS: Integrated System Architecture

LifeGraph OS operates as a distributed, browser-native cognitive virtual machine. At the computational foundation, WebGPU provides high-throughput parallel execution for neural and tensor workloads, while WebAssembly hosts high-performance kernels for graph transforms, cryptographic operations, and other non-tensor compute. Where available, WebNN and ONNX Runtime Web extend this layer by routing neural workloads to device-specific accelerators such as GPUs and NPUs, supporting models exported from heterogeneous training frameworks. Each browser node thus becomes a fully local, hardware-accelerated AI runtime.

Above this compute substrate, orchestrated domain-specific Small Language Models function as the cognitive engine. Executed primarily through Transformers.js and ONNX Runtime Web, and coordinated by an agent runtime inspired by LangGraph-style state machines, these models treat each browser as a resident cognitive process. To support immediate responsiveness across heterogeneous devices, the cognitive layer is organized into a tiered model runtime: a resident micro-model provides continuous low-latency inference for intent routing and structural reasoning, while larger SLMs are streamed in quantized, sharded form via a Service Worker and persisted in IndexedDB or the Origin Private File System. This ensures that more capable models are progressively activated without blocking interaction, allowing the system to adapt dynamically to available compute, memory, and user preferences.

At the orchestration level, LifeGraph OS adopts a TypeScript-native, worker-parallel execution model in which cognitive operations are decomposed into independent functional units executed across Web Workers, WASM kernels, and GPU-backed operators. These modular units are coordinated through a graph-defined controller that schedules, sequences, and aggregates their outputs as a distributed set of cooperating capacities. Each operation is executed as a bounded, resumable step, with intermediate states persisted into the semantic graph and local storage, enabling complex workflows to progress incrementally and resume deterministically after suspension, throttling, or tab lifecycle events. This orchestration layer allows the system to distribute cognitive load across multiple lightweight workers rather than relying on a monolithic model loop, increasing throughput and ensuring predictable behaviour under browser constraints.

At the data layer, the GUN.js peer-to-peer graph extended with SEA for identity, integrity, and access control serves as the connective substrate. All system state is represented as a CRDT-replicated, freely mutating memory graph: a continuously evolving semantic structure in which nodes, edges, and higher-order patterns can be created, reconnected, rewritten, or pruned by both human inputs and cognitive operations. To maintain long-term stability, the temporal dimension of this graph is implemented as a dual-channel history system. Fine-grained edits flow through an append-only operation log segmented into temporal epochs, while a background compaction process driven by a dedicated Worker periodically replays closed epochs into stable semantic snapshots and compressed deltas stored in OPFS. This preserves verifiability, convergence, and version navigation while preventing unbounded growth of low-level mutation history.

Knowledge ingestion sits directly on this substrate. TipTap acts as the canonical structured document layer: external files such as PDF, DOCX, HTML, and Markdown are transformed into TipTap JSON blocks and mapped into the memory graph as composable, linkable semantic units. Obsidian-like views render this graph as a navigable web of documents, concepts, and relationships, exposing to the user the same structure that the models operate over. Firecrawl functions as the external knowledge acquisition engine, crawling and extracting structured web data and converting it into the same graph-native TipTap format whenever the system requires context beyond the user’s local corpus.

For large artifacts, long-lived models, or immutable knowledge modules, LifeGraph OS can anchor data in content-addressed storage layers such as IPFS. In this configuration, the memory graph references stable content hashes rather than heavyweight binaries, allowing the system to adopt a compute-over-data pattern in which cognitive functions execute on nodes that hold the relevant data rather than replicating content globally.

Together, these layers form a unified, mutation-capable cognitive architecture in which compute, reasoning, orchestration, data synchronization, ingestion, and semantic memory operate as an integrated system inside the browser. Each user device participates as a node of a decentralized virtual machine whose freely mutating memory graph can grow, reorganize, and accumulate patterns over years, functioning as both a second brain for the human and a research substrate for emergent digital cognition.

# User Interface Architecture

The UI layer of LifeGraph OS is designed as a single unified command surface centered entirely around a chat-first main page. All system functionality is accessed through natural-language commands, making the interface act as the user’s primary cognitive terminal. Around this central surface, only a minimal set of modular components are invoked on demand, without sidebars, dashboards, or separate application zones.

The Node component serves as a Universal Canvas. Instead of maintaining separate file types, the canvas adapts fluidly to the content being created. Documents, spreadsheets, presentations, and imported files become different manifestations of the same semantic canvas, capable of rendering text, tables, diagrams, timelines, or slides in a single continuous environment. This eliminates conceptual fragmentation and mirrors the behavior of the underlying mutating memory graph.

The Connector component integrates a GUN.js-based universal messenger with real-time translation, media exchange, and shareable video/audio rooms. It embeds collaborative task and calendar management directly into nodes so that responsibilities and events become graph-linked annotations rather than isolated items. Communication, coordination, and collaboration therefore occur natively within the same semantic substrate.

The Explorer component operates both as an AI-driven course generator and as a Perception Mode: an epistemic lens that overlays explanations, dependencies, knowledge gaps, and learning paths onto the user’s knowledge graph. In this mode, the user can directly perceive how their memory graph is structured, which regions are strong or weak, and what learning trajectories the system recommends, transforming exploration from a static content-generation process into a dynamic cognitive experience.

All components converge into the chat interface, forming a unified cognitive command center where writing, communication, planning, learning, and creation occur within a single continuous semantic field. This integration is reinforced by the system-wide temporal spine. LifeGraph OS maintains a Git-like chronological record of every thought process, interaction, edit, and graph mutation, treating each change as a semantic commit. Users can navigate through time as well as meaning, replaying the evolution of ideas, branching into alternative drafts or conceptual paths, and merging divergent developments with the assistance of agents. Over long periods, this temporal structure forms a version-controlled cognitive archive where the complete history of the user’s mindspace becomes navigable, inspectable, portable, and preservable.

LifeGraph OS inherits the core advantages of decentralized architecture. Because all computation runs on the user’s own device and all state is maintained through peer-to-peer CRDT replication, the system has no central servers, no backend infrastructure, and therefore no operational scaling costs even at global scale. Hosting requires only a static build of the application, which can be mirrored indefinitely at negligible expense. This also makes the platform structurally resilient: with no central point of control and no server-side dependencies, the system is extremely difficult to block or censor. LifeGraph OS remains accessible and functional as long as users can access a browser, making it a robust, cost-free, and globally persistent cognitive environment by design.

# Open Source Technology Stack Reference:
Core Compute Layer:
WebGPU: https://github.com/gpuweb/gpuweb
WebAssembly (Binaryen): https://github.com/WebAssembly/binaryen
WebNN: https://github.com/webmachinelearning/webnn
ONNX Runtime Web (ONNX ecosystem): https://github.com/onnx/onnx

Model & Cognitive Layer:
Transformers.js: https://github.com/huggingface/transformers.js
ToolOrchestra (reference but in TS):https://github.com/NVlabs/ToolOrchestra

Distributed Data Layer:
GUN.js: https://github.com/amark/gun
IPFS: https://github.com/ipfs/ipfs

Document & Semantic Layer:
TipTap: https://github.com/ueberdosis/tiptap
Obsidian (reference): https://github.com/obsidianmd

Knowledge Ingestion:
Firecrawl: https://github.com/firecrawl/firecrawl

UI Runtime Supporting Technologies:
WebRTC (reference): https://github.com/webrtc
WebSockets (reference): https://github.com/websockets/ws
WebCodecs (reference/spec): https://github.com/WICG/web-codecs
WebComponents: https://github.com/WICG/webcomponents

Local Persistence:
IndexedDB (reference/spec): https://github.com/w3c/IndexedDB

Worker-Based Concurrency:
Service Workers (spec reference): https://github.com/w3c/ServiceWorker
Web Workers (spec reference): https://github.com/w3c/webappsec

Identity & Trust Layer:
Decentralized Identifiers (DID): https://github.com/w3c/did-core

CRDT Ecosystem References:
Automerge: https://github.com/automerge/automerge
Yjs: https://github.com/yjs/yjs
Hypercore Protocol: https://github.com/holepunchto/hypercore

WASM Performance Extensions:
WASM SIMD & Threads (reference): https://github.com/WebAssembly/simd

Explorer:
Roadmap.sh (reference): https://github.com/kamranahmedse/developer-roadmap/tree/master
