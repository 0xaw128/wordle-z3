<b>note</b>: this was used before it moved over to the NYT so the `get_dict.py` doesn't work anymore

--------------

wordle solver
=============

wordle is cool. I also want to learn Z3 and be better at wordle.

its basically hangman+. you get 5 guesses for a 5 letter word, and with each word guess it states whether a letter either doesnt exist in the answer, exists but you entered it at the wrong position, or it exists and you entered it in the right position.

this script supports n length words though, not just 5.

requirements
------------

- z3-solver

usage
-----

```sh
# begin to solve
python3 solve.py
# enter the constraints to determine the word to enter into the wordle website
# the first should be 'slate' because it seems to work well
# run the solve.py script every time when wanting to find the next word
# which is super hacky
```

notes on constraints:
* the gray constraints are just the excluded letters
* the gold constraints are the letter and position pairs separated by a
* the green constraints are the letter, position, and occurrence pairs separated by a . T for occurrence means it occurs only once, F means multiple times or unknown

the constraints need not be strictly appended, as if letters are found to be green and occur once, having the same letter as a gold constraint is not necessary but it works either way.

for example, for 2022-01-16:
1. entering 'slate' reveals 's' green, 'la' gold, 'te' gray
	- constraints are `te,l1.a2,s0F`. this produces 'salad'
2. entering 'salad' now reveals 'la' as green, 'ad' as gray
	- constraint are now `ted,l1.a2,s0F.l2F.a3T`. this produces 'solar' which is correct.

```
Wordle 211 3/6

🟩🟨🟨⬛⬛
🟩⬛🟩🟩⬛
🟩🟩🟩🟩🟩
```
