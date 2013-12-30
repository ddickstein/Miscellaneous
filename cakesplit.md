## The Problem ##

I have come across various restatements of the cake-splitting problem on the net, and I'm sure this solution does not satisfy all of them.  My goal in this algorithm is to suggest a means by which a cake can be split among N people such that each individual feels confident that they received at least 1/N of the cake.  My assumption is that even if an individual believes that his friend received more cake than he, he will still not be disappointed so long as he believes he has received at least 1/N.

Note: *This is a solution I thought of indepenently, but I'm sure others have thought of it before me.  I have heard several approaches to this problem and thought I would post my own.*

## Solution for 3 People ##

I will consider the problem for three people, and then abstract it out to its more recursive form.  Say you have three people, Adam, Ben, and Cindy, splitting a cake.  Adam cuts the cake into three equal pieces (therefore Adam would be equally happy receiving any of those three pieces as his portion).  Ben and Cindy may not see the pieces as equal at all.  Let Ben and Cindy each select the two pieces of the three that they think are the biggest.

If Ben and Cindy select the same two pieces, the solution is trivial.  Adam takes the piece the both rejected, and Ben and Cindy then re-split the two pieces they want (e.g. Ben splits the total portion and Cindy chooses).  Thus Adam, Ben, and Cindy all believe they have at least 1/3 each - Adam believed he had 1/3 from the get-go, and Ben and Cindy both believe they got at least half of a portion that was greater than or equal to 2/3.

If Ben and Cindy select different pieces then the solution is a little trickier.  If Ben and Cindy are both selecting 2 pieces, there must be one piece they both select as the biggest.  They split that piece.  Then Ben splits the other piece he chose with Adam, and Cindy splits the other piece she chose with Adam.  Thus Adam gets at least 1/2 of each of the 1/3 pieces he originally cut, so he is happy, and Ben and Cindy both get at least 1/2 of the two pieces they felt were greater than or equal to 2/3, so they each end up with at least 1/3 and they are happy as well.

Another way to think about what happens is to assign names to the pieces that are cut.  Here Adam cuts the cake, and then Ben and Cindy choose their preferences.  We can create a preference chart as follows:

    +-----------+-----------+-----------+      +-----------+-----------+-----------+
    |  Piece 1  |  Piece 2  |  Piece 3  |      |  Piece 1  |  Piece 2  |  Piece 3  |
    +-----------+-----------+-----------+      +-----------+-----------+-----------+
    |    Ben    |    Ben    |           |  OR  |    Ben    |    Ben    |           |
    +-----------+-----------+-----------+      +-----------+-----------+-----------+
    |   Cindy   |   Cindy   |           |      |   Cindy   |           |   Cindy   |
    +-----------+-----------+-----------+      +-----------+-----------+-----------+

The remaining slots are automatically filled by the cake cutter, because the person who cuts by default has no preference:

    +-----------+-----------+-----------+      +-----------+-----------+-----------+
    |  Piece 1  |  Piece 2  |  Piece 3  |      |  Piece 1  |  Piece 2  |  Piece 3  |
    +-----------+-----------+-----------+      +-----------+-----------+-----------+
    |    Ben    |    Ben    |   Adam    |  OR  |    Ben    |    Ben    |   Adam    |
    +-----------+-----------+-----------+      +-----------+-----------+-----------+
    |   Cindy   |   Cindy   |   Adam    |      |   Cindy   |   Adam    |   Cindy   |
    +-----------+-----------+-----------+      +-----------+-----------+-----------+

Then each of the 3 pieces gets 2 names, and ends up getting split in two between the individuals with a preference for that piece.

## Solution for N People ##

This concept can be abstracted out to a recursive solution.  If you have a cake that must be split between N people, have person N cut the cake into N pieces.  Then the N-1 people each express N-1 preferences for the different pieces (basically each of them expresses a preference for every piece he or she wants aside from one).  Then the gaps in the preference chart are filled in by person N, who has no preference.  The result is that the N pieces each have a list of N-1 people with a preference for that piece.  Each of those pieces in turn gets recursively split according to this exact algorithm, the base case of which is a 2-way split in which one person splits and the other picks.

### 4-Person Example ###

Here is an example of this algorithm being applied for 4 people - Adam, Ben, Cindy, and Danielle.  Danielle is person N (person 4), so she cuts the cake into four pieces.  Now we make a preference chart for those four pieces.  Say the preference chart falls like this:

    +-----------+-----------+-----------+-----------+
    |  Piece 1  |  Piece 2  |  Piece 3  |  Piece 4  |
    +-----------+-----------+-----------+-----------+
    |   Adam    |   Adam    |           |   Adam    |
    +-----------+-----------+-----------+-----------+
    |           |    Ben    |    Ben    |    Ben    |
    +-----------+-----------+-----------+-----------+
    |   Cindy   |           |   Cindy   |   Cindy   |
    +-----------+-----------+-----------+-----------+

We then fill Danielle into the gaps:

    +-----------+-----------+-----------+-----------+
    |  Piece 1  |  Piece 2  |  Piece 3  |  Piece 4  |
    +-----------+-----------+-----------+-----------+
    |   Adam    |   Adam    | Danielle  |   Adam    |
    +-----------+-----------+-----------+-----------+
    | Danielle  |    Ben    |    Ben    |    Ben    |
    +-----------+-----------+-----------+-----------+
    |   Cindy   | Danielle  |   Cindy   |   Cindy   |
    +-----------+-----------+-----------+-----------+

Now pieces 1 through 4 must be divied up into 3 pieces each (I'm not going to draw a chart for each one, but here is a brief rundown of how it would work).

For piece 1, Cindy will cut the piece in 3, Adam and Danielle will each express preferences for 2 of the 3, Cindy will fill in the gaps, and then those pieces will each be split in 2.

For piece 2, Danielle will cut the piece in 3, Adam and Ben will each express preferences for 2 of the 3, Danielle will fill in the gaps, and then those pieces will each be split in 2.

For piece 3, Cindy will cut the piece in 3, Danielle and Ben will each express preferences for 2 of the 3, Cindy will fill in the gaps, and then those pieces will each be split in 2.

For piece 4, Cindy will cut the piece in 3, Adam and Ben will each express preferences for 2 of the 3, Cindy will fill in the gaps, and then those pieces will each be split in 2.

Truly it does not matter at each point who does the splitting and who expresses preferences, but it's simple to implement as person N always does the splitting.

I truly hope this explanation was clear - if not, please leave comments and/or edits.  Enjoy your cake!
