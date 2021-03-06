---
layout: post
title:  "Bitcoin mining as a sacrifice ritual"
date:   2018-07-12
author: Paul Boes
katex: true
---

Assuming that you have money in some bank account, how do you know that next time you want to withdraw any of it, the bank won’t pretend that you’ve never paid anything into the account? The answer, I suppose, is that the bank is forced by the laws of the state you live in to document all its incoming and outgoing transfers in a difficult-to-forge manner, that this state can ask them to report those documents upon request, that this state is allowed to fine the bank in case of fraud, that further this state has sufficient credible executive power to enforce the above rights and that, finally, the prospect of being fined appears worse to the bank than simply being honest.
This property of a currency, that anybody who owns some amount of it can rely on this amount not suddenly vanishing from his or her possession, I call its *persistence* and the reasoning above is exactly how, I think, currencies minted by states establish their persistence: through credible political and executive power. 

Abstractly speaking, what was going above is that, in every state, there exists a big book and every monetary transaction, such as you paying something into your account, is noted in this book. This book, and this book alone, decides in situations of conflict about who owns what. The credible political power of a state then is a way of (a) ensuring that this book is always up-to-date (by being able to enforce proper reporting) and (b) correcting discrepancies between what the book says and what the actual situation is.

I think it is clear that persistence is an important and necessary property of any functioning currency and the question for decentralised currencies is: How do they achieve persistence?  The above mechanism cannot work because it is the very point of such currencies that there does not, abstractly or otherwise, exist a single big book that defines the collective state of ownership at any given time. Instead, in such currencies, everybody is allowed to keep their own book and the tricky bit is to design a mechanism that keeps the advantages of this decentralisation while ensuring, among other things, the persistence of the currency. 

### Mining

The way in which bitcoin, the best-known cryptocurrency, ensures persistence is through a mechanism called /mining/. In very simplified form, this works as follows: Let $$ B_t$$ be the complete history of bitcoin transactions up to time $$ t$$. Then there exists a number $$ H(B_t)$$ that depends on $$ B_t$$ and that has the following properties:

Given $$ B_t$$, in order to find $$ H(B_t)$$ one needs to solve a puzzle that, on average, requires a long run time on the computer, hence consuming a lot of electricity.
For two different histories $$ B_t$$ and $$ B_t'$$, it’s practically impossible to infer anything about $$ H(B_t')$$ from knowing $$H(B_t)$$, even if these two histories are almost identical.
The puzzle has no structure so that the best strategy for solving it is always to randomly guess numbers.




The basic rule in Bitcoin then is “Don’t believe any information about some history $$ B_t$$ unless it’s accompanied by $$ H(B_t)$$”. A moment of thought will reveal that this is indeed an (ingenious!) way to ensure persistence of a decentralised currency: If your bank wanted to pretend that you haven’t given them money, then they can, of course, change the history in their local book from $$ B_t$$ (the true history) to $$ B_t'$$ (the false history), but as soon as they want to spend the money they took from you, they would have to convince a third party that $$ B_t'$$ is true, but if that third party plays according to the rules then the bank will have to calculate $$ H(B_t')$$ which costs them a lot of electricity and hence if the expected cost of fraud is higher than the gain then there is no point in attempting it! *So it is the hardness of the puzzle that generates the trust necessary for the currency’s persistence!*

But what, you may ask, happens if technology advances and computer processors become much faster? Or if electricity in a country becomes cheaper? Then fraud might turn from being economically unfeasible to being feasible! But here’s the twist: *Bitcoin adjusts the difficulty of the puzzle to accommodate such changes.* More precisely, the difficulty is adjusted in such a way that the average time required for all miners, the people that do the mining, to find  $$ H(B_t)$$ is about ten minutes. In other words, Bitcoin creates persistence by making sure that the process by which it is decided who owns what is always sufficiently expensive in an external resource to disincentivize fraud. Note, however, that $$ H(B_t)$$ needs to be calculated also for the “true” history, which is why Bitcoin consumes so much electricity even when nobody attempts to cheat.

### Sacrifice rituals

What is a sacrifice ritual, in a wider sense? I don’t know a good definition but also don’t think a clear-cut one exists. Yet, I submit that the following list of properties delineates sacrifice rituals from other activities rather well: A sacrifice ritual involves

- an act of irreversibility, i.e. something gets destroyed or lost irretrievably,
- some form of hurting those that sacrifice,
- theatricality, i.e. it is usually done publicly or there is a form of proof of sacrifice,
  decadence.


Here, by *decadence*, I mean something quite specific that I want to distinguish from the notion of excess: An act is decadent if the destruction of some resource is a constitutive part of this act. In contrast, an act is excessive if it could have been realised with fewer resources than it was. To illustrate the difference, I would say that driving a Porsche car is decadent but not excessive, while accidentally heating with an open window is excessive but not decadent. I make this distinction because I don’t think that a sacrifice ritual is always excessive.

### Mining as a sacrifice ritual

I think that from my presentation of it, it is pretty clear that mining satisfies the first three of the above characteristics of a sacrifice ritual. The only question is whether it is actually decadent. Why would it not? Well, one might argue that for miners the question about whether to participate in mining has nothing decadent about it, but that instead it is driven by profitability calculations and that the energy consumption of the mining process is, for them, certainly not the purpose of doing the mining. And I would agree with that. But I think that the miners are not the relevant community here. Rather, it’s the people holding bitcoin. For *them* I think the situation is quite different: Since they rely on the persistence of the currency, and since this persistence relies on miners running their computers to run a problem that, by construction, has to be wasted on random guessing of numbers (instead of, say, trying to solve helpful problems), mining has as its explicit purpose the wasting of energy and, as such, is clearly decadent in my terminology.

A moment of thought on this also clarifies another telling parallel between mining and sacrifice rituals: They serve, partially, the same purpose, namely that of creating trust and stabilising social structure in the community where the sacrifice is carried out, such as the village or family. By sacrificing stock, for example, farmers symbolically, and publicly, reconfirm their loyalty to the community, by sacrificing private goods to the public. For instance, Hubert and Mauss in their classic essay on sacrifice write “… the act of abnegation implicit in every sacrifice, by recalling frequently to the consciousness of the individual the presence of collective forces, in fact, sustains their ideal existence.” (p.97 in *Understanding Religious Sacrifice*, ed. Jeffrey Carter)

So, what do we make of this curious little insight? For one, looking at Bitcoin in this way nicely highlights the not so surprising fact that even the most radical technological innovations often work by exactly the same basic mechanisms as the most ancient practices. Moreover, it also puts an emphasis on the important *economic* role of destructive or dissipative mechanisms. Indeed, Georges Bataille made such mechanisms the very foundation of his own theory of economics, arguing that “Bourgeois” economists such as Smith but also Marx had overlooked their relevance. Finally, understanding better the connection between mining and sacrifice rituals might allow us to find alternative and less resource-intensive ways of creating persistence for cryptocurrencies (and people, of course, look a lot for such alternatives). Specifically, we might look at other ways in which trust is created in societies and see whether any of them offer themselves for application in the context of cryptocurrencies.
