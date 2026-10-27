# Rules and gates

How to write a rule into a system so it still works in the case you did not think of, when a gate earns its place, and how to tell a cause from a correlation. Load this at the moment you are about to encode any rule, check, or gate. That moment, not the review afterward, is where discernment pays.

## The rule shape

A year or two ago the risk with agents was too little constraint. The models were worse at following instructions and you wanted guardrails. Today the risk has flipped. The models thrive with guardrails now, they follow them well, and so the failure has moved: a rule so tight it blocks the work you actually asked for. The mechanism is specific: when an AI writes or optimizes its own rules, it reaches for black and white. It writes "never merge to main," and three weeks later it fights you about merging to main in a repo you are using as a versioned filing cabinet where branching makes no sense. It is not going to think to take that step. You have to.

So a rule carries its reason and its exception:

Generally avoid X, because [the real reason], unless [the named exception], and if uncertain, flag it.

The because lets the agent reason about a case you never anticipated: "we almost never merge to main unless it's an emergency" works the day the server is burning, and "never merge to main" does not. The unless scopes the rule instead of banning the category. The flag keeps the judgment in the loop at the place you want it. Absolutes are for genuine absolutes: irreversible harm, syntax that breaks, the thing that has to hold when nobody is watching. Everywhere else an absolute costs twice. It suppresses a move you never thought to allow, and it makes the real absolutes elsewhere read as merely emphatic.

Watch the noun as much as the verb. Something called a gate will stop work. Something called a rule of thumb will be weighed. If a thing is advice, call it advice. If it genuinely must hold, say so and say why.

## Gates

A gate is useful where a requirement must be met, full stop: nothing ships with a secret in it, nothing sends email without the operator's yes, the tree compiles before a push. Those earn their friction.

Everywhere else a gate is friction without a reason. Most best practice is advice: a good idea most of the time, with cases where the showrunner's judgment should win. Making advice into a gate does something worse than slow things down. It teaches the system to oversteer itself away from the outcome the operator wanted, on the grounds that the rules said gate. The showrunner's judgment is supposed to be the gate.

When importing discipline from software engineering (proof standards, required checks, typed statuses), test each piece against one question: does it add a gate the showrunner must obey, or does it help the showrunner see and decide? Only the second kind transfers cleanly. A sensor that makes a problem visible is almost always worth having. A checklist the showrunner has to satisfy before it may use its judgment usually is not.

The same applies to how the rule is phrased. Say how we do things, not what we refuse to do. "We write rules with their reasons" lands better than "never write a rule without a reason," and it leaves the operator the room to decide.

## Cause versus correlation

Here is the trap that scales. You hand-fix a batch of AI-sounding paragraphs. Nearly every fix comes out longer, because the originals were vague and making them specific took more words. The AI looks at the batch and writes the rule: to sound human, write longer. The pattern is real. It is not the point. The principle was "be specific," and length was a side effect. Longer was not the fix.

Same thing in code. The agent sees a bad value arrive, writes a check that rejects it, and calls the bug fixed. The real question was how the bad value got produced upstream, and the fix belongs there, where it also fixes the three other places that value was going.

So before a lesson becomes a rule, ask whether the stated cause would survive a counter-example. If a shorter, more specific rewrite would also have been fine, length was not the cause. If a correct value could also have come from that upstream path, the rejection check was not the fix. A wrong rule is worse than no rule, because it runs a thousand times.

This is where the operator's discernment goes: once, at the moment the rule is written, instead of in every downstream instance. Tune the system after a session full of corrections and those corrections retire. The same work that used to need twenty-five catches needs one or two.
