# Sylvio Faneva Randrianarisata

**AI systems engineer — agent tooling, context engineering, MCP.**
Antananarivo, Madagascar · UTC+3 · taking on remote contracts.

---

**[Portfolio →](https://claude.ai/code/artifact/216d894b-cdc6-4d02-83be-3cb3d6c85f2c)** — the same
work written up properly, with my push_swap replaying its own instruction stream and my FdF renderer
compiled to WebAssembly and running in the page.

I build the layer agents run on, and I have the systems background to know what that layer has to
guarantee. Generating code is easy now. Keeping a codebase coherent at month six is the harder problem.

### Archit — what I am building now

A SaaS I have been building alone since March 2026. Every generation tool improvises architecture as it
goes: fine for a weekend, ruinous at scale. Archit makes it an interrogable, validated source of truth
**before** generation, then exports it into the language each tool speaks — MCP first. The repository is
private while it is a commercial product; the discipline is the part worth showing:

| | |
|---|---|
| **96 numbered decisions** | each supersedes or amends the ones before it, by number — `§94` retires `§85`'s Redis lock |
| **Five non-negotiable Laws** | *Align before you build* · Single Schema Truth · Intent Layer · validation at every boundary · tests in the same commit |
| **A cascade rule** | change one decision and every dependent document changes in the same commit |
| **Determinism as a contract** | golden fixtures compared **byte for byte** between the TypeScript and Python sides |
| **Fail-closed** | an unresolvable risk manifest blocks generation rather than waving it through |

What `§94` actually did: I removed a Redis lock from the concurrency protocol and replaced it with a
compare-and-swap on the aggregate, with leases and epochs — because **a lock with a timeout is not a
fence**. An expired holder can still write. That is the difference between a system that looks correct
and one that is.

### Context engineering — the part most people leave implicit

The bottleneck is not generation, it is **context**: past a threshold, more of it makes a model
measurably worse. So I engineered it rather than hoped.

- **Cold** — loaded every session: five Laws, the decision index, the project in thirty seconds.
  **Hot** — only what the current step needs, reached through **symbolic links**, so nothing else is
  even *reachable*. Controlling reachability beats instructions that ask politely.
- Windows bounded by **tokens, not turns**, with the step's own documents placed at the **tail**,
  because attention sags in the middle. From the research on context rot and lost-in-the-middle, not blog posts.
- **MCP-first** — four endpoints, plus `/archit-bootstrap` and `/archit-step`, so starting a step is a
  reproducible operation rather than an improvisation.

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

**Languages** — `C` · `C++98/11` · `Python` · `TypeScript` · `Bash`
**Agents & retrieval** — MCP · context engineering · LiteLLM · ChromaDB · `pgvector` · sentence-transformers
**Systems** — sockets · `poll` · pthreads · HTTP internals · TLS · Linux
**Services & data** — `PostgreSQL` · `Redis` · Hono on Bun · FastAPI · Next.js · Docker · NGINX

Underneath all of it: non-blocking I/O, POSIX processes and threads, memory management without a
garbage collector, and the kind of debugging where the bug is three layers below the language.

---

<picture>
  <source media="(max-width: 520px)" srcset="assets/card-narrow.svg">
  <img src="assets/card.svg" alt="Sylvio Faneva Randrianarisata — AI systems engineer, Antananarivo, UTC+3" width="880">
</picture>

### Work with me

Native French and Malagasy, professional English. UTC+3 gives a full working-day overlap with Europe
and a solid morning overlap with US eastern time.

**randrianarisatasylvio@gmail.com**

Agent tooling and context engineering, backend and systems work, and projects where getting the
architecture right actually matters.

**Available for remote contracts.**
