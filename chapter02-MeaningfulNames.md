# Chapter 02. Meaningful Names
## Use Intention-Revealing Names
- Names should **REVEAL INTENT**
- Choosing good names takes time but saves more than it takes.
- **If a name needs further explanation, then the name is not appropriate for representing itself.**
- ex. elapsed time in days
	- `int d;`
	- `int elapsedTimeInDays;`, `int daysSinceCreation;`, `int daysSinceModification;`, `int fileAgeInDays;`
	- The latter are names for specifying the range and limitation of variables.
- ex. 
```
public List<int[]> getThem() {
	List<int[]> list1 = new ArrayList<int[]>();
	for(int[] x : theList) {
		if(x[0] == 4)
			list1.add(x);
	}
	return list1;
}
```
The problem is **NOT THE SIMPLICITY** of the code but **THE IMPLICITY** of the code.
```
public List<int[]> getFlaggedCells() {
	List<int[]> flaggedCells = new ArrayList<int[]>();
	for(int[] cell : gameBoard) {
		if(cell[STATUS_VALUE] == FLAGGED)
			flaggedCells.add(cell);
	}
	return flaggedCells;
}
```
The simplicity of the code has not changed. But the code has become more explicit by naming the variables more clearly than before.
```
public List<Cell> getFlaggedCells() {
	List<Cell> flaggedCells = new ArrayList<Cell>();
	for(Cell cell : gameBoard) {
		if(cell.isFlagged())
			flaggedCells.add(cell);
	}
	return flaggedCells;
}
```
By using `Class`, it is able to create an intention-revealing function(ex. `isFlagged()`).

## Avoid Disinformation
- Programmers should avoid words with entrenched meanings vary from their intended meaning.
	- ex. `hp`, `aix`, `sco`: names of Unix platforms or variants.
	- ex. `accountList` while it's not actually `List` -> `accountGroup`, `accounts`
- Be careful with names having difference in small part.
- ex. `XYZControllerForEfficient**Handling**OfStrings`, `XYZControllerForEfficient**Storage**OfStrings`
