---
name: docsmith
description: Use when writing, editing, or reviewing any project document — PRD, architecture spec, API doc, README, deployment guide, changelog, user guide, test plan, ADR, or any technical writing for websites or apps. Triggers: write doc, write documentation, write README, write PRD, write spec, write guide, edit doc, review doc, technical writing, 写文档, 写技术文档, 写PRD, 写README, 写架构文档, 写接口文档, 写部署文档, 写用户手册.
---

# Docsmith

Craft project documentation that reads like a human engineer wrote it. No AI slop. No hallucinated claims. Strong structure with diagrams and tables. Works for any website or app project regardless of tech stack.

<IRON-LAWS>

These rules are absolute. No exceptions. No "but this case is different."

**LAW 1 — EVIDENCE BEFORE CLAIMS.** Every technical claim must originate from verifiable source: actual code, official docs, or user-provided spec. Never fabricate API names, parameter types, config keys, library versions, benchmark numbers, or URLs. If unverifiable, mark `[UNVERIFIED — needs source]` or remove.

**LAW 2 — HUMAN VOICE ONLY.** Active voice with a human subject. Address the reader as "you." Vary sentence length deliberately — mix 5-word punches with 30-word explanations. No metronomic rhythm. No filler openers. No promotional adjectives.

**LAW 3 — VISUAL FIRST.** Every 2-3 content sections must include at least one visual element: Mermaid diagram, comparison table, flowchart, or architecture graph. Text is the last resort when a picture truly can't convey it.

**LAW 4 — VERIFY OR REMOVE.** If you cannot prove a technical fact, mark it `[UNVERIFIED]` or cut it. This covers API names, version numbers, config keys, performance numbers, third-party behavior, and URLs.

</IRON-LAWS>

## Core Writing Principles

1. **Lead with the point.** First sentence of every section states what the reader will learn or do. No throat-clearing ("In this section, we will explore...").

2. **One idea per sentence. One topic per paragraph.** 2-4 sentences per paragraph max. If a paragraph exceeds 4 sentences, split it.

3. **Concrete over abstract.** "The login endpoint accepts POST with JSON body containing `email` and `password`" beats "The authentication module handles user credentials."

4. **Delete filler ruthlessly.** If a word doesn't change meaning, remove it. "Use" > "utilize." "Start" > "commence." "Show" > "demonstrate."

5. **Tech-stack agnostic.** Describe the role, not the tool. "The frontend framework" not "React." "The database layer" not "PostgreSQL." Only name specific tech when the document explicitly requires it (setup guides, dependency lists).

6. **Write for scanning.** Engineers skim before they read. Put the answer first, context second. Use headings that state conclusions ("Auth tokens expire after 24h" not "About Token Expiration").

## Document Router

Match the user's request to a document type. Read TEMPLATES.md for the structural spec of each type.

```
User needs to document...
│
├─ WHAT to build and why
│  ├─ Features + acceptance criteria → PRD (product-requirements)
│  ├─ Business goals + scope → Project Brief (project-brief)
│  └─ Specific capability → Feature Spec (feature-spec)
│
├─ HOW it works architecturally
│  ├─ System overview + component diagram → Architecture Doc (architecture-doc)
│  ├─ Why we chose X over Y → ADR (adr)
│  ├─ Endpoint contracts + request/response → API Spec (api-spec)
│  └─ Schema + relationships + indexing → Database Design (database-design)
│
├─ HOW to build / use
│  ├─ Project overview + setup → README (readme)
│  ├─ Team conventions + style rules → Coding Standards (coding-standards)
│  ├─ Step-by-step learning journey → Tutorial (tutorial)
│  └─ How to do a specific thing → How-To Guide (howto-guide)
│
├─ HOW to ship / operate
│  ├─ Deploy steps + rollback → Deployment Guide (deployment-guide)
│  ├─ What changed in this version → Changelog (changelog)
│  ├─ Testing strategy + scope → Test Plan (test-plan)
│  └─ Runbook + monitoring + escalation → Operations Manual (ops-manual)
│
├─ HOW to use (end user)
│  ├─ First steps in 5 minutes → Quick Start (quickstart)
│  ├─ Complete usage reference → User Guide (user-guide)
│  └─ Common problems + fixes → FAQ (faq)
│
└─ REFLECTION
   ├─ What happened + lessons → Post-Mortem (postmortem)
   └─ Knowledge transfer → Handover Doc (handover)
```

If the user's description doesn't map cleanly, ask one question to clarify intent. Don't guess.

## Writing Workflow

### Step 1 — IDENTIFY

Determine document type from the router. Identify:
- **Audience**: who reads this (new hire? end user? API consumer? ops engineer?)
- **Scope**: what's covered and what's explicitly NOT covered
- **Evidence sources**: code, configs, existing docs, user-provided specs

### Step 2 — OUTLINE

Build the skeleton from TEMPLATES.md. Mark visual element positions:
- `[TABLE: ...]` — what data the table compares
- `[DIAGRAM: mermaid type — ...]` — what the diagram illustrates
- `[CALLOUT: note|warning|tip — ...]` — critical information

### Step 3 — DRAFT

Write section by section. Follow the core writing principles. Consult PATTERNS.md for the banned vocabulary and structural tells. Key rules:

- No banned opener in the first sentence of any section
- Vary sentence length: after 2-3 long sentences, drop a short one
- Every code block shows expected output or result
- No "In this document/article/section..." meta-commentary

### Step 4 — VISUALIZE

Insert diagrams and tables at marked positions. Rules:

| Visual Type | Use When | Format |
|---|---|---|
| Architecture diagram | Showing system components + connections | `mermaid graph TD` or `graph LR` |
| Sequence diagram | Showing request/response flows between actors | `mermaid sequenceDiagram` |
| Flowchart | Decision trees, branching logic, workflows | `mermaid flowchart` |
| State diagram | Entity lifecycle, status transitions | `mermaid stateDiagram-v2` |
| Comparison table | Comparing options, features, parameters | Markdown table with header row |
| ER diagram | Database schema, entity relationships | `mermaid erDiagram` |
| Class diagram | Module/component structure + interfaces | `mermaid classDiagram` |
| Gantt chart | Timelines, project schedules | `mermaid gantt` |
| Callout box | Warnings, tips, critical notes | `> **Warning:**` or `> **Tip:**` |

Every visual must have a caption and be referenced in surrounding text. Never drop a diagram without context.

### Step 5 — RED-TEAM VERIFY

This step is MANDATORY. Skipping it is a violation.

**Pass 1: Pattern Scan.** Read PATTERNS.md. Scan the document for every banned pattern. Fix or rewrite flagged content.

**Pass 2: Hallucination Check.** For every technical claim:
- Can you point to the source (code line, doc URL, config file)?
- If no → mark `[UNVERIFIED]` or remove
- Pay extra attention to: API names, parameter types, default values, version numbers, third-party behavior, performance claims

**Pass 3: Rhythm Check.** Read the document aloud (or simulate). Flag:
- 3+ consecutive sentences with similar length (±3 words) → rewrite some
- 3+ consecutive paragraphs starting the same way → restructure
- Any sentence that sounds like a motivational poster → delete

**Pass 4: Completeness.** Check against the template in TEMPLATES.md. All required sections present? All visual elements inserted? All cross-references valid?

## Anti-Pattern Quick Reference

| If you catch yourself writing... | You're doing this wrong | Do this instead |
|---|---|---|
| "In today's rapidly evolving..." | Throat-clearing | Delete. Start with the fact |
| "It's worth noting that..." | Filler | Delete. Just state the thing |
| "Leverage / Harness / Utilize" | Corporate buzzword | Use / Start / Show |
| "Not X, but Y" | Binary contrast formula | Just state Y |
| "This is more than X; it's a Y" | Grandiosity | State what it does, stop |
| "Seamlessly / Robust / Cutting-edge" | Empty adjective | Delete or give metrics |
| "赋能 / 端到端 / 一站式" | Chinese corporate buzzword | Say what it actually does |
| "在当今...的背景下" | Chinese throat-clearing | 删除，直接说事实 |
| "值得注意的是" | Chinese filler | 删除，直接陈述 |
| "不仅...而且..." | Chinese binary contrast | 直接说结论 |
| Every sentence is 15-20 words | Metronomic rhythm | Mix 5-word and 35-word sentences |
| "Developers should..." | Distant narration | "You..." |
| "The configuration was updated" | Passive voice | "We updated the configuration" |
| "..., emphasizing/highlighting..." | Dangling participle tail | Start a new sentence |

## Hallucination Defense

Technical claims by risk level and verification tactic:

| Claim Type | Risk | Verification Tactic |
|---|---|---|
| API name / endpoint | HIGH | Check actual source code or official docs |
| Parameter type / default value | HIGH | Check schema definition or type declaration |
| Library version compatibility | HIGH | Check package manifest or release notes |
| Performance number | HIGH | Must come from actual benchmark — never fabricate |
| Third-party behavior | MEDIUM | Check official documentation URL |
| Config key / env variable | MEDIUM | Check actual config file or .env example |
| URL / link | MEDIUM | Verify URL exists and points to claimed content |
| Architecture behavior | LOW | Inferable from code structure, but still verify |
| General concept definition | LOW | Common knowledge, but don't fabricate quotes |

**The UNVERIFIED protocol:** When you cannot verify a claim but believe it may be correct:
1. Mark it: `[UNVERIFIED — needs source: reason]`
2. Suggest how the user can verify: "Check `path/to/file` or see `https://...`"
3. Never present unverified content as fact

## Red Flags — STOP and Verify

These thoughts mean you're about to produce AI slop:

| Thought | Reality |
|---|---|
| "This draft looks clean enough" | Run PATTERNS.md scan. "Looks clean" is how slop ships |
| "The reader won't notice" | They will. AI patterns are instantly recognizable |
| "I'll verify technical details later" | Later never comes. Verify now or mark UNVERIFIED |
| "This sentence sounds professional" | "Professional" is often a mask for "corporate buzzword" |
| "Let me add a summary paragraph" | Documents don't need summaries. Each section states its point |
| "I should explain what X is before using it" | If the reader doesn't know X, link to docs. Don't pad |
| "This needs more detail to be thorough" | More words ≠ more thorough. More specifics does |
| "Let me add a diagram to look professional" | Diagrams serve the reader, not your appearance |
| "I'll use a filler transition to flow better" | Good writing doesn't need transitions between sections |
| "The user didn't specify tech stack, I'll pick a common one" | Tech-agnostic by default. Name tech only when required |

## Language-Specific Rules

### English

- Contractions OK: it's, you'll, we're, don't
- Sentence case for headings: "Getting started" not "Getting Started"
- Oxford comma: "Android, iOS, and Windows"
- One space after periods
- Target 10-25 words per sentence

### Chinese (中文)

- 短句优先：一句话一个意思，平均15-25字
- 禁止翻译腔："关于...的问题" → 直接说问题
- 用具体名词代替笼统词："处理" → 具体动作（校验/存储/转发）
- 禁止无意义前缀："关于"、"对于"、"就...而言" → 删除
- 主动语态："该配置被修改了" → "我们修改了该配置"
- 避免"的"字堆叠：连续3个"的"必须改写
- 技术术语保留英文原文：不翻译 "API"、"endpoint"、"middleware"

## Quality Metrics

Before declaring a document complete, check:

| Metric | Target |
|---|---|
| Average sentence length | 10-25 words (EN) / 15-25 chars (ZH) |
| Max consecutive similar-length sentences | 2 |
| Paragraph length | 2-4 sentences |
| Visual elements per major section | ≥ 1 (diagram or table) |
| Code blocks with expected output | 100% |
| Banned pattern hits (per PATTERNS.md) | 0 |
| UNVERIFIED claims | Flagged with source suggestion |
| Filler content ratio vs AI baseline | Reduced ≥ 50% |
| Headings state conclusions (not topics) | ≥ 80% |

## Final Checklist

Before delivering any document:

- [ ] PATTERNS.md scanned — zero banned patterns remain
- [ ] Sentence rhythm varies — no 3+ consecutive similar-length sentences
- [ ] All technical claims verified or marked [UNVERIFIED]
- [ ] All diagrams/tables present and referenced in text
- [ ] No throat-clearing openers in any section
- [ ] Headings state conclusions, not just topics
- [ ] Tech-stack agnostic (specific names only where required)
- [ ] Document matches template structure from TEMPLATES.md
- [ ] Every code block has expected output or result
- [ ] Document would pass the "read aloud" test — sounds like a human talking
