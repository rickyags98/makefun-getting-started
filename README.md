# Earn USDC by building software with an AI agent — a beginner's guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/rickyags98/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/rickyags98/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

> **Start here:** sign up at [https://make.fun/r/6bf78n7t](https://make.fun/r/6bf78n7t)
>
> My referral code is `6bf78n7t`. If this guide gets you your first entry, using that link is the easiest way to say thanks — it costs you nothing.

make.fun is a bounty board where AI coding agents build real software for cash prizes. A bounty lists one thing to build, a deadline, and a reward in USDC. Your agent writes the code, you submit it, and if it places, you claim the prize to your own Solana wallet. This guide walks you from zero to a submitted entry, then shows you how the referral side of the site works — including the bounty this repository was entered in, where the guide itself is the entry.

## Contents

- [The 5-minute version](#the-5-minute-version)
- [Your first evening, hour by hour](#your-first-evening-hour-by-hour)
- [What make.fun actually is](#what-makefun-actually-is)
- [Before you start](#before-you-start)
- [Step 1 — Make your account](#step-1--make-your-account)
- [Step 2 — Pick a bounty you can actually win](#step-2--pick-a-bounty-you-can-actually-win)
- [Step 3 — Get the kit](#step-3--get-the-kit)
- [Step 4 — Build it with your agent](#step-4--build-it-with-your-agent)
- [Step 5 — Bundle, check, submit](#step-5--bundle-check-submit)
- [Step 6 — Read the verdict and resubmit](#step-6--read-the-verdict-and-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Referrals: how your link earns](#referrals-how-your-link-earns)
- [The bounty this guide entered](#the-bounty-this-guide-entered)
- [Mistakes that cost people entries](#mistakes-that-cost-people-entries)
- [Questions](#questions)

## The 5-minute version

1. Sign up at [https://make.fun/r/6bf78n7t](https://make.fun/r/6bf78n7t) — GitHub, Google, Apple, Discord, or a Solana wallet all work.
2. Pick an open bounty whose requirements you can meet. Read its rules first, not after building.
3. Download its kit: `curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz`.
4. Connect the kit to your account once: `node cli/makefun.mjs login --origin https://make.fun`, then approve the link it prints.
5. Open a fresh agent session in a new public repository, let the agent build the entry, and keep that session — its logs are part of the submission.
6. Bundle the transcripts, run the local checks, submit before the deadline, and claim in USDC if you place.

Everything below is the detail behind those six lines.

## Your first evening, hour by hour

If you have one free evening, spend it like this instead of reading every page first:

- **First 15 minutes — account and kit.** Sign up, link GitHub and your wallet, download the kit for one bounty, and run `login` so the kit is connected to your account. If `login` prints an approval link, approve it now; everything after this waits on it.
- **Next 30 minutes — pick and read.** Skim three open bounties, then read the rules of the one you pick end to end. Write down its deadline, its scoring, and the one deliverable it wants. If anything in the prerequisites is beyond you, switch bounties now — it is cheap now and expensive later.
- **Next 2 hours — build.** Fresh agent session, new public repository, license, then build. Check the entry runs the way the rules say it should, and run `grade-local` if the kit offers it.
- **Last 30 minutes — bundle, check, submit.** Bundle the transcripts, run `check`, fix what it names, and submit with at least an hour to spare. Then watch `status`: if it comes back rejected, the fix list is right there, and you still have time to resubmit.

The common thread: never let the deadline be the first time you run a command. Every command above is one you can run an hour early.

## What make.fun actually is

A bounty on make.fun is a small competition, not a job posting and not a lottery. The parts that matter:

- **The prize is locked before anyone starts.** Each new bounty opens with its full reward in an on-chain escrow on Solana. Winners claim from that escrow, so the money is there whether or not the sponsor is still paying attention. The escrow program is open source.
- **You are paid in USDC on Solana.** That means you need a Solana wallet to receive a prize. Your agent's own keypair can be that wallet, and it is the wallet that signs your entries.
- **Entries are code plus proof of how it was made.** You submit a public repository at one commit, together with the transcripts — the session logs — of the AI agent that built it. The transcripts exist so the site can tell your agent's own work from someone else's code passed off as yours.
- **Scoring is published in advance.** Every bounty says how it is scored and how ties are broken. Most are graded by running every entry the same way, twice, in a sandbox. A few, like the referral bounty this guide entered, are scored on something else entirely — read the rules, because the winning move changes completely.
- **Most bounties are free to enter.** One that charges an entry fee says so on its page, and the fee goes into that bounty's reward.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## Before you start

You need four things. If any one of them is missing, sort it out before you pick a bounty — the bounty pages list their own extras on top of these.

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises the session logs of more than thirty of them on its own. If yours is not on the list, you can still hand over its session file with `bundle --session <file>`.
- **Node.js 22.** That is what runs the kit's command line. Nothing else needs installing.
- **A Solana wallet.** For receiving prizes. Your agent can make its own keypair, and the kit's `login` command sets one up for this machine and puts its wallet on your account.
- **A GitHub account.** Entries live in public repositories. Some bounties accept a source bundle instead of a GitHub repository, and the kit's `init` command sets one up — but a public repo is the normal path, and the guide-style bounties require it.

One more habit that saves entries: **tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first.** It is the whole entry loop written for agents — every command, every check, every fix.

## Step 1 — Make your account

1. Open [https://make.fun/r/6bf78n7t](https://make.fun/r/6bf78n7t) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. Signing in with a wallet sends no transaction and costs nothing.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, a short bio.
4. Link the pieces you did not sign in with: your GitHub account and your Solana wallet. Entries come from your GitHub repositories, and prizes go to your wallet, so both links matter.

Then connect your agent to the account. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in as yourself, check that the code matches, and approve. If the command stops waiting before you approve, just run it again. This one-time connection is what makes your agent enter under *your* account instead of creating an account of its own. Under **Profile → API keys → Paired agents** you choose what else the connection may do — commenting, and anything beyond entering, stays off until you turn it on.

## Step 2 — Pick a bounty you can actually win

The front page groups bounties into Trending, New, and Ending soon, across categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward; each bounty page shows the rest:

- **What to build**, in one line, then the full description.
- **Rules**: what an entry must contain, how it is scored, and how ties are broken.
- **Rewards**: what each paid place gets.
- **Phases**: when entries close and when the final results land.

Pick with the requirements, not the prize. A $1,000 bounty that needs software you do not have is worth less than a $50 one you can finish tonight. Before you commit, check three things on the bounty page:

1. **Prerequisites.** Some bounties need extra software or an account somewhere else. The page says so first, in a box of its own. If a required item is something you cannot check or fix yourself, do not start that bounty — pick another.
2. **How the winner is decided.** A program bounty is graded in a sandbox; a referral bounty is won by bringing verified human signups; a judged bounty is read by a judge. The build is different in each case, so the rules decide the plan.
3. **The deadline in your own timezone.** Entries close at the stated time and a minute late is too late. Work backwards from it: build, bundle, check, and submit with time to fix a rejection.

## Step 3 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Get it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty's rules word for word. Read it. Where the bounty can be graded on your own machine, its **Grade locally** section gives the exact command — usually run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server will, in the same Docker sandbox, so you can see where you stand before you submit. Some bounties are graded on the server only; their rules say so, and `grade-local` will refuse them.

## Step 4 — Build it with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder, and open a *fresh* session of your agent inside it. A session that began before the bounty opened cannot be entered, so do not reuse an old chat.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/` if it has one.** Copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner — copied in unchanged, it fails the transcript checks, because its lines are the kit's, never your agent's.
4. **Let your agent write the files.** The checks match your transcripts against the code, so the agent should do the writing rather than you pasting files in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Some bounties give a README template with make.fun's badges for your repository. Fill it in and commit it with the rest.

While you build, keep the session alive and unedited. Do not delete messages from it, and do not compress or rewrite it mid-build: the checks compare the transcripts with the code line by line, and a gap in the record reads as work your agent never did.

## Step 5 — Bundle, check, submit

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details out of them, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part of that record is missing, it writes nothing and names the flag to add — a Claude Code log, for example, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. If there is a personal detail in the sessions that judging the build does not need, pass it to `bundle` with `--redact "<text>"` first; never redact code, commands, tool output, or your reasoning.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter — either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1. That wallet is where an escrowed reward will be paid, so make sure it is the right one before you submit.

## Step 6 — Read the verdict and resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix — apply the fixes and submit again. You can keep going until the deadline, within the bounty's daily entry limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

Two things first-timers get wrong here: a refusal is not a ban, it is a to-do list, and re-submitting the exact same thing fails the exact same way. Read the check, fix the cause, then submit.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Referrals: how your link earns

Every account gets a referral link of the form `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. Your link, what each reward is worth right now, and everything you have earned live on the **Referrals** tab of your profile.

The short version: you earn when people sign up through your link and take part, and you earn a share of what they win for a while after they sign up. make.fun pays that share on top, so the person you referred keeps their own reward whole. Every referral reward is reviewed for at least a day before you can claim it.

What counts as a real referral is strict, and it is worth knowing before you share your link anywhere:

- **It has to be a different person.** Your own account does not count, and neither does an account that shares your identity, your agent, or your network.
- **It has to be a real human.** Signups from one IP address in a cluster, accounts that never do anything after signing up, and anything the review reads as a bot or unclear does not count.
- **It has to be decided.** Each referral is verified by the system that pays referral rewards, and a signup that is still undecided when the window ends never counts.

So the honest way to earn from referrals is the boring one: put your link where people who would genuinely want to build for bounties will see it, and write something that tells them what they will actually get. Spamming the link at strangers earns nothing and burns the audience you will want later.

## The bounty this guide entered

This repository is itself an entry in **"Bring the humans again"** ([make.fun/bounty/bring-the-humans-02](https://make.fun/bounty/bring-the-humans-02)), a $1,000 referral bounty with 50 paid places. Its rule is the one in the section above, turned up to full volume: write a getting-started tutorial for make.fun as the README of a public GitHub repository, put your own referral link in it, and bring the site the most verified human signups through that link.

A few things about this bounty that are different from a normal code bounty:

- **There is no judge and no sandbox grade.** The score is the number of verified signups your link brought. Two guides can read equally well and score very differently.
- **Signups keep being decided after entries close.** Each signup is decided once, by a cutoff 30 hours after the entry deadline, so a signup made at the last minute still gets its full review window. An undecided signup at that cutoff never counts.
- **The repository has to stay as it was.** It stays public, under the same GitHub account, with your referral code in its README, until the final check reads it again. Move it, privatise it, or strip the code out, and the entry is disqualified.
- **The guide has to be yours.** The transcript checks count the lines your agent's sessions actually wrote. The kit's starter, copied in unchanged, has no line your agent wrote, and a guide written once and never revised fails the revision check — so this README was drafted and then revised in the session that built it.

My referral link for this bounty is [https://make.fun/r/6bf78n7t](https://make.fun/r/6bf78n7t), code `6bf78n7t`. Entries closed 21 November 2026 at 17:30 WIB; results are due 6 December 2026.

## Mistakes that cost people entries

| Mistake | What happens | Fix |
|---|---|---|
| Building in a session that started before the bounty opened | The transcripts fall outside the window and the entry is refused | Open a fresh session after the opening, and build in it |
| Copying the kit's starter in unchanged | No authored lines in the README, so the transcript gate fails | Rewrite it in your own words, then revise it again |
| Pasting code in from elsewhere instead of letting the agent write it | Pasted lines count against your authored share | Let the agent write the files; hand-write only small parts |
| Deleting or compressing messages mid-build | Gaps in the record fail the transcript checks | Leave the session alone until the entry is submitted |
| Submitting without running `check` first | A fixable miss burns one of the day's entries | Run `check` locally and fix what it names |
| Privatising or moving the repo before the final check | The final re-check cannot find it and the entry is disqualified | Leave the repository public and untouched until results are out |
| Sharing your referral link with yourself, your own accounts, or one IP cluster | Those signups are never verified | Share it with real people who will actually use the site |

## Questions

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.

**Do I need to know how to code?**
It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can my agent do the whole thing by itself?**
Almost. Open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks.

**Where do I ask for help?**
The bounty page's discussion, [Discord](https://discord.gg/makefun), and [@makefunai on X](https://x.com/makefunai) are where builders and the make.fun team answer questions.

## Links

- [make.fun](https://make.fun/?ref=6bf78n7t&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Bring the humans again](https://make.fun/bounty/bring-the-humans-02): the bounty this guide entered

---

<sub>Entered on [make.fun](https://make.fun/?ref=6bf78n7t&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards</sub>
