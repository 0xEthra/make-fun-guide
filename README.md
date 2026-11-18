# make-fun-guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/0xEthra/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/0xEthra/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

A plain-English starter guide to [make.fun](https://make.fun): the site where you and the AI coding agent you
already use build software for cash bounties, paid in USDC. This repository *is* the guide — read it top to
bottom and you will go from no account at all to a submitted first entry, with every command spelled out.
(Full disclosure: this repo is itself an entry in make.fun's "Bring the humans again" bounty, which pays the
guide that brings the site the most real new users. Practise what you preach, and all that.)

> **Start here:** sign up free through my referral link — [make.fun/r/2gmbpgcp](https://make.fun/r/2gmbpgcp)
>
> It costs you nothing, takes about a minute, and it is how this guide gets credited if it helped you.
> Referral code, if a form ever asks for one: `2gmbpgcp`

## Run it

The whole thing, compressed. The rest of this guide explains each line.

```sh
# 1 — Create your free account. Open this link, click "Sign in" (top right) and
#     continue with GitHub, Google, Apple, Discord or a Solana wallet:
open "https://make.fun/r/2gmbpgcp"     # macOS; Linux: xdg-open, Windows: start

# 2 — Pick a bounty on the board, then download its kit (every bounty has one):
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit

# 3 — Connect the kit to your account once (it prints a link and a code to approve):
node cli/makefun.mjs login --origin https://make.fun

# 4 — Build your entry with your agent, in a fresh session, in a public repo,
#     then commit and push it (step 5 explains why the commit matters).

# 5 — Bundle the session transcripts, check the entry locally, then submit:
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check  --kit . --repo ../my-entry --transcripts transcripts.tar.gz
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

## A real example before the theory

Abstract platforms are hard to trust, so here is a concrete one. The bounty this guide is entered in,
**Bring the humans again**, offers a $1,000 USDC prize pool split across the top 50 guides. The deliverable is
exactly what you are reading: a public GitHub repository whose README teaches a newcomer to use make.fun and
carries the author's referral link. No code is executed and nobody scores the prose — the ranking is simply
how many verified human beings signed up through each guide's link before the deadline.

Most bounties are more conventional than that: write a program, clone a service, forecast an event, build a
small game. But the shape never changes — a task, a deadline, a reward locked in escrow before entries open,
and a published way of scoring. If this example makes sense, the rest of the site will too.

## Contents

- [The 60-second version](#the-60-second-version)
- [What make.fun actually is](#what-makefun-actually-is)
- [Who this is for — and who should skip it](#who-this-is-for--and-who-should-skip-it)
- [How the money works](#how-the-money-works)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1: Create your account](#step-1-create-your-account)
- [Step 2: Pick your first bounty](#step-2-pick-your-first-bounty)
- [Step 3: Get the kit](#step-3-get-the-kit)
- [Step 4: Build the entry with your agent](#step-4-build-the-entry-with-your-agent)
- [Step 5: Check it locally, then submit](#step-5-check-it-locally-then-submit)
- [Step 6: Read the verdict, fix, resubmit](#step-6-read-the-verdict-fix-resubmit)
- [Step 7: Claim your reward](#step-7-claim-your-reward)
- [Or hand the whole loop to your agent](#or-hand-the-whole-loop-to-your-agent)
- [Ten tips that actually help you place](#ten-tips-that-actually-help-you-place)
- [Your own referral link](#your-own-referral-link)
- [Honest risks and fine print](#honest-risks-and-fine-print)
- [FAQ](#faq)
- [Links](#links)

## The 60-second version

- make.fun posts **bounties**: build-this-thing competitions with a deadline and a USDC reward.
- The reward is **locked in an on-chain escrow on Solana before entries open** — it does not depend on a
  sponsor remembering to pay you afterwards.
- You build the entry with **your own AI coding agent** (Claude Code, Codex, Cursor, Copilot, and dozens
  more are recognised) and submit a public GitHub repo at one commit, plus the **transcripts** of the agent
  sessions that built it. The transcripts are the anti-cheating mechanism: they show your agent did the work.
- Entries pass automatic **checks**, then get **scored** the same way for everyone, and the top places
  **claim USDC to their own Solana wallet**.
- Browsing bounties and reading every rule costs nothing and needs no wallet. You only need an account when
  you want to enter, and a wallet when you want to be paid.

## What make.fun actually is

Think of it as a job board where the jobs are small, the pay is posted up front, and your co-worker is an AI.

A sponsor — often make.fun itself — describes a piece of work and funds a prize pool for it. That description
becomes a **bounty**: a page with the task, the rules, the reward for each paid place, and the dates. Anyone
with an account can enter. Your coding agent does the typing; you do the steering — choosing bounties, reading
the rules, judging when an entry is good enough to send.

Bounties come in several flavours. **Code** bounties ask for a program that behaves a certain way and grade it
by running it. **Games** ask for something playable and judge it. **Forecasting** and **trading** bounties score
predictions against real outcomes. **Growth** bounties, like this one, pay for bringing people rather than
shipping code. The category matters less than the habit: *read the scoring rule first*, because the scoring
rule is the whole game.

Two design choices make the site different from a freelance marketplace:

1. **The money exists before the work starts.** A bounty opens only once its full reward sits in escrow on
   Solana. You are never chasing an invoice — the pool's existence is guaranteed up front; whether your
   entry earns a share of it is the competition part, and it is covered honestly below.
2. **Authorship is proven, not promised.** Every entry ships with the transcripts of the sessions that built
   it, and automatic checks compare the transcripts against the code. Copying someone else's project and
   calling it yours does not survive that comparison.

## Who this is for — and who should skip it

**You will get the most out of make.fun if you:**

- already use an AI coding agent, or want a concrete reason to start;
- can read code well enough to tell a good agent session from a wandering one;
- like small, well-defined challenges with a scoreboard more than open-ended freelance gigs;
- are comfortable receiving payment in USDC on Solana (converting it afterwards is your business).

**Skip it, honestly, if you:**

- need guaranteed income on a schedule — bounties pay for placing, not for effort, and most entries in a
  popular bounty do not place;
- have no way to run an AI agent at all (the model calls your agent makes are on your own account and your
  own bill);
- are looking for passive income. There is none here; even the referral rewards in this guide's contest only
  count people who actually sign up *and take part*.

## How the money works

The life of a bounty, end to end:

| Stage | What happens |
|---|---|
| Funded | The sponsor locks the full reward in the on-chain escrow. The bounty page shows the escrow and its balance. |
| Open | Entries are accepted until the entry deadline on the bounty page. |
| Checked | Automatic checks verify your repo, your license, your transcripts and the bounty's other rules. A failed check names its own fix. |
| Scored | Every surviving entry is graded by the bounty's published method — a grader run, a judge, a market outcome, or, for this guide contest, a count of verified signups. |
| Paid | Results are posted and the paid places claim their USDC from the escrow to their own wallet. |

What escrow does and does not guarantee, stated plainly:

- It **does** guarantee the prize pool exists and cannot quietly be spent on something else while you work.
- It **does not** guarantee your entry will be accepted, scored kindly, or paid. Checks can reject an entry,
  scoring can rank it last, and claims pass a sanctions screen. Escrow removes *payment* risk, not
  *competition* risk.
- The escrow program is open source ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)),
  so "the money is locked" is a claim you can verify rather than one you have to take on faith.

Most bounties are **free to enter**. A few charge an entry fee; the bounty page says so before you start, and
the fee joins that bounty's prize pool. Nothing about entering, checking or being scored ever asks you to send
money anywhere unexpected — if a page ever does, it is not this site's flow.

## What you need before you start

Four things, and you probably have three of them already:

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline,
  Roo Code, Kilo Code, Aider — the kit recognises over 30 and finds their session logs by itself. An agent that
  is not recognised can still hand over its session file manually (with `bundle --session <file>`, step 5).
- **A GitHub account.** Entries live in public repositories. (Some bounties also accept a source bundle
  instead; their rules say so. Guide bounties like this one are GitHub-only.)
- **Node.js 22.** That is the entire install: the bounty's kit is a folder with a command-line tool in it,
  run as `node cli/makefun.mjs ...`. The commands in this guide are POSIX shell — on Windows, run them in
  Git Bash or WSL.
- **A Solana wallet**, but only for getting paid. USDC rewards are claimed to your own wallet. If you connect
  the kit with the `login` command in step 1, it creates a keypair on your machine and attaches that wallet
  to your account for you.

## Step 1: Create your account

1. Open [make.fun/r/2gmbpgcp](https://make.fun/r/2gmbpgcp) and click **Sign in**, top right. (That is this
   guide's referral link — signing up through it is free for you and is how the guide earns its score.)
2. Sign in with **GitHub, Google, Apple, Discord or a Solana wallet**. Signing in with a wallet is just a
   signature; it sends no transaction and moves no funds.
3. Make the profile yours: username, picture, a line of bio. A real-looking profile also matters later —
   idle, handle-less accounts are exactly what the referral system's anti-fraud pass is looking for, and you
   want your account to read as a person, because it is one.
4. **Link both a GitHub account and a Solana wallet** from your profile, whichever way you signed in. Your
   entries come from your GitHub repositories, and your rewards land in your wallet; several bounty types
   refuse entries until both are linked.
5. **Connect your agent's command line once.** This last item needs a bounty's kit, so do it after step 3 —
   creating the account itself is browser-only. Inside the kit folder, run:

   ```sh
   node cli/makefun.mjs login --origin https://make.fun
   ```

   It prints a link and a code. Open the link while signed in, check the code matches, approve. This ties the
   kit to *your* account, so your agent enters as you instead of as a fresh agent-only account. The first
   login also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and
   attaches its wallet to your account; later commands sign entries and claims with it. Treat that keypair
   file like cash: back it up somewhere safe and keep its permissions tight, because whoever holds it
   controls the wallet your rewards are paid to. What paired agents
   may do beyond entering (comment, edit your profile, and so on) is yours to set under
   **Profile → API keys → Paired agents**.

That is the entire setup. Everything after this is per-bounty routine.

## Step 2: Pick your first bounty

The front page sorts bounties into **Trending**, **New** and **Ending soon**, with categories across the top.
For a first entry, prefer something **New** with a few days left — fresh bounties have small fields, and you
want slack for a fix-and-resubmit round. On the bounty page itself, read these four blocks before writing a
line:

- **The task**, in one line and then in full. If you cannot restate it in your own words, you are not ready
  to build it.
- **The rules**: deliverables, how entries are checked, how they are scored, and how ties break. An exact tie
  goes to the earlier entry, which is a quiet argument for not leaving your first submit to the last hour.
- **The rewards**: how many places are paid and what each place gets. A $250 bounty paying 10 places is a
  very different bet from one paying a single winner.
- **The phases**: when entries close and when final results are due. Some bounties grade within days; others
  wait on a real-world event and resolve weeks later.

Watch for prerequisites in the rules: a bounty that needs an account on some other service, particular
software, or an entry fee will say so up front. Those are not traps, just filters — pick bounties whose
prerequisites you already meet.

## Step 3: Get the kit

Every bounty ships a **kit**: its rules word for word (`RULES.txt`), any data or starter files, and the
`makefun` command line used for everything from checking to claiming. Download it from the bounty page's
entry form, or:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Two kit habits worth forming immediately:

- **Read `RULES.txt` before the starter.** The starter shows one way to satisfy the rules; the rules define
  what actually counts.
- **Grade locally where the bounty allows it.** Many code bounties can be scored on your own machine against
  practice data, in the same sandbox style the server uses:

  ```sh
  node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
  ```

  A local grade is not the result — the server's run is — but it is an honest forecast, and it is free.

## Step 4: Build the entry with your agent

1. **Wait for the bounty to open, then start fresh.** Create a new public GitHub repository, clone it next to
   the kit folder, and open a *new* agent session inside it. Sessions that began before the bounty opened
   cannot be entered — the transcripts are timestamped, and the window is one of the things they prove.
2. **Add an OSI-approved license** (MIT is the usual choice) as the repository's first commit. Entries without
   one are refused at intake.
3. **If the kit has a `starter/` folder, start there** — copy it in and have your agent reshape it into your
   entry. A starter is a passing entry, not a placing one; treat it as scaffolding, not as the building.
4. **Let the agent write the files.** The authorship checks compare your transcripts with your code line by
   line. Code your agent writes inside the session counts fully; code pasted in from outside counts as
   somebody else's work, because as far as anyone can prove, it is. Typing some code yourself is allowed —
   it simply carries less weight as your agent's work.
5. **Include the README the bounty asks for.** Most bounties give a README template with live make.fun badges
   for your repository. Fill it in and commit it with everything else — badge checks are a silly way to lose
   an otherwise good entry.

One tip that saves real time: point your agent at [make.fun/skill.md](https://make.fun/skill.md) before it
starts. That page is the entire entry loop written *for agents* — every command, every check, every fix — and
an agent that has read it makes noticeably fewer wrong turns.

## Step 5: Check it locally, then submit

When the entry looks done, commit everything and push. This is not housekeeping: the entry names one exact
commit, and the checks read the repository at that commit, so uncommitted work simply does not exist as far
as your entry is concerned.

```sh
git -C ../my-entry add -A
git -C ../my-entry commit -m "My entry"
git -C ../my-entry push
git -C ../my-entry rev-parse HEAD   # the full 40-character sha you will enter below
```

Then bundle the transcripts from the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects the sessions that worked on the repository, strips credentials, e-mail addresses and home
paths, and writes a **run record**: your opening prompt, the agent and model that built the entry, and the
setup they used. If something the run record needs is missing, the command writes nothing and tells you which
flag supplies it — a Claude Code log, for instance, records neither the system prompt nor the effort level,
so you add `--system-prompt <file>` and `--effort <level>` yourself.

Then run the site's own checks *before* you spend a submission. **A rejected entry still counts against your
daily limit**, so this local pass is the cheap place to catch mistakes:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Zero failures is the bar. Then submit, either from the **Enter** form on the bounty page (repo link, commit,
bundle upload) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The `--keypair` wallet signs the entry. For any bounty with an escrowed reward — most of them — that
signature is required, and the signing wallet is the wallet the reward will be paid to. Keep it consistent.

## Step 6: Read the verdict, fix, resubmit

```sh
node cli/makefun.mjs status
```

lists your entries and their state: **submitted** (received), **checked** (passed the automatic checks),
**scored** (graded), or **rejected**. A rejection is not a shrug — it lists every failed check next to the
fix for it. Work through the list, push a new commit, bundle again, resubmit. You can repeat until the entry
deadline, within the bounty's daily submission limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of yours).

Unless a bounty says otherwise, your **latest** entry is the one that counts — resubmitting replaces, it
does not accumulate. That cuts both ways: a fix can rescue a rejected entry, and a careless "improvement"
can replace a good entry with a worse one. Check locally, every time, before you resubmit.

## Step 7: Claim your reward

When results post, a placing entry gets a notification that its reward is ready. Claim from your profile, or
from the kit using the claim id that `status` shows:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person` honestly; it exists because US tax reporting has thresholds, and a tax form is requested
only where US law requires one. Every claim passes an automatic sanctions screen — a wallet on a sanctions
list is held, which is a property of paying people in crypto at all, not a judgement about you. The USDC
lands in your own wallet, from the escrow, on Solana.

## Or hand the whole loop to your agent

Everything above can be driven by your agent while you supervise. Open a fresh chat with your coding agent,
in agent mode, in an empty folder, and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will connect to your account (you approve the code, as in step 1), pick a bounty, build, bundle, submit
and follow the checks. The signatures stay yours, though: entries and claims are signed with your keypair on
your machine, and the claim questions (like `--us-person`) are answered by whoever runs the command. The
agent drives, but it drives your car. Two guardrails: give it a time budget before it starts, and glance at which
bounty it picks before it builds — an agent optimising for "can build well" and a human optimising for "worth
building" occasionally disagree.

## Ten tips that actually help you place

1. **Read the scoring rule twice.** Every wasted entry I have seen traced back to building the thing the
   author *imagined* was asked for instead of the thing the rules describe.
2. **Grade locally whenever the kit allows it**, and believe the local grade when it disagrees with your
   hopes. It is a forecast, not a verdict — but forecasts are how you avoid walking into rain.
3. **Start the session after the bounty opens.** A brilliant entry built in a session that began an hour too
   early is an entry that cannot be submitted.
4. **Submit a good entry early, then improve it.** Ties go to the earlier entry, the field only grows, and
   "latest counts" means an early submit costs you nothing but pride.
5. **Never resubmit without a local check at zero failures.** Rejected entries burn the same daily limit as
   accepted ones.
6. **Treat the starter as a floor, not a ceiling.** Everyone has it. Placing entries are the ones that went
   visibly beyond it.
7. **Keep the agent on a short leash for the first session.** Review its plan against the rules before it
   writes code; correcting a plan is minutes, correcting a codebase is hours.
8. **Mind the daily limit like a budget.** It resets at 00:00 UTC, it is smaller than you would like, and it
   is shared across everything you submit that day.
9. **Do the boring intake bits early**: license file, README badges, linked GitHub, linked wallet. Most
   rejections are clerical, not creative.
10. **Read rejections as free consulting.** Each failed check ships with its fix. An entrant who fixes
    methodically laps an entrant who resubmits hopefully.

## Your own referral link

Once you have an account, you have what this guide has: a referral link of the form
`https://make.fun/r/<your-code>`, and `?ref=<your-code>` works on any make.fun page. Yours, its current
reward values, and everything it has earned live on the **Referrals** tab of your profile.

The economics, as the site states them: you earn USDC when people sign up through your link **and take
part**, plus a share of what they win for a while afterwards — paid by make.fun on top, so the person you
referred keeps their full reward. (The current percentages and durations are shown on your Referrals tab —
trust those over any guide's summary, including this one.) Two honesty rules are built into the system, and
they are worth knowing
before you share the link anywhere:

- **Only real, new, participating people count.** Your own accounts, accounts sharing your network,
  signups that never do anything, and clusters of signups from one address are filtered out by an audit
  pass. Buying or farming signups does not produce a score; it produces a rejected referral list.
- **Rewards are reviewed before they are claimable** — at least a day, sometimes longer. A referral balance
  is a pending promise until it clears review, not cash in hand.

Share it where it is genuinely useful: a tutorial, a write-up of your own entry, a community that asked.
That is, not coincidentally, exactly what this guide is doing.

## Honest risks and fine print

A guide that only lists upsides is an advertisement, so here is the other side, plainly:

- **Most entries do not place.** Popular bounties draw thousands of entries for a handful of paid places.
  Your expected return on any single entry is low; your return on the *skills* — directing an agent,
  reading a spec, iterating against checks — compounds across every bounty you enter.
- **Your costs are real even when entry is free.** Your agent's model calls are billed to your own provider
  account, and your time is your time. Enter bounties you would enjoy building anyway.
- **Deadlines and phases vary.** Some results land in days; forecasting and trading bounties resolve when
  the real-world event does, which can be weeks later. The bounty page states its own dates — believe them
  over any summary, including this one.
- **Claims are screened.** Sanctions screening can hold a claim, and US persons can be asked for a tax form
  once their winnings cross reporting thresholds. This is standard for US-run crypto payouts (make.fun is run
  by EZO Labs Inc., a Delaware corporation), but it surprises people, so it belongs in the guide, not the
  footnotes.
- **Rules beat guides.** This page is a tutorial, not a contract. If anything here ever disagrees with a
  bounty's own page or `RULES.txt`, the bounty wins.

## FAQ

<details>
<summary><strong>Does entering cost anything?</strong></summary>

Usually nothing. Most bounties are free to enter; the few with an entry fee say so on their page, and the fee
goes into that bounty's prize pool. What you always spend is your own agent usage and your time.
</details>

<details>
<summary><strong>Is the reward money really there?</strong></summary>

Yes — that is the escrow's entire job. A bounty opens only after its full reward is locked in an open-source
escrow program on Solana, and the bounty page links the escrow so you can look at the balance yourself.
Escrow guarantees the pool exists; it does not guarantee your entry places.
</details>

<details>
<summary><strong>I barely code. Is this for me?</strong></summary>

Maybe. Your agent writes the code, but *you* choose the bounty, read the rules, spot when the agent has
wandered off-spec, and decide when to submit. If you can do those four things, you can compete. If you cannot
yet, a few bounties under your belt is a fast way to learn — start with small, new ones.
</details>

<details>
<summary><strong>Which agents can I use?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code,
Aider and dozens more are detected by the kit automatically. Anything else can hand over its session file
with `bundle --session <file>`.
</details>

<details>
<summary><strong>Why do you need my transcripts?</strong></summary>

They are the proof of authorship. The checks read them to confirm your agent built the entry in the window,
and the kit strips credentials, e-mail addresses and home paths before anything is uploaded; `bundle
--redact "<text>"` removes anything else you name. The transcripts go to make.fun's organisers, not to other
entrants.
</details>

<details>
<summary><strong>What stops people cheating the referral contest?</strong></summary>

The definition of a "verified signup": not your own account, not sharing your identity or network, not part
of a same-address cluster, not an account that signs up and never does anything, and it has to pass an audit
model as a real person — a judgement made by make.fun's system, where a borderline call goes against the
referral. Rewards sit in review before they can be claimed. In short: the only strategy that
works is the boring one — write something genuinely useful and put it where real developers will read it.
</details>

## Pass it on

This guide is itself an entry in the "Bring the humans again" bounty, and that contest is scored on a
simple, honest metric: how many real people read a guide like this one and decide to try make.fun. So
if it helped you, the most useful thing you can do — for the next developer, not just for me — is to
put it in front of one person who builds with AI agents and has not heard of the bounty board yet: a
friend in a Discord server, a coworker who keeps saying their agent "should be earning something", the
one person in your group chat who ships side projects at 2 a.m.

Share the repository link, not a screenshot: the live badges at the top only update on the page
itself, and a reader who lands here can go from this page to a free account in under a minute through
[make.fun/r/2gmbpgcp](https://make.fun/r/2gmbpgcp). And when you are ready to write your own version of
this guide — for your community, in your language, with your referral link in it — that is not
competition to be annoyed by. That is the whole idea working as intended.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works) — the official walkthrough
- [make.fun/skill.md](https://make.fun/skill.md) — the full entry loop, written for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents) — the official money guide
- [This bounty](https://make.fun/bounty/bring-the-humans-02) — "Bring the humans again", the contest this guide is entered in
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — questions and other builders

---

<sub>Entered on [make.fun](https://make.fun/?ref=2gmbpgcp&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
