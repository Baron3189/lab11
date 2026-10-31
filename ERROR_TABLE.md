# Error table

One row per failure. Fill in every column. You need at least eight rows.

| Scenario | Function that detects it | Error value | What the player sees |
|---|---|---|---|
| Scenario | Function that detects it | Error value | What the player sees |
|---|---|---|---|
| Fleet file does not exist | `load_fleet` | `Err(DataError::Io(..))` (kind `NotFound`) | `Error: could not load data/fleet.txt: No such file or directory (os error 2)`, then the game exits with code 1 |
| A directory given as the fleet path (`data`) | `load_fleet` | `Err(DataError::Io(..))` | `Error: could not load data: Is a directory (os error 21)`, then exit code 1 |
| Fleet file with only comments (`fleet_empty.txt`) | `load_fleet` | `Err(DataError::NoShips("data/fleet_empty.txt"))` | `Error: could not load data/fleet_empty.txt: no valid ships in data/fleet_empty.txt`, then exit code 1 |
| Fleet file where every line is bad (`fleet_all_bad.txt`) | `load_fleet` | `Err(DataError::NoShips("data/fleet_all_bad.txt"))` | `Error: could not load data/fleet_all_bad.txt: no valid ships in data/fleet_all_bad.txt`, then exit code 1 |
| Board file with nine rows (`broken_rows.txt`) | `parse_board`, called by `load_board` | `Err(DataError::Board(BoardError::WrongRowCount(9)))` | `Practice board unavailable: bad board layout: found 9 rows, but the board needs exactly 10`, then back to the menu |
| Board file with a bad character (`broken_char.txt`) | `parse_board`, called by `load_board` | `Err(DataError::Board(BoardError::BadChar { line: 6, ch: 'x' }))` | `Practice board unavailable: bad board layout: line 6 has 'x', but only '.' (water) and 'S' (ship) are allowed`, then back to the menu |
| Scores file missing | `load_scores` | `Ok(Vec::new())` (normal, not an error) | `  no scores yet` in the menu |
| Scores file that cannot be written | `append_score` | `Err(DataError::Io(..))` | `Could not save the score: Permission denied (os error 13)`, then back to the menu |
| `K11` typed at the prompt | `parse_coord` | `Err(CoordError::ColumnOutOfRange('K'))` | `column K is off the board (A-J)`, asked again, no shot counted |

Scenarios to cover (add more if you find them):

- fleet file missing
- a directory given as the fleet path
- fleet file with only comments
- fleet file where every line is bad
- board file with nine rows
- board file with a bad character
- scores file missing
- scores file that cannot be written
- `K11` typed at the prompt
