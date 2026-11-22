# VPS for AI Agent Hosting: How Much RAM You Actually Need, What the Monthly Bill Really Covers, and Which Ava Hosting Plan Fits OpenClaw, Hermes Agent or Ollama (Full Plan Table)

A VPS for an AI agent needs to do three things: stay on while your laptop sleeps, give you root so you can install whatever the agent needs, and carry enough RAM for the runtime plus its memory store. Two vCPU and 4 GB is the working floor for Hermes Agent, n8n, LibreChat, AnythingLLM and Coolify. OpenClaw wants 4 vCPU and 8 GB before it behaves.

Then there is the second bill. The server is infrastructure. The model behind the agent is usually an API from OpenAI, Anthropic or OpenRouter, billed per token by that company. Running open-weight models on the box itself removes the token line and moves the cost into RAM and disk.

Ava Hosting sells the plain version of this: root KVM VPS in one Moldovan datacenter, priced in euros, with the 2 vCPU / 4 GB plan at €10/month as displayed. Below is which of its seven plans clears which app's published minimum, what the full monthly cost looks like once the model is paid for, and the setup mistakes that cost people a weekend.

> **Most readers:** Ava Hosting VPS Basic (2 vCPU / 4 GB / 50 GB NVMe) at €10/month. It meets the published minimum for Hermes Agent, n8n, LibreChat, AnythingLLM, Coolify and Portainer.
> **Running OpenClaw, or a local model you actually use:** VPS Power (4 vCPU / 8 GB / 90 GB) at €20/month.
> 👉 [Compare Ava Hosting's VPS plans and the price each one is listed at](https://my.ava.hosting/aff.php?aff=15562)

## The full Ava Hosting lineup

Seven plans sit on the VPS/VDS store page, all of them full-root KVM with a control panel, NVMe storage, ECC RAM on Intel Xeon E5 hardware, unlimited traffic, free DDoS protection, weekly backups, a 99.9% uptime SLA and 24/7 support. The port is 1 Gbps except on the smallest plan, which is listed at 100 Mbps. The entry plan's listing also notes that port 25 is closed, which matters if your agent is supposed to send mail.

| Plan | vCPU · RAM · NVMe | Price as displayed | What it fits | Order |
| --- | --- | --- | --- | --- |
| VPS Nano | 1 · 512 MB · 20 GB | €11/year (100 Mbps) | WireGuard, a jump host, a status page | [VPS Nano](https://my.ava.hosting/aff.php?aff=15562) |
| VPS One | 1 · 2 GB · 25 GB | €5/month | Portainer, Webmin, one small bot | [VPS One](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Basic | 2 · 4 GB · 50 GB | €10/month | Hermes Agent, n8n, LibreChat, AnythingLLM | [VPS Basic](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Lucky ✪ | 2 · 6 GB · 70 GB | €15/month | the 4 GB apps plus Postgres and a reverse proxy | [VPS Lucky](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Power ☆ | 4 · 8 GB · 90 GB | €20/month | OpenClaw, Ollama with a model you keep loaded | [VPS Power](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Extra ☆ | 6 · 12 GB · 120 GB | €30/month | several agents, subagent fan-out, larger local models | [VPS Extra](https://my.ava.hosting/aff.php?aff=15562) |
| VPS Ultra ☆ | 8 · 16 GB · 160 GB | €40/month | parallel workloads, team-scale memory | [VPS Ultra](https://my.ava.hosting/aff.php?aff=15562) |

Every price in that table is a "starting from" figure in EUR as the store page shows it. Billing cycle and tax change the number at checkout, and the smallest plan is listed as 0 available, so treat it as a catalog entry rather than something you can order today.

Two other things on the site worth knowing before you compare prices anywhere else. First, a separate "Self-hosted Start" order flow lists six packages from €2/month, with an identical vCPU and RAM ladder and slightly different storage at the top end: 4 vCPU / 8 GB / 100 GB at €20 there, against 90 GB for VPS Power in the store. Compare the storage line if you land on that page. Second, the same flow advertises a free trial without spelling out its terms, so ask support what it covers and how long it runs.

## How much server does each agent actually need?

Start from the app, not the plan. The minimums below are published by a provider that ships one-click installers for all of these, which makes them vendor sizing numbers rather than guesses:

| What you're running | Published minimum | Plan that clears it |
| --- | --- | --- |
| OpenClaw | 4+ vCPU, 8+ GB RAM | VPS Power (4 / 8) |
| Hermes Agent | 2+ vCPU, 4+ GB RAM | VPS Basic (2 / 4) |
| AnythingLLM | 2+ vCPU, 4+ GB RAM | VPS Basic |
| LibreChat | 2+ vCPU, 4+ GB RAM | VPS Basic |
| Ollama + Open WebUI | 2+ vCPU, 4+ GB RAM (models want more) | VPS Basic to start, VPS Power for real use |
| n8n | 2+ vCPU, 2+ GB (4 GB with Postgres + AI tools) | VPS Basic |
| Coolify | 2+ vCPU, 2+ GB (4 GB with databases and proxy) | VPS Basic |
| AdminBolt | 2 vCPU, 2 GB, on AlmaLinux 9 | VPS Basic |
| Portainer | 1+ vCPU, 2+ GB | VPS One |
| WireGuard (wg-easy) | 1+ vCPU, 1+ GB | VPS One |
| Webmin, CyberPanel | 1+ vCPU, 1+ GB | VPS One |

The same floor shows up elsewhere. QuantVPS, which sells to people running coding agents around the clock, tells customers to take at least 4 vCPU / 8 GB and installs Ubuntu 24.04. That is exactly where OpenClaw's minimum lands, and it is why the €20 tier rather than the €10 one is the honest recommendation for OpenClaw.

Two rows in that table deserve a second look. n8n and Coolify both run on 2 GB, and both vendors suggest 4 GB once you add a database, a reverse proxy and AI tool calls to the same box. Paying €5 more for VPS Lucky's 6 GB buys you room you will otherwise spend an evening debugging. Ollama is the other trap: the published minimum gets the service running, but model weights live in RAM, so the minimum is where you start, not where you stay.

👉 [See the 4 vCPU / 8 GB VPS Power plan in Ava Hosting's store](https://my.ava.hosting/aff.php?aff=15562)

## Hermes the model is not Hermes Agent

Search results blur these two, and the confusion changes your RAM budget. Hermes is a family of open-weight models from Nous Research: Hermes 3 is the current line, Hermes 4 is rolling out alongside it, and older variants such as Hermes 13B are still in use. Hermes Agent is a separate product from the same group. It keeps memory across sessions, schedules tasks, hands work to subagents and calls tools to browse, read files and run code.

What you install on a VPS is the Agent. The model it talks to is either an API call or weights you load on the same machine. An Agent pointed at an API fits comfortably in 4 GB. An Agent plus local weights does not.

## The other half of the bill

Server rental buys infrastructure and nothing else. IONOS states it plainly on its Hermes page: the monthly VPS plan covers the server, while external models such as GPT-4 or Claude are billed separately, typically on your own API key. QuantVPS says the same thing about model subscriptions and API fees. Contabo advertises a flat monthly bill for the server and still leaves model choice, and model cost, to you.

That splits buyers into two groups with different bottlenecks. If your agent calls a hosted model, the server is small and cheap, the token bill scales with how busy the agent is, and a 4 GB plan is genuinely enough. If you load open weights on the box, tokens are free but RAM and disk decide what you can run, and CPU inference is slow enough that a €10 plan is a test bench rather than a worker.

Agents that wake on a cron schedule make this harder to predict than a chatbot. A weekly digest job and an always-on gateway with a memory index cost very different amounts per month.

👉 [Start with the 2 vCPU / 4 GB VPS Basic plan if your agent uses an API](https://my.ava.hosting/aff.php?aff=15562)

## Installation: what Ava Hosting doesn't do for you

Ava Hosting's pages describe root access, a control panel and Docker support. They do not advertise a one-click catalogue of AI apps, GPU plans or a prebuilt Hermes image. Plan on installing over SSH: Node or Docker, the agent runtime, a process manager, a reverse proxy if the agent has a web UI.

That makes one warning relevant even though it comes from a different provider. RackNerd documents that its one-click installer reinstalls the OS before deploying, takes roughly 15 to 45 minutes, and erases whatever was on the server: operating system, applications, files. Any control panel OS reload behaves the same way. Do the reinstall once, on an empty box, before you load data or hand the agent any credentials. Weekly backups are included with every Ava plan, but confirm with support what a restore actually covers before you rely on it.

## Unmanaged means the defaults are yours

Full root is the point of a box like this, and it also means nobody patches it for you. Three things to settle in the first hour: SSH keys instead of password login, a firewall that exposes only the ports the agent needs, and API keys stored in environment variables rather than committed to a repo.

Watch the web UI defaults as well. IONOS documents that its Hermes image ships with HTTP Basic Auth where the username is `admin` and the password is the server's root password. That puts the highest-privilege credential on the box behind a browser login. If your install arrives with anything similar, change the password or put the UI behind a reverse proxy with its own auth before you point a domain at it.

## How Ava Hosting compares with the AI-branded VPS crowd

| Provider | Entry price as displayed | What stands out | What to check |
| --- | --- | --- | --- |
| IONOS | from $2/month (1 vCore, 2 GB, 60 GB NVMe) | Hermes installable at checkout, 99.99% uptime, 30-day money-back guarantee | upgrades only, no downgrade to a smaller plan; models billed separately |
| Contabo | 4 vCPU / 8 GB / 100 GB at €4.40/month for the first 24 months | one-click Hermes add-on, 9 regions | a footnote on the same page calls the figure a 12-month effective rate including tax; the two statements conflict, so confirm the term |
| QuantVPS | from $39.99/month | 99.999% uptime SLA, New York, dedicated CPU and RAM | priced for that SLA; 4 vCPU / 8 GB recommended for coding agents |
| Bluehost | self-managed VPS with one-click Hermes | NVMe 2 graded A for performance stability by VPSBenchmarks in a February 2026 trial | infrastructure-only support |
| Ava Hosting | VPS Basic at €10/month (2 vCPU, 4 GB, 50 GB) | root, 1 Gbps, unlimited traffic, weekly backups, 99.9% SLA, one flat euro price | no AI app catalogue, one location |

The €2 IONOS number buys the smallest tier, not a production Hermes host, and its own page notes that you should be comfortable with SSH, Docker and securing the server yourself. Contabo's promotional rate is the cheapest way to 8 GB on this list by a wide margin, which is why the 24-month and 12-month wording on that page matters.

## Quick answers

**Does an AI agent VPS need a GPU?** Not if the model is a hosted API. A GPU starts to matter when you run inference on the same server, and none of Ava Hosting's plans include one.

**Can OpenClaw run on the €10 plan?** No. It lists 4 vCPU and 8 GB as its minimum, which is VPS Power at €20. Buying the €10 box and hoping is how people end up reinstalling a week later.

**What is a 512 MB plan for?** WireGuard, a jump host, a status page. Not an agent runtime.

## Which plan to buy

- A tunnel, a dashboard, or a single lightweight bot: **VPS One**, €5/month.
- Hermes Agent, n8n, LibreChat, AnythingLLM, Coolify or Portainer: **VPS Basic**, €10/month.
- Adding Postgres, a reverse proxy and a memory index to the same box: **VPS Lucky**, €15/month, for the extra 2 GB.
- OpenClaw, or Ollama with a model you keep loaded: **VPS Power**, €20/month.
- Multiple agents, subagent fan-out, or local models past the small ones: **VPS Extra** at €30 or **VPS Ultra** at €40.

Two things to confirm on the order page before you pay. The billing period and price you'll actually be charged matter more than the headline rate: a third-party plan catalogue's price check records the 1 vCPU / 2 GB plan at $4.18/month effective on a 12-month commitment ($50.14 upfront) against $4.91/month on a one-month term, while Ava's own store displays €5/month for the same tier. Different currencies, different tax treatment, so read the total at checkout rather than the monthly figure.

The second is the RAM floor for the app you're installing. If you're on OpenClaw, that floor is 8 GB; if you're on Hermes Agent with an API key, 4 GB does the job and the €10 plan is the right buy.

👉 [Pick your plan and start the install on Ava Hosting's VPS store](https://my.ava.hosting/aff.php?aff=15562)
