# NumPy Interview Questions PDF with Answers

A free PDF of twenty multiple choice NumPy interview questions with a full answer key, [numpy-interview-questions-with-answers.pdf](numpy-interview-questions-with-answers.pdf).

Every answer is real output, every snippet was run on NumPy 2.4.4, so the answers match the current version. Each of the four options comes with the reason it is right or wrong, because the wrong ones are where you learn something.

Ten of the twenty are below. All twenty are also playable in the browser at https://thibaudlepan77-svg.github.io/interview-questions-verified/#numpy

**What does this print?**

```python
import numpy as np
a = np.array([1, 2.5, True])
print(a.dtype)
```

- **A.** `int64`
- **B.** `float64`
- **C.** `bool`
- **D.** `object`

<details><summary>Answer</summary>

**B**, as NumPy 2.4.4 printed it.

- **A**. Assumes the two non float values outvote the single float and the dtype settles on int64.
- **B**. Correct. With bool, int and float all present, NumPy still promotes to the widest of the three, float64.
- **C**. Assumes the presence of a boolean anywhere forces the narrower bool dtype regardless of the other values.
- **D**. Assumes a three way mix of value kinds is too ambiguous for a numeric dtype and falls back to object.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-01.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.array([1, 2, 3], dtype=np.float32)
b = a + 1.5
print(b.dtype)
```

- **A.** `int64`
- **B.** `float32`
- **C.** `float64`
- **D.** `object`

<details><summary>Answer</summary>

**B**, as NumPy 2.4.4 printed it.

- **A**. Assumes mixing a float32 array with a Python float drops back to a whole number dtype.
- **B**. Correct. The same NEP 50 rule applies to floats, a Python float added to a float32 array keeps the result float32 rather than upgrading it to float64.
- **C**. Assumes the bare Python float on the right widens the result to the default double precision dtype, the way older NumPy versions behaved.
- **D**. Assumes this kind of mixed operation needs a generic object dtype to represent the result.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-03.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.array([10, 20, 30, 40, 50])
fancy = a[[0, 1, 2]]
fancy[0] = 999
print(a.tolist())
```

- **A.** `[999, 20, 30]`
- **B.** `[10, 20, 30]`
- **C.** `[10, 20, 30, 40, 50]`
- **D.** `[999, 20, 30, 40, 50]`

<details><summary>Answer</summary>

**C**, as NumPy 2.4.4 printed it.

- **A**. Assumes the edit does reach the original array but only up to the length of the fancy selection.
- **B**. Assumes the entire original array was replaced by the shorter fancy selection.
- **C**. Correct. Fancy indexing always returns a new array, so changing fancy afterward has no effect on the original array a, which stays 10, 20, 30, 40, 50.
- **D**. Assumes fancy indexing returns a view into the same memory, so the edit reaches back into the original array.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-05.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.arange(3)[:, np.newaxis]
b = np.arange(4)[np.newaxis, :]
print((a + b).tolist())
```

- **A.** `[[0, 1, 2, 3], [0, 1, 2, 3], [0, 1, 2, 3]]`
- **B.** `[[0, 1, 2, 3], [1, 2, 3, 4], [2, 3, 4, 5]]`
- **C.** `[[0, 0, 0, 0], [1, 1, 1, 1], [2, 2, 2, 2]]`
- **D.** `[[0, 1, 2], [1, 2, 3], [2, 3, 4], [3, 4, 5]]`

<details><summary>Answer</summary>

**B**, as NumPy 2.4.4 printed it.

- **A**. Ignores the contribution of a entirely and repeats b unchanged on every row.
- **B**. Correct. Each row i adds the constant a value i to every entry of b, so row 0 is b itself, row 1 is b plus 1, and row 2 is b plus 2.
- **C**. Ignores the contribution of b entirely and repeats each value of a across a whole row.
- **D**. Transposes the grid, producing 4 rows of length 3 instead of 3 rows of length 4.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-07.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.arange(6)
b = a[[1, 2, 3]]
print(b.base is None)
```

- **A.** `False`
- **B.** `True`
- **C.** `AttributeError`
- **D.** `None`

<details><summary>Answer</summary>

**B**, as NumPy 2.4.4 printed it.

- **A**. Assumes any array built from indexing another array must carry a base pointing back to it.
- **B**. Correct. Fancy indexing produces an independent array that owns its own memory, so it has no source array to point back to and its base is None.
- **C**. Assumes an array produced by indexing has no base attribute to check at all.
- **D**. Assumes base reports the missing marker None as a printed value instead of the array being asked whether its base is that value.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-09.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.array([[1, 2, 3], [4, 5, 6]])
print(a.sum(axis=1).tolist())
```

- **A.** `[6, 15]`
- **B.** `21`
- **C.** `[3, 6]`
- **D.** `[5, 7, 9]`

<details><summary>Answer</summary>

**A**, as NumPy 2.4.4 printed it.

- **A**. Correct. axis=1 collapses the columns and adds across each row, giving 1+2+3 for the first row and 4+5+6 for the second.
- **B**. Collapses the whole array into one grand total instead of one sum per row.
- **C**. Keeps only the last entry of each row rather than adding the whole row.
- **D**. Sums down each column instead, the result for axis=0 on the same array.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-11.html)

</details>

**What does this print?**

```python
import numpy as np
b = np.array([[1, 2], [3, 4], [5, 6]])
print(b.argmax())
```

- **A.** `5`
- **B.** `6`
- **C.** `(2, 1)`
- **D.** `1`

<details><summary>Answer</summary>

**A**, as NumPy 2.4.4 printed it.

- **A**. Correct. Flattened in row major order the values are 1, 2, 3, 4, 5, 6, and the largest one, 6, sits at the last position, index 5.
- **B**. Confuses the index of the maximum with the maximum value itself.
- **C**. Assumes argmax returns the row and column coordinates as a tuple instead of a single flat index.
- **D**. Confuses the index of the maximum with the row it happens to sit in.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-13.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.array([1, 2], dtype=np.int8)
print((a + 127).tolist())
```

- **A.** `OverflowError`
- **B.** `[126, 127]`
- **C.** `[-128, -127]`
- **D.** `[128, 129]`

<details><summary>Answer</summary>

**C**, as NumPy 2.4.4 printed it.

- **A**. Assumes the Python int 127 does not fit an int8 array and must raise before any arithmetic happens.
- **B**. Subtracts instead of adds, as if the operator had been reversed.
- **C**. Correct. 127 fits within int8 so the addition proceeds, but the true sums, 128 and 129, both overflow int8 and wrap to negative 128 and negative 127.
- **D**. Assumes the addition returns the true mathematical sums without wrapping them into the int8 range.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-15.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.array([[3, 1], [2, 4]])
print(np.sort(a, axis=1).tolist())
```

- **A.** `[[1, 3], [2, 4]]`
- **B.** `[[2, 1], [3, 4]]`
- **C.** `[[3, 1], [4, 2]]`
- **D.** `[[1, 2], [3, 4]]`

<details><summary>Answer</summary>

**A**, as NumPy 2.4.4 printed it.

- **A**. Correct. axis=1 sorts each row independently across its columns, so 3, 1 becomes 1, 3 and 2, 4 stays 2, 4.
- **B**. Sorts along the columns instead of the rows, the result axis=0 would actually give.
- **C**. Sorts each row in descending order instead of the default ascending order.
- **D**. Assumes the whole array gets flattened, sorted, and reshaped back, ignoring the axis argument entirely.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-17.html)

</details>

**What does this print?**

```python
import numpy as np
a = np.arange(9)
print(np.split(a, 3))
```

- **A.** `[array([0, 1, 2]), array([3, 4, 5])]`
- **B.** `[array([0, 1, 2]), array([3, 4, 5]), array([6, 7, 8])]`
- **C.** `[array([0, 3, 6]), array([1, 4, 7]), array([2, 5, 8])]`
- **D.** `[array([0, 1, 2, 3, 4, 5, 6, 7, 8])]`

<details><summary>Answer</summary>

**B**, as NumPy 2.4.4 printed it.

- **A**. Drops one of the three expected pieces from the result.
- **B**. Correct. split with an integer count of 3 cuts the nine values into three equal, contiguous chunks in order, and it returns a plain Python list of the resulting arrays.
- **C**. Assumes split distributes the values round robin across the pieces instead of keeping each chunk contiguous.
- **D**. Assumes split with a count argument returns the array untouched inside a single element list.

[Play it in the browser](https://thibaudlepan77-svg.github.io/interview-questions-verified/q/numpy-19.html)

</details>

## The full bank

These come from a bank of 279 NumPy questions built the same way, sold as a PDF, [9 euros on Ko-fi](https://ko-fi.com/s/bc22cdcdd3). SQL, Python, pandas and NumPy together are [19 euros](https://ko-fi.com/s/8151d45764).

If an answer looks wrong to you, open an issue with the question and what your own run prints.
