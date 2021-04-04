
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
- Inconsistent spellings can cause disinformation. -> Spelling similar concepts similarly is needed.
	- ex. `O and l` that can be misunderstood as `0 and 1` respectively.
## Make Meaningful Distinctions
- If there are differences on names, there should be something different.
- Number-series naming
	- ex. `a1, a2, ..., aN`
	- non-informative; not providing a clue for author's intention.
	- ex.
```
public static void copyChars(char a1[], char a2[]) {
	for(int i = 0; i < a1.length; i++) {
		a2[i] = a1[i];
	}
}
```
This function would be more helpful when `char a1[]` and `char a2[]` are named as `source` and `destination`.
- Noise words
	- ex. `ProductInfo`, `ProductData` in `Class Product`: indistinct noise on `Info` and `Data`
	- Noise words are redundant.
- **Distinguish names should offer differences to readers.**

## Use Pronounceable Names
- The variables names should be pronounceable. Because programming is a social activity.
```
class DtaRcrd102 {
    private Date genymdhms;
    private Date modymdhms;
    private final String pszqint = "102";
}
```
```
class Customer {
    private Date generationTimeStamp;
    private Date modificationTimeStamp;
    private final String recordId = "102";
}
```
## Use Searchable Names
- Longer names and searchable names are recommended than short names and a constant.
- ex. **e**
	- the most common letter in English
	- If it is defined as a variable, it could be found every code line.
- Single-letter names used as local-variables.
- If a variable/constant shows up multiple places, it should be given a search-friendly name.
```
for(int j = 0; j < 34; j++) {
	s += (t[j]*4) / 5;
```
```
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;
for(int j = 0; j < NUMBER_OF_TASKS; j++) {
	int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
	int realTaskWeeks = (realdays / WORK_DAYS_PER_WEEK);
	sum += realTaskWeeks;
```
- `sum`: not a useful name but at least searchable than `s`
- The intentionally named code makes a longer function, but much easier to find `WORK_DAYS_PER_WEEK` than `5` itself.
## Avoid Encodings
### Hungarian Notation
[Hungarian notation](https://en.wikipedia.org/wiki/Hungarian_notation)
## Class Names
- Classes and objects should have noun or noun phrase names.
- ex. `Customer`, `WikiPage`, `Account`, and `AddressParser`
- Not Recommended: `Manager`, `Processor`, `Data`, or `Info`
- A verb cannot be used as a class name.
## Method Names
- Methods should have verb or verb phrase names
- ex. `postPayment`, `deletePage`, or `save`
```
string name = employee.getName();
customer.setName("mike");
if(paycheck.isPosted()) ...
```
- When constructors are overloaded, use static methods with names describing the arguments.
`Complex fulcrmPoint = Complex.FromRealNumber(23.0);` is better than `Complex fulcrumPoint = new Complex(23.0);`
## Don't Be Cute
- Choose clarity over entertainment value.
- **Say what you mean. Mean what you say.**
## Pick One Word per Concept
- Choose one word for one abstract concept and stick with it for total code.
- ex. `DeviceManager`-`ProtocolController`: choose one 'manager' or 'controller' and use one.
## Don't Pun
- Do not use the same word for multiple purposes.
- ex. `add` for "adding or concatenating two values"
	- if defining method that puts its single parameter into a collection, is it appropriate to use `add`?
	- -> using `insert` or `append` is appropriate instead of add.
## Add Meaningful Context
- Names in context should be placed by enclosing them in well-named classes, functions, or namespaces.
```
private void printGuessStatistics(char candidate, int count) {
	String number;
	String verb;
	String pluralModifier;
	if(count == 0) {
		number = "no";
		verb = "are";
		pluralModifier = "s";
	} else if(count == 1) {
		number = "1";
		verb = "is";
		pluralModifier = "";
	} else {
		number = "Integer.toString(count)";
		verb = "are";
		pluralModifier = "s";
	}
	String guessMessage = String.format("There %s %s %s%s", verb, number, candidate, pluralModifier);
	print(guessMessage);
}
```
```
public class GuessStatisticsMessage {
	private String number;
	private String verb;
	private String plurarlModifier;
	
	public String make(char candidate, int count) {
		createPluralDependentMessageParts(count);
		return String.format("There %s %s %s%s", verb, number, candidate, pluralModifier);
	}
	
	private void createPluralDependentMessageParts(int count) {
		if(count == 0) {
			thereAreNoLetters();
		} else if(count == 1) {
			thereIsOneLetter();
		} else {
			thereAreManyLetters(count);
		}
	}

	private void thereAreManyLetters(int count) {
		number = Integer.toString(count);
		verb = "are";
		pluralModifier = "s";
	}

	private void thereIsOneLetter() {
		number = "1";
		verb = "is";
		pluralModifier = "";
	}

	private void thereAreNoLetters() {
		number = "no";
		verb = "are";
		pluralModifier = "s";
	}
}
```
## Don't Add Gratuitous Context
- As long as shorter names are clear, they are better than longer ones.
- Examples:
	- `Address`: fine name for class
	- `accountAddress`, `customerAddress`: fine names for instances of the class `Address`
	- `PostalAddress`, `MAC`, `URI` <=> post address, MAC address, web address
