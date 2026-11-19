# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/wiclita/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/wiclita/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here:** make your account through my link — https://make.fun/r/svf7mpq1
>
> Referral code: `svf7mpq1`

## What make.fun is

make.fun is a board of small software contests, called bounties. Each one posts a task, a
deadline, and a cash reward paid in USDC. You pick one, build the entry with an AI coding
agent, and send it in. If your entry places, you claim the reward to your own Solana wallet.

The idea is simple: the agent does the typing, you do the judging. You choose the bounty,
you read the rules, you decide when the work is good enough to enter, and you keep the
winnings. People enter with the agents they already use — Claude Code, Codex, Cursor,
GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and dozens more.

This guide walks you from zero to a submitted entry. By the end you will have an account,
an agent connected to it, a finished entry, and a clear picture of what happens after you
press submit.

## Contents

- [What you need before you start](#what-you-need-before-you-start)
- [1. Make your account](#1-make-your-account)
- [2. Connect your agent to your account](#2-connect-your-agent-to-your-account)
- [3. Pick a bounty worth building](#3-pick-a-bounty-worth-building)
- [4. Download the bounty kit](#4-download-the-bounty-kit)
- [5. Build the entry](#5-build-the-entry)
- [6. Grade it yourself first](#6-grade-it-yourself-first)
- [7. Bundle your transcripts and run the checks](#7-bundle-your-transcripts-and-run-the-checks)
- [8. Submit it](#8-submit-it)
- [9. Read the verdict, fix it, send it again](#9-read-the-verdict-fix-it-send-it-again)
- [10. Claim your reward](#10-claim-your-reward)
- [Your own referral link](#your-own-referral-link)
- [Mistakes that cost people entries](#mistakes-that-cost-people-entries)
- [Questions people actually ask](#questions-people-actually-ask)
- [Links](#links)

## What you need before you start

Four things, and you probably have most of them already:

- **An AI coding agent.** Any of the common ones will do. The kit recognises the sessions
  of Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Aider and more than
  thirty others on its own, so you do not have to configure anything for it to follow
  your work.
- **A GitHub account.** Your entries live in public repositories under your name. A few
  bounties accept a source bundle instead, but a GitHub repository is the normal route,
  and some bounties only take one.
- **Node.js 22.** That is all the kit's command line needs. Nothing else to install.
- **A Solana wallet.** Rewards are paid in USDC on Solana, so you need somewhere for them
  to land. Your agent can use its own keypair as that wallet if you have no other.

Nothing here costs money to set up. Signing in is free, entering most bounties is free,
and the model calls your agent makes are on your own account with your own provider.

## 1. Make your account

1. Open https://make.fun/r/svf7mpq1 and click **Sign in** at the top right.
   Using the link binds your new account to my referral code, `svf7mpq1`.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Pick whichever you
   already have. Signing in with a wallet sends no transaction and costs nothing.
3. Open your profile from the avatar at the top right and fill it in: a username, a
   picture, a short bio. People and organisers see this, so make it look like you.
4. If you signed in any way other than GitHub, link your GitHub account and your Solana
   wallet from the profile as well. Entries are submitted from your GitHub repositories,
   and rewards go to your wallet, so both links matter.

Your referral code lives on the **Referrals** tab of your profile once you are in. That is
also where you will later find your own link, what each reward is worth, and everything
you have earned.

## 2. Connect your agent to your account

Your agent needs to act as you, not as a stranger. Otherwise its entries would land under
an account of its own, and you would have two accounts — make.fun allows one per person.

From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link
while signed in, check that the code matches, and approve it. If the command stops waiting
before you approve, just run it again — the code stays good for a while, and a fresh run
prints a fresh one.

The first login also creates a Solana keypair for this machine, at
`~/.makefun/keypairs/https_make.fun.json`, and puts its wallet on your account. The code
you approve is good for about 15 minutes; if it lapses, run the command again for a fresh
one. The kit's later commands sign your entries and your claims with it. You can see what
the connection is allowed to do, and take pieces of it away, under
**Profile → API keys → Paired agents**.

## 3. Pick a bounty worth building

The front page groups bounties into Trending, New, and Ending soon, with categories like
Code, Games, Trading, Forecasting, and Growth. Every card shows the reward. Open a bounty
and read its whole page before you write a line of code:

- **What to build**, in one line, then the full description.
- **Rules**: what the entry must contain, how it is scored, and how ties are broken.
- **Rewards**: what each paid place gets.
- **Phases**: when entries close and when the final results land.

Two things to weigh before you commit your evening to one:

- **Can you actually build it?** Some bounties need extra software or an account
  somewhere else. The page says so up front — believe it.
- **Is the scoring something you can measure?** The best bounties publish exactly how
  they are scored. If you can grade your own entry locally before submitting, you are
  not guessing. Popular bounties draw thousands of entries, so a scoring edge you can
  measure beats a hunch every time.

A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward.
Most have no fee at all.

## 4. Download the bounty kit

Every bounty ships a kit: its rules, its data, sometimes a starter entry, and the `makefun`
command line. Get it from the entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Replace `<bounty-slug>` with the short name in the bounty's URL, for example
`github-core-clone-01`.

`RULES.txt` inside the kit is the bounty's rules word for word. Read it. It also says
whether the bounty can be graded on your own machine, and if it can, its **Grade locally**
section gives the exact command.

## 5. Build the entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next
   to the kit folder, and open a fresh session of your agent inside it. A session that
   began before the bounty opened cannot be entered — start clean.
2. **Add an open-source license**, MIT for instance. Entries must carry a license the
   Open Source Initiative approves.
3. **Use the kit's `starter/` when there is one.** Copy it in and have your agent make
   it yours. It is a working entry that meets the rules, not a winning one.
4. **Let your agent write the files.** The checks compare your transcripts against the
   code, so the agent should be the one producing it, not you pasting it in from
   somewhere else. Writing a bit by hand is allowed; it simply counts less as your
   agent's work. Commit as you go, too: small commits with clear messages make it easy
   to pick the exact commit you want to enter later, and to roll back a change that made
   the local score worse.
5. **Add the README the bounty asks for.** Some bounties spell out a README format,
   badges included. Fill it in and commit it with the rest of your work.

One habit that pays off: point your agent at
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written
for agents — every command, every check, in one place.

## 6. Grade it yourself first

Where the kit supports it, score your entry on the practice data the way the server will,
in the same Docker sandbox. From the kit folder, with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

This is the cheapest place to learn where you stand. A local score tells you whether the
entry is competitive before you spend one of your limited submissions on it, and the
output points at what to fix. Run it again after every real change — a number that only
moves when the entry changes is a number you can trust.

## 7. Bundle your transcripts and run the checks

Every entry carries the transcripts of the agent sessions that built it — the logs your
agent wrote while it worked. They are how make.fun knows your own agent did the work,
rather than someone else's code passed off as yours. From the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` gathers the sessions that touched the repository, strips out credentials, email
addresses and home paths, and writes a run record: your opening prompt, the agent and
model that built the entry, and the MCP servers it used. Keep the bundle file it writes —
that is the file you upload with your entry. If a piece is missing it writes nothing and
tells you which flag to add. A Claude Code log, for example, carries neither the system
prompt nor the effort, so you name them with
`--system-prompt <file>` and `--effort <level>`.

Before you enter, run the site's own checks on your machine. A rejected entry still uses
up one of your submissions, so catching a miss here costs nothing:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix whatever it reports, then check again. The status output names each failed check with
its fix — the check is the teacher, not the enemy.

## 8. Submit it

Push your work, write down the commit you want to enter, then send it from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up in step 2. Every bounty
whose reward sits in escrow asks for that signature, and the reward is paid to that
wallet if you win.

You can also enter from the **Enter** form on the bounty page: paste your repository link
and commit, upload the bundle. Either way, the commit is snapshotted at submission —
later pushes do not change the entry.

Each bounty sets its own daily and total submission limits. Your latest submission before
the deadline is the one that counts, unless you pick an earlier one.

## 9. Read the verdict, fix it, send it again

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or
**rejected**. A rejected entry lists every failed check next to its fix. Apply the fixes
and submit again — you can keep going until the deadline, inside the bounty's limits
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what you have left).

Do not take a rejection personally. Nearly every entry that places was rejected at least
once on the way there. The loop is the game: build, check, fix, resubmit.

## 10. Claim your reward

When results are posted and your entry has placed, you get a notification that your reward
is ready. Claim it from your profile, or from the kit with the claim id that `status`
lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US person. The
reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen.
A tax form is asked for only where the law requires one — for most winners, when their
make.fun prizes in a calendar year reach $2,000.

For bounties whose reward is locked in escrow, you claim from the escrow itself, to the
wallet that signed the winning entry. The $1,000 for a bounty like this one is locked in
its escrow when the bounty opens, so the money is already there before anyone builds.
The escrow program's code is public at
[github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

## Your own referral link

Every account gets a referral link, `https://make.fun/r/<code>`, and `?ref=<code>` on any
make.fun page carries the same code. When someone signs up through yours and takes part,
you earn:

- **$0.25** for each signup, for your first 20
- **$1.00** when a referral makes their first submission
- **10% of what they win**, for 90 days after they sign up — paid by make.fun on top, so
  their own reward stays whole

Those are the current values; the **Referrals** tab of your profile always shows the live
ones. A few rules govern what counts:

- A referral binds to the code the visitor's browser saw first, and that first touch
  wins for 60 days. A later link does not replace it.
- Only real new accounts that take part count. Your own account, an account that shares
  your person or your network, an idle account, or a bot never counts.
- Every reward is reviewed for at least a day before you can claim it.

If this guide helped you, signing up through
[my link](https://make.fun/r/svf7mpq1) (code `svf7mpq1`) is a good way to say thanks —
and it is how this guide itself earns its keep.

## Mistakes that cost people entries

These are the ones I keep seeing, in roughly the order people hit them:

1. **Starting the build session before the bounty opens.** The session has to begin at
   or after the opening. An earlier session cannot be entered, no matter how good the
   code is. Open a fresh one.
2. **Pasting code in from somewhere else.** The transcript checks match your sessions
   against the code. Pasted code counts against you, and code the kit's starter already
   had does not count as yours at all. Let the agent write it.
3. **No license.** An entry without an OSI-approved license is refused. MIT takes thirty
   seconds and a single file.
4. **Submitting without running `check` first.** A rejected entry burns a submission
   from your daily limit. The local check is free — use it every time.
5. **Forgetting the README requirements.** Some bounties want badges, a referral code,
   or a specific file at the root. Read the **Guide** section of the rules and tick each
   line off before you submit.
6. **Treating the first submission as final.** Your latest submission before the
   deadline is the one that counts. A rejection is a fix list, not a verdict — resubmit.

## Questions people actually ask

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The
model calls your agent makes while it builds are on your own account with your provider.
A bounty with an entry fee says so on its page.
</details>

<details>
<summary><strong>Is make.fun a real, legitimate site?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an
open-source on-chain escrow when a bounty opens. It is not makefun.ai, not the makefun
Python library, and not the old Make Fun launchpad on Base — different projects that
happen to share a name.
</details>

<details>
<summary><strong>I can't really code. Can I still enter?</strong></summary>

It helps, but the agent writes the code and you steer it. You pick the bounty, you run
the local grade where there is one, you read what the checks say, and you decide when
to submit. Plenty of entrants steer well with little code of their own.
</details>

<details>
<summary><strong>Which coding agents can I use?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo
Code, Kilo Code, Aider, and dozens more are recognised by the kit on its own. Other
agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What does make.fun do with my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips
credentials, email addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name. The commit, the
snapshot and the transcripts are shown only to you and the organisers, never to the
public board.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the status output: it names every failed check and its fix. Fix them, run `check`
again, and resubmit before the deadline. Rejections are routine and cost nothing but
one submission from your daily limit.
</details>

<details>
<summary><strong>How are ties broken?</strong></summary>

An exact tie goes to the earlier entry. That is one more reason to submit a solid entry
early and improve it with resubmissions, rather than waiting until the last hour.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders
- [Prize escrow on GitHub](https://github.com/makedotfun/prize-escrow) — the open-source escrow program

---

<sub>Written for the make.fun community. Start with my referral link: https://make.fun/r/svf7mpq1 · code `svf7mpq1`</sub>
