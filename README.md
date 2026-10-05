# Chris Kim

Senior backend engineer, seven years in. I build identity, access, and
data-protection systems for other engineers and API consumers.

At Capital One I work on identity and access management. I enforce access
across 50,000+ employees and 4,000+ AWS accounts, run OAuth and JWT
service-to-service auth, rotate secrets through Vault and AWS Secrets
Manager, and designed credential propagation with a 500/day revocation cap
and a staging queue, so one bad rotation cannot revoke everything at once.
Before IAM I worked on data retention, and before that on account ingestion,
where I reimplemented a Java service in Go and sustained 2.4k req/s in load
testing.

Go is my primary language. Outside work I pick a workflow that annoys me and
build the whole toolchain to replace it.

## Projects

**job-search.** A multi-tenant job search platform: ATS ingest,
resume-variant scoring, referral-gated applications, and outcome analytics.
The Next.js layer owns no database. It mints a short-lived service token for
an internal Go API, and that API owns the entire schema. The repo holds 69
migrations, 150 test files, and custom go-ruleguard lint rules that have
tests of their own. Go, Next.js, Neon Postgres, and a FastAPI embedding
sidecar. Source is private.

**[seakim-design-system](https://github.com/christophercuongkim/seakim-design-system).**
One platform-neutral rule set, proven by a React binding and a Flutter
binding. It carries 38 numbered decision records and 41 React components.
Each binding declares which rules version it was reviewed against, and a
binding may lag that version but never lead it. CI runs a conformance
self-test that checks every rule fires on a bad fixture and stays quiet on a
good one, so the gate cannot pass while doing nothing. Four of my other repos
consume it.

**[studio](https://github.com/christophercuongkim/studio).** Every stage of a
personal video in one static Go binary: script, shoot, ingest, review,
rename, scaffold a kdenlive project, generate chapters, run QC, build
thumbnails, upload, and archive. It also searches across every shoot I have
ingested. The binary is 12,660 lines of Go and depends on four third-party
modules, with no CLI framework, no web framework, and no database. Three web
UIs compile in through `go:embed`. Every destructive command takes
`--dry-run`, and `apply` writes a journal so `undo` works.

**[fantasy-hub](https://github.com/christophercuongkim/fantasy-hub).** NFL
fantasy analytics. A FastAPI service runs projections and simulation, Neon
Postgres holds the hot tier, DuckDB queries Parquet for the cold tier, and d3
draws the charts. It ingests from the Yahoo Fantasy API and runs at
[fantasy.chriskim.cloud](https://fantasy.chriskim.cloud).

**Juntio.** Group trip planning: chat, propose and vote on plans, build a
shared itinerary, and split expenses. One Flutter codebase covers iOS,
Android, and web, over a Go backend and Postgres. TestFlight releases run on
manual dispatch, because macOS runner minutes bill at roughly ten times the
Linux rate. It runs at [juntio.io](https://juntio.io). Source is private.

**[dotfiles](https://github.com/christophercuongkim/dotfiles).** NixOS on a
Framework 13, built on the flake-parts dendritic pattern so hosts and
features compose as separate modules. Hyprland, Ghostty, tmux, and Neovim.

**[zmk-config](https://github.com/christophercuongkim/zmk-config).** Firmware
for a wireless split Corne. It defines five layers and two custom devicetree
hold-tap behaviors, raises Bluetooth transmit power, and sets a one-day idle
timeout. CI builds the flashable artifacts.

## How I work

I write no ORM in Go. Queries are hand-written SQL with sqlc codegen, and
`sqlc diff` runs in CI so the generated code cannot drift from the schema.

Every repo opens with `direnv allow`. I maintain twelve hand-written Nix
flakes with pinned versions, and each one lists the manual-install
equivalents for people who do not run Nix.

I deploy to Dokploy on a VPS, and the deploy webhooks answer only inside a
Tailscale tailnet. GitHub Actions joins that tailnet as an ephemeral,
ACL-tagged node using OAuth client credentials, because GitHub's own webhooks
cannot reach a private address.

Each project carries a `CONTEXT.md` that defines its domain terms, and every
term lists the words not to use for it.

I write comments that give the reason and the number behind it. The comment
explaining why CI splits into separate api and web jobs sits next to the
measurement that forced the split: 75% of the repository's Actions minutes
went to the api job.

## Background

I am finishing an M.S. in Cybersecurity at NYU. I hold a B.S. in Computer
Science from Cal Poly San Luis Obispo and the AWS Solutions Architect
Associate certification.

My OS coursework paper proposes detecting kernel credential and namespace
struct tampering with BPF-LSM, event-driven rather than polled. Its
limitations section states plainly where the watcher itself can be attacked.

## Now

I am looking for senior backend and platform roles where another engineer or
an API consumer is the customer. Remote within the United States, or on-site
in San Francisco.

Reach me on [LinkedIn](https://www.linkedin.com/in/christophercuong/).
