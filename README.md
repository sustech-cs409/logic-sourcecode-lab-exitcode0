# logic-sourcecode-lab-exitcode0

select a `if` statement from your selected app

the path: RedReader/src/main/java/jp/tomorrowkey/android/gifplayer/[GifDecoder.java](https://github.com/QuantumBadger/RedReader/blob/8dd409f781c3613bd8b0f9b3f8f32fe0aa180db3/src/main/java/jp/tomorrowkey/android/gifplayer/GifDecoder.java)

```java
/**
	 * Gets display duration for specified frame.
	 *
	 * @param n
	 *          int index of frame
	 * @return delay in milliseconds
	 */
	public int getDelay(int n) {
		delay = -1;
		if ((n >= 0) && (n < frameCount)) {
			delay = frames.elementAt(n).delay;
		}
		return delay;
	}
```
### Step 1: Simplify the cluse
`(n >= 0) && (n < frameCount)`
* **a:** n >= 0
* **b:** n < frameCount

**p = a && b**


### Step 2: Get Predicate Coverage
**1. Make p=true**
* a=true, b=true

**2. make p=false**
* a=true, b=false
* a=false, b=true
* a=false, b=false


### Step 3: Get Clause Coverage
Two tests:
* a=true, b=true
* a=false, b=false


### Step 4: Get Combinatorial Coverage (CoC)
How many tests is need?
* 2^2 = 4

| Row# | a  | b  | p = a && b |
| ---- | -- | -- | -- |
| 1    | T  | T  | T  |
| 2    | T  | F  | F  |
| 3    | F  | T  | F  |
| 4    | F  | F  | F  |

### Step 5: Get Correlated Active Clause Coverage (CACC)
According to the CACC definition : The values chosen for the minor clauses cj must *cause p* to be true for one value of the major clause ci and false for the other
* For the major cluse **a**:
  - the row# in previous table (1, 3), the minor cluse **b** is both True. **p** is True for Row# 1 and False for Row# 3.

* For the major cluse **b**:
  - the row# in previous table (1, 2), the minor cluse **a** is both True. **p** is True for Row# 1 and False for Row# 2.

### Step 6: Get Restricted Active Clause Coverage (RACC)
According to the RACC definition : Only need the chosen minor cluses cj be the same, not for the Predicate p be the same.
However, it is the same outcome with CACC.
* For the major cluse **a**: (1, 3)
* For the major cluse **b**: (1, 2)

### Step 7: Find pc that determine p
