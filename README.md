# Yavalath

This is an engine and AI player for the [Yavalath][yl] 2-player board
game. The goal is to form 4-in-a-row without first forming 3-in-a-row.

The game has 61 hex tiles, and internally the game state is
represented using a pair of 64-bit bitboards, one for each player. The
rules are encoded as two bit mask tables, and detecting wins and
losses is just a handful of bit operations.

The AI has an API, documented in `yavalath.h`, and can be plugged into
a variety of interfaces. For embedding, consider using the
amalgamation build (`make amalgamation`), which will reduce the AI
sources to one source file (`yavalath.c`) and won't require an
intermediate build program.

For a user interface, only a minimal, crude CLI is available since the
focus is on creating an AI player. The input must be in [Susan
notation][sus]. For example, the upper-left tile is `a1` and the
bottom-right tile is `i5`.

           1 2 3 4 5
        a . . . . . 6
       b . . . . . . 7
      c . . . . . . . 8
     d . . . . . . . . 9
    e . . . . . . . . .
     f . . . . . . . . 9
      g . . . . . . . 8
       h . . . . . . 7
        i . . . . . 6
           1 2 3 4 5

The AI is a [UCT Monte Carlo tree search][mcts] and it's a decent
player. However, it suffers from UCT's "shallow trap" problem and can
easily be defeated once you recognize its blind spots.


[yl]: http://cambolbro.com/games/yavalath/
[sus]: http://www.stephen.com/sue/sue_man.txt
[mcts]: https://en.wikipedia.org/wiki/Monte_Carlo_tree_search
