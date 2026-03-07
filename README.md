# Stranded

A word puzzle game inspired by the NYT Strands. Find all the hidden theme words in the grid by tracing paths through adjacent letters (including diagonals). One special word — the **spangram** — spans the entire board edge to edge.

## How to Play

- **Drag** (or tap) through adjacent letters to form words
- Find all the **theme words** hidden in the grid
- The **spangram** (highlighted in yellow when found) connects opposite edges of the board
- Finding non-theme words earns **hint credits** — every 3 non-theme words gives you a hint
- Use hints to reveal letters of an unfound word

## Files

- `index.html` — the game
- `maker.html` — puzzle maker for creating custom puzzles

## Custom Puzzles

Create custom puzzles via URL parameters:

```
index.html?theme=THEME&spangram=SPANGRAM&words=WORD1,WORD2,WORD3,...
index.html?theme=all+in+the+family&spangram=FUNNYONE&words=UPLAND%2CCARDS%2CSUSHI%2CWAFFLES%2CMOVIES%2CDOGGIES%2CBIGB
```

The total letter count (spangram + all words) must equal exactly **48** to fill the 8×6 grid.

### Pinning a Layout

The generator tries many board layouts and picks the best one. To lock in a specific layout, add `&layout=N` where N is the attempt number. The debug panel shows a copyable "Layout URL" after each generation so you can share the exact board you're looking at.

```
```

file:///home/depps/code/stranded/index.html?theme=Hiking+with+Seth&spangram=BULLSHIT&words=COMPLAIN%2CBRIDGES%2CHATS%2CWATERS%2CBLUEBARN%2CROLLING&layout=927

file:///home/depps/code/stranded/index.html?theme=all+in+the+family&spangram=FUNNYONE&words=UPLAND%2CCARDS%2CSUSHI%2CWAFFLES%2CMOVIES%2CDOGGIES%2CBIGB&layout=3271

# FAM
https://dougepps.github.io/stranded/index.html?theme=all+in+the+family&spangram=FUNNYONE&words=UPLAND%2CCARDS%2CSUSHI%2CWAFFLES%2CMOVIES%2CDOGGIES%2CBIGB&layout=3271

fam https://tinyurl.com/y3ajpkux

# Hike

Hiking with Seth
BULLSHIT, COMPLAIN, BRIDGES, HATS, WATERS, BLUEBARN, ROLLING

https://dougepps.github.io/stranded/index.html?theme=Hiking+with+Seth&spangram=BULLSHIT&words=COMPLAIN%2CBRIDGES%2CHATS%2CWATERS%2CBLUEBARN%2CROLLING&layout=927

hike  https://tinyurl.com/5n86bkwx

### Example

```
index.html?theme=Hiking+with+Seth&spangram=BULLSHIT&words=COMPLAIN,BRIDGES,HATS,WATERS,BLUEBARN,ROLLING
```

## Puzzle Generation

The generator uses a seeded PRNG (based on a hash of the puzzle inputs) so reloading the same puzzle always produces the same board. The algorithm:

1. **Place the spangram** first, since it must span edge to edge
2. **Place theme words** one at a time, preferring cells adjacent to already-placed words
3. **Island checking** — after each placement, flood-fill empty regions to ensure none are smaller than the shortest remaining word (prevents unfillable gaps)
4. **Straighten paths** — a second pass finds non-crossing paths through each word's cells, checking both self-crossings and inter-word crossings, then reassigns letters along the clean path

## Running

Open `index.html` in a browser. No build step, no dependencies — it's a single self-contained HTML file.
