Explained in picturesarXiv 1706.03762 · NIPS 2017

# How AI learned to read a whole sentence *at once*

The 2017 Google paper behind the “T” in ChatGPT, explained with pictures and as few words as possible.

12 JUN 2017

31st Conference on Neural Information Processing Systems (NIPS 2017)

Attention Is All You Need

Ashish Vaswani · Noam Shazeer · Niki Parmar · Jakob Uszkoreit · Llion Jones · Aidan N. Gomez · Łukasz Kaiser · Illia Polosukhin

Google Brain · Google Research · University of Toronto

Every word is linked to every other word. The orange lines show where “it” looks, and the thickest one goes to “robot”.

1

## Old AI read one word at a time.

It passed a small note from word to word, so long sentences got blurry and every step waited for the one before. The Transformer lets every word look at every other word, all in one step.

In the paper**recurrent** networks, replaced by **self-attention** (Table 1)

### Before: a chain

9 turns, one after another. News of “robot” reaches “it” after **5 hand-offs**.

### Transformer: a web

Every pair at the same time. “it” sees “robot” **directly**.

The same nine words, read two ways.

2

## Who is “it”?

To understand “it”, the model checks every word and leans on the ones that fit. Change one word and the lean moves. A translator needs this: in German, “it” is *sie* for the box but *er* for the robot.

In the paper**attention** weights. Figure 4 shows real attention heads working out what “its” refers to.

### …because it was heavy.

“it” is the box, 54%. German: **sie** (die Kiste).

### …because it was clumsy.

“it” is the robot, 57%. German: **er** (der Roboter).

Line thickness shows how much “it” leans on each word. The percentages are made up for teaching.

3

## Ask, match, mix.

Every word carries three cards: a question, a name tag, and its meaning. Each question is matched against every name tag, and each word mixes in the meanings of its best matches.

In the paper**query** (the question), **key** (the name tag), **value** (the meaning)

### 1 · Ask

“it” asks a question. Every word shows a name tag.

### 2 · Match

Good matches get big shares.

### 3 · Mix

The new “it” is a mix: 57% robot.

### The paper’s version: one line

This happens for every word at the same time. Real questions and name tags are lists of numbers, not sentences. The paper writes all three steps as one line (its Equation 1); dividing by √64 = 8 keeps the scores from getting too big.

4

## Eight looks at once.

One look can’t notice everything. So the model takes 8 looks side by side, like 8 readers with 8 highlighters, and glues their notes together.

In the paper**multi-head attention**: 8 heads of 64 numbers each (Figure 2)

Each head learns its own job during training. These jobs are examples; the paper’s Figures 3 to 5 show real heads doing jobs like these.

5

## Who sits where?

Looking at everything at once loses the order: “dog bites man” and “man bites dog” look the same. So every word gets a stamp of its seat number, drawn with clock hands.

In the paper**positional encoding**, made of sine and cosine waves

### Without seats

Same words, same jar. The order is gone.

### With seat stamps

A fast, a medium and a slow hand give every seat its own pattern.

The hands are drawn at their real angles from the paper’s formula. The real stamp has 256 hands; the slowest turns about 10,000 times slower than the fastest.

6

## A Reader and a Writer.

The Reader turns the English into notes. The Writer writes German while checking those notes. Each is a tower of 6 floors, and every floor does the same thing: look, then think.

In the paper**encoder** (the Reader) and **decoder** (the Writer), N = 6 layers each (Figure 1)

- look at the other words
- look at the Reader’s notes
- think it over

The paper’s Figure 1, redrawn as two towers. Inside, each word is a list of 512 numbers; the “think” step briefly widens it to 2,048.

7

## It writes one word at a time.

The Writer picks the most likely next word, adds it, and goes again. It can never peek at words it hasn’t written yet.

In the paper**auto-regressive** decoding, with a **mask** that hides future words

Each row is one moment. Orange is the word being written now; dashed chips are words that don’t exist yet. Chatbots write their answers the same way. The options at “er” are made up for teaching.

8

## Better, and much cheaper.

It beat the best translation systems of its day and needed a fraction of the computer time to train.

In the paperTable 2: English-to-German news translation (WMT 2014), scored in **BLEU**

### Trained in 12 hours

On one machine with 8 graphics chips. The big version trained for 3.5 days.

### 23 times less work

Score **27.3** against 26.4 for the best system before it. Higher is better. The big version scored 28.4.

Base model compared with the best earlier system, a group (ensemble) of ConvS2S models. Training work is counted in calculations (FLOPs), as in the paper’s Table 2.

9

## Where it went.

The two towers became the blueprints for modern AI. GPT stands for Generative Pre-trained Transformer, and today’s chatbots are giant Writers.

From one paper to today’s chatbots.

## The whole idea, in four steps

1. Stamp every word with its seat.
2. Every word asks, matches and mixes, 8 ways at once.
3. Repeat on 6 floors.
4. Write the answer one word at a time.

[Read the paper on arXiv](https://arxiv.org/abs/1706.03762)

Numbers marked as examples are teaching props, not measurements from the model. Facts about the model and its results come from the paper, arXiv:1706.03762.
