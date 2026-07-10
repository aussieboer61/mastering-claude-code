# What Claude Code Actually Is

*The other half of the tool, for everyone the developers forgot to invite.*

You've heard the name. Probably from a developer friend, or in passing on a podcast, or because somebody on the internet was very excited about it. The framing is almost always the same: *"It's like ChatGPT, but for code."* And that's not wrong, exactly — programmers were the first to find it, and it's been very good to them. But it's also the reason most people who could get enormous use out of it close the tab and go back to pasting questions into the ChatGPT box.

This guide is for everyone else. The lawyer with eight years of case files spread across folders nobody has organised. The novelist who's lost track of which character knows which thing. The bookkeeper for a small trades business whose filing system is the kitchen table. The doctoral researcher with three hundred PDFs on Pliny the Elder and no clean way to ask one question across all of them. The person renovating a house who has fourteen email threads about tiles and cannot remember which supplier quoted what.

None of those people are writing software. All of them are doing the kind of work Claude Code was made to make less painful.

## So what is it, in one sentence

It is a way of using Claude — the AI — that **lives on your computer, can see your files, can remember you between conversations, and can do work while you're not at the keyboard.**

Five things in that sentence. Each of them is what makes it different from the chat box you already know.

## Why the chat box hits a wall

If you've used ChatGPT or Claude in a browser tab, you've probably had this experience. You start a conversation, you explain your situation, you get useful help. The next day you open a fresh conversation and have to do all the explaining again. By the fifth conversation you've stopped bothering with anything complicated and use it for one-off questions only — "summarise this paragraph", "draft a polite chase email". Real, but small.

The wall is that the browser version is a *visitor*. It arrives, helps, and leaves. It doesn't know your folders. It doesn't keep notes. It can't pop back tomorrow and check whether the council got back to you. Every conversation starts at the same place: zero.

Claude Code is the same Claude, but it's no longer a visitor. It's been handed a set of keys to a workspace you control. What it can do with those keys is up to you — and it's almost entirely about the keys, not the AI.

## Five things it can do that the chat box can't

**It can read the actual files on your computer.** Not "paste them in", not "upload them one at a time" — read them, in place, the same way you would. A folder of contracts, a tax-year's worth of bank statements, an inbox of emails you've exported, a draft manuscript split across forty Word documents. You point it at the folder and ask the question. It opens what it needs to open.

**It remembers you across conversations.** You can hand it a few sentences about who you are, what you're working on, and how you like to be spoken to — and it reads those sentences at the start of every future conversation, automatically. You will not have to say "I'm an Australian small-business owner doing quarterly BAS" ever again. You say it once.

**It follows rules you set.** This is the one that surprises people. You can write down "never send an email without showing me a draft first" or "always check the cited paragraph actually says what we claim it says" — and those rules sit between Claude and your work, every time. The AI doesn't decide to follow them. They're enforced. The same way a procurement policy is enforced: you can't get around it.

**It can work while you're not there.** You can hand it a job — *go through every supplier email from the last six months, pull out the prices, and put them in a table I can read in the morning* — and walk away. It will work overnight, leave you the result, and ping your phone if it gets stuck. This is the capability that most reframes what you can do in a week.

**It can talk to your other tools.** Your email account, your calendar, your accounting software, your task list. Anything that has the kind of plug-in connection that ChatGPT plugins exist for, Claude Code can use — but at the level of "do the whole job", not "answer a question about the data". *Draft the invoice in the accounting system, attach the timesheet from the shared drive, save the email to my drafts folder, then tell me what's left.* That request, end to end, is one prompt.

None of those five things require you to write a single line of code. They require you to be willing to set up a workspace, the way you'd set up a new desk.

## Three people, three uses, no coding

**The solicitor.** She has nine years of client files on a network drive. They are organised, but only because she organised them, and she's the only one who can find anything. When a new matter comes in she spends an hour every week looking for the precedent she knows is in there somewhere. She sets up Claude Code with read-only access to the network drive, writes one short note explaining how her files are named, and from that point on she asks plain English: *find the three most recent retainer agreements where we acted for the lessor in a commercial tenancy dispute, and pull out the indemnity clauses.* Two minutes, not an hour. She didn't index anything. She didn't tag anything. She didn't write a script.

**The novelist.** Two-hundred-thousand words, fourteen point-of-view characters, a timeline that started in 1983 and now stretches to 2011. He cannot remember which character knows that the youngest daughter is not the husband's biological child. He sets up Claude Code with his manuscript folder and a short note about each character — name, what they know, what they don't. Then every time he writes a new scene, he asks: *given Sarah's POV in this scene, is there anything she knows or doesn't know that would change what she says here?* The AI does not write the scene for him. It catches the continuity break that costs him a week of rewriting if he misses it.

**The small business owner.** A husband-and-wife trades business. The bookkeeping is six months behind, the receipts are in a shoebox, the bank statements are PDFs, and the quarterly tax return is due in three weeks. They set up Claude Code with the receipts scanned to a folder and the bank statement PDFs in another. They write down their account codes once. Then they tell it: *go through every bank transaction in February, match it to a receipt where you can, flag the ones you can't, and put together the BAS draft so I can check it.* It works for forty minutes. They check it for twenty. The job that was going to consume their weekend takes an evening.

Each of those people set up something **once**. After that, the same setup serves them every time the problem recurs. That's the part the browser tab cannot do.

## The honest catches

It isn't magic. There are three things you have to accept.

**You have to set the rules.** The AI will do what you ask. If you ask it badly, or if you don't tell it the things that matter — *we never agree to indemnities uncapped by the contract value*, *the youngest character can't know about the affair until chapter eleven* — it will produce work that doesn't match your judgement. The rules-and-memory part of the setup is where you put your judgement, once, so it shows up every time.

**You have to give it the keys.** It runs on your computer. It can see what you let it see. That's the point — it's also the responsibility. You don't hand the keys to your kitchen to someone you don't know, and you don't let Claude Code into a folder you wouldn't show a thoughtful assistant. The control is yours, but you have to use it deliberately.

**It can be wrong.** It is much, much better than it was two years ago, but it still occasionally invents citations, misreads numbers, and confidently states things that aren't true. The rule "always show me the draft" exists for a reason. The leverage isn't that it never makes mistakes — it's that it makes the kind of mistakes a careful reader can catch in two minutes, doing work that would have taken you two hours.

## What you'll need to actually try it

Almost nothing, by software standards. A computer running macOS, Linux, or Windows. A Claude account — the Pro plan at twenty US dollars a month is the usual starting point. About half an hour to install it and run a first session. And a folder you actually care about, because there's no point setting up an assistant for the workspace you never visit.

The terminal — the black-text window that programmers use — is where Claude Code lives. If you've never opened one, that is the only piece of "this is for coders" that's real. You will need to spend twenty minutes getting comfortable with the four or five commands required to change folders and start a program. Anyone who has ever used a command on a Mac to fix a printer, or typed into a Windows Run box, has done harder things. After those twenty minutes the rest is plain English.

## Why pick this up at all

The case for it, in the end, is not about the AI. It's about what stops being a chore.

Most adults have a list of work they don't get to because the setup cost is too high. Going through six months of receipts. Reading the new contract carefully enough to catch the bit that's changed. Pulling together the quarterly numbers. Indexing the research. Replying to the email backlog. Comparing the three quotes. Writing the council submission. The work isn't difficult; the *getting started* is difficult, every single time.

Claude Code is, at its most honest, a way of dropping the getting-started cost to roughly zero — for the kind of work that has structure and lives in files. The first time you set it up to do something you'd been avoiding for two months, and it does it in twenty minutes, you understand why people are excited.

The rest of this guide — the nine things you build once and use forever — is about how to set that up well. But you don't need any of that to begin. You need to know that the tool is not what its name suggests. It is a working environment for anyone whose job involves reading, writing, remembering, and following rules — which is, when you think about it, most jobs.
