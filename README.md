# Sylvio Faneva Randrianarisata

**AI systems engineer — agent tooling, context engineering, MCP.**
Antananarivo, Madagascar · UTC+3 · taking on remote contracts.

---

**[Portfolio →](https://claude.ai/code/artifact/216d894b-cdc6-4d02-83be-3cb3d6c85f2c)** — the same
work written up properly, with my push_swap replaying its own instruction stream and my FdF renderer
compiled to WebAssembly and running in the page.

I build the layer agents run on, and I have the systems background to know what that layer has to
guarantee. Anyone can generate code in 2026; almost nobody is building the part that keeps generated
code coherent at month six.

### Archit — what I am building now

A SaaS I have been building alone since March 2026. Every generation tool improvises architecture as
it goes: fine for a weekend, ruinous at scale. Archit makes the architecture an interrogable, validated
source of truth **before** generation, then exports it into the language each tool speaks — MCP first,
plus Prisma, OpenAPI and the rest.

Five months in, and the discipline is the point:

| | |
|---|---|
| **96 numbered architecture decisions** | each one supersedes or amends the ones before it, by number, with its rationale — `§94` retires `§85`'s Redis lock, `§96` amends `§79` |
| **Five non-negotiable Laws** | *Align before you build* · Single Schema Truth · Intent Layer · validation at every boundary · tests in the same commit |
| **A cascade rule** | when one decision changes, every dependent document changes in the same commit — a spec that drifts from its own decisions is worse than no spec |
| **Determinism as a contract** | canonical JSON, domain-separated SHA-256, and golden fixtures compared **byte for byte** between the TypeScript and Python sides |
| **Fail-closed by default** | an unresolvable risk manifest blocks generation rather than waving it through |

One decision that shows how I think: I removed a Redis lock from the concurrency protocol and replaced
it with a compare-and-swap on the aggregate, with leases and epochs — because **a lock with a timeout
is not a fence**. An expired holder can still write. That distinction is the difference between a
system that looks correct and one that is.

I also run contradictory reviews against my own drafts and record the verdict, including when the
verdict kills a position I had already written down.

### Context engineering — the part most people leave implicit

On a codebase this size the bottleneck is not generation, it is **context**. Sending everything is not
the same as remembering everything: past a threshold, more context makes a model measurably worse. So
I engineered it rather than hoped.

- **Cold context** — loaded every session: the five Laws, the decision index, the project in thirty seconds.
- **Hot context** — only what the current step needs, reached through **symbolic links**, so nothing
  else is even *reachable*. Control over reachability beats instructions that ask politely.
- **Windows bounded by tokens**, not by number of turns.
- **Tail placement**, because attention sags in the middle of long inputs.
- Grounded in the research — context rot (Chroma, 2025) and lost-in-the-middle (Liu, 2023) — not in blog posts.
- **MCP-first**: four endpoints, plus `/archit-bootstrap` and `/archit-step` so that starting a step is
  a reproducible operation instead of an improvisation.
- Multi-provider routing through LiteLLM, chosen per task complexity rather than per habit.

The architecture and the judgement are mine. What is accelerated is the typing.

### The systems underneath

I completed the full Common Core at **[42 Antananarivo](https://42antananarivo.mg/)**, where the curriculum bans frameworks and
external libraries. You do not import the thing — you write it.

| Project | What it is |
| --- | --- |
| **[webserv](https://github.com/SylvioRand/webserv)** | An HTTP/1.1 web server in C++98 — single-threaded non-blocking event loop over `poll()`, virtual hosts, chunked transfer, file uploads, CGI execution, and an NGINX-inspired configuration parser. |
| **[minishell](https://github.com/SylvioRand/minishell)** | A working Unix shell in C — hand-written lexer and parser for quotes, redirections, heredocs and arbitrary-length pipelines, with bash-accurate signal handling and exit statuses. |
| **[push_swap](https://github.com/SylvioRand/push_swap)** | Sorting a stack through eleven permitted instructions, optimised for the fewest operations — my own cost model rather than a borrowed algorithm. A median of 3 853 operations on 500 values, where full marks stop at 5 500. |
| **[FdF](https://github.com/SylvioRand/fdf)** | A 3D wireframe renderer in C — hand-written Bresenham rasterisation, transformation matrices, isometric and front projections. MiniLibX gives me one pixel; everything between a text file and a picture is mine. |
| **[CASA](https://github.com/SylvioRand/ft_transcendence-42)** | My capstone: a property marketplace for the Malagasy market, with AI tooling that lets a buyer describe what they want in their own words instead of filling in a filter form. **I was tech lead of the five.** I owned `services/listings` end to end and built the whole front end for `reservation`, plus `auth`, the NGINX routing, the compose file, the React pages, French/English localisation and the documentation the other four worked from. **243 of the 953 commits are mine**, second of five contributors. |
| **[Inception](https://github.com/SylvioRand/inception)** | Docker infrastructure built from base images only — NGINX terminating TLS 1.2/1.3, WordPress on PHP-FPM, MariaDB, dedicated network, persistent volumes. |
| **[Philosophers](https://github.com/SylvioRand/philosophers)** | Concurrency under tight timing: POSIX threads and mutexes, no data race, no deadlock, no starvation. |

*webserv, minishell and CASA are team projects; my contribution is described in each repository's README.*

Five ranked exams, all passed — taken alone, on the clock, offline, graded by a harness that either
accepts your program or does not. **The pass mark is 100**, so those are passes, not distinctions. What
separates a transcript is the projects, where 100 is where you are *allowed* to stop and 125 means the
bonus was built and defended as well. I have **ten at 125**.

The early exercises the curriculum is built on — the C standard library, `printf` and its variadic
parsing, buffered line reading, bit-level IPC over UNIX signals, the C++98 modules — are **private on
purpose**, so current 42 students cannot lift them. Happy to share on request.

### Built for someone else

**[info-connectee](https://github.com/SylvioRand/info-connectee)** — a digital newspaper written by a
class of ten-year-olds. A primary-school teacher described what she wanted her pupils to be able to do;
turning that into technical decisions was the whole job. I chose Hugo deliberately and against my own
preferences: a static site means free hosting, no database to administer, no dependency to patch, and
articles that live in markdown files the teachers edit themselves. It has been running through a school
year without me.

### Working with

`Python` · `TypeScript` · `C` · `C++98/11` · `Bash` · MCP · LiteLLM · `pgvector` · `PostgreSQL` ·
`Redis` · `BullMQ` · `Hono` · `Bun` · `FastAPI` · `Next.js` · `Docker` · `NGINX` · `Linux`

Agent tooling and context engineering on codebases large enough for it to matter; and underneath that,
sockets and non-blocking I/O, POSIX processes and threads, memory management without a garbage
collector, HTTP internals, TLS termination, and the kind of debugging where the bug is three layers
below the language.

---

<picture>
  <source media="(max-width: 520px)" srcset="assets/card-narrow.svg">
  <img src="assets/card.svg" alt="Sylvio Faneva Randrianarisata — AI systems engineer, Antananarivo, UTC+3" width="880">
</picture>

### Work with me

Native French and Malagasy, professional English. UTC+3 gives a full working-day overlap with Europe
and a solid morning overlap with US eastern time.

**randrianarisatasylvio@gmail.com**

I take on remote contracts: agent tooling and context engineering, backend and systems work, and
projects that want their architecture settled before the first line of code.

**Open to proposals.**
