    [BLOpts]
    title = "Monkey typing ABRACADABRA"
    tags = [probability, martingale, monkey]
    categories = [Probability, Math]

Since I decided to call this blog **martingalemeasure** it seems only fitting that
the first post should be about probability; martingales in particular. In my
favorite introductory book on measue theoretical probability, \"Probablity with
Martingales\" by David Williams, we find an exercise in Chapter 10. Which I
paraphrase here:

*Suppose a monkey is typing randomly at a typewriter whose only keys are the
capital letters $A$ through $Z$ of the english alphabet. What is the
expected (average) time it will take for the monkey to type the word
$ABRACADABRA$?*

This is not an easy problem. In fact it\'s not entirely obvious that the average time is even finte! Williams expects the reader to solve it using the
beautiful theory of martingales and in particular *Doob\'s optional-stopping theorem*.
We will calculate the result below, but stop short of a proof.
(There are many proofs of this result already on the web. A quick search for \"monkey abracadabra\" will
provide several links).

The purpose of this post is to try to provide
the intuition behind the result. We do this by comparing the expected time it takes for
the monkey to type $ABRACADABRA$ with the expected time it takes to type the first
eleven letters of the alphabet
$ABCDEFGHIJK$.

Simplification
--------------

It\'s almost always a good idea when trying to solve a problem to first attack
the simplest case you can think of that still embodies the essence of the problem.
For our problem  we can certainly benefit both from picking shorter strings, and by
choosing a smaller alphabet. The important distinction between $ABRACADABRA$ and
$ABCDEFGHIJK$ is that the former starts to repeat at charcter 8, i.e has a repeated
sub-string. So if we look
at $ABA$ versus $ABC$ we have a much shorter word that has the repeated sub-string $A$. Since we lose nothing by restricting the possible letters to one of $A$,$B$, or $C$; we restrict
our alphabet to these three letters.

Solution
--------

Ok, let\'s use martingale theory to solve the simplified problem and then apply
the result to the bigger problem. As is often the case in probability theory we will think in terms of
gamblers making bets. Suppose that just before each keystroke made by the monkey,
a new gambler shows up at a casino and employs the following betting strategy. She wagers
one dollar that the monkey will type an $A$, the first letter in the word. If she wins,
the casino pays her fair odds and she receives $3$ dollars. She then bets
the entire $3$ dollars that the next keystroke will be a $B$, the second letter. She
continues until either she has lost her intial dollar or the word is typed in full; in that case
she wins $27$ dollars, for a profit of $26$.

Each individaul bet is fair, that is, has an expected value of zero. Indeed,
our gambler has a ${1}/{3}$rd  chance of tripling her wager, say $x$ for
profit of $2x$ and a ${2}/{3}$rds chance of losing it. Therefore, her expected value
is $2x\cdot 1/{3} - x\cdot 2/3 = 0$. Hence, the entire strategy is fair, the
gambler on average will not make or lose any money. If we now consider the total amount won or
lost by the casino at any point in time, then that too must have expectation zero,
since each gambler is playing a fair game, so is the casino as a whole. I should
probably mention that the stochastic process describing the profit of the casino
is a martingale, which is why we can apply the necessary mathematical machinary we
need to solve this problem.

Here comes the big trick, when we say that the casino has expected gains of zero
at *any* time, we mean random times as well. Including random times like $T_{ABC}$ the first
time the word $ABC$ is typed or $T_{ABA}$ the first time the word $ABA$ is typed (technically time $T$ is called a stopping
time and needs to satisfies one of the sufficient conditions of Doob\'s theorem). We are almost there, all we need to do is calculate the expected gain by the casino
at times $T_{ABC}$ and $T_{ABA}$ and we will be done. Let\'s do $ABC$ first. The
first time the monkey types $ABC$, all of the gamblers except the 3rd to last will have
winnings of zero. The third to last will have winnings of $27$. The total amount wagered will be $T_{ABC}$. So in order for the game to be fair we must have,

$$\mathbb{E}[T_{ABC} - 27]=0$$

Hence, by the linearity of expectation,

$$\mathbb{E}[T_{ABC}]=27$$

But what happens when we analyze the string $ABA$ instead? At time $T_{ABA}$, not
only has the third to last gambler 27 in winnings, but the last gambler has 3.
Since she wagered one dollar on the event the monkey typed an A and the monkey
did. Hence,

$$\mathbb{E}[T_{ABA}-27-3]=0$$

and

$$\mathbb{E}[T_{ABA}]=30$$

Wow, the average time for the monkey to type $ABA$ as actually longer than the average time to
type $ABC$.

Back to ABRACADABRA
-------------------

It should now be straight forward to calculate the expected time it takes for the monkey to
type $ABRACADABRA$ and $ABCDEFGHIJK$. We simply compute how much money the casino owes the first time the monkey types the word. In the case of $ABCDEFGHIJK$
the only winner is the gambler who started 11 keystrokes ago. She grosses $26^{11}$
so that turns out to be the expected time. But in the case of $ABRACADABRA$ the gambler who
started playing 4 keystrokes ago has winnings of $26^4$ and the gambler who bet
on the last keystroke won $26$, hence for $ABRACADABRA$,

$$\mathbb{E}[T]=26^{11} + 26^4 + 26$$

Intuition
---------

I don't know about you, but I find this result is counter-intuitive. I expected it
would take the same time on average, or if anything shorter to type $ABRACADABRA$,
since at the 8th keystroke the monkey types an A starting the sequence again. Here
is where the simplified case using $ABC$ and $ABA$ can help us get a better grip on what
is really going on. In these cases we can easily caculate some probabilities. Let\'s
look at all of the winning strings after 5 keystrokes. We use \* to mean any
character in the alphabet, in this case one of $A$, $B$, or $C$. Here are the three events
that represent a case where the monkey has typed the string $ABC$ in 5 keystrokes or less:

    A B C * *
    * A B C *
    * * A B C

If we want to know the probability that the monkey typed $ABC$ in the first 5
strokes, we need to take the probability of the union of the three events above.
By looking at the third character in each string, we can see that the three cases
are mutually exclusive. Therefore, we can just add their probabilities.
The probability of the first case is clearly ${3^2}/{3^5}$ so the probability
of the union is ${3^3}/{3^5}={1}/{9}$. In other words the probability that the
monkey types $ABC$ in 5 keystrokes or less is $1/9$. On the
other hand for the $ABA$ case we have events:

    A B A * *
    * A B A *
    * * A B A

And again the probability of each event is ${1}/{27}$, but we can no longer add
the three events since they are no longer mutually exclusive. We can see that
the first and third cases overlap, they both contain the sequence:

    A B A B A

And that is the only string that they have in common. So by the inclusion - exclusion principle we need to subtract that case out to
get the probability as $(27-1)/{3^5}$
Which is lower by ${1}/{243}$rd.

And now it should be clear why the average
time for the monkey to type a word is longer if the word has repeated sub-strings.
*For any given time the probability of typing the string with repeated sub-strings
is lower so it must take longer on average for the event to happen*.