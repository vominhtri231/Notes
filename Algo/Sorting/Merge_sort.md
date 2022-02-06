# Merge sort

## Pseudo code

- Calculate middle point
- Sort each half
- Merge them together

## Pros and cons

- Work great with sorting linked list, where insertion is O(1)
- Can be used to find inversion count
- Require additional data when merging array
- Slow compare to others for small input

## Example

```java
  public void mergeSort(int[] input) {
    mergeSort(input, 0, input.length - 1);
  }

  private void mergeSort(int[] input, int l, int r) {
    if (l >= r) {
      return;
    }

    int mid = (l + r) / 2;

    mergeSort(input, l, mid);
    mergeSort(input, mid + 1, r);

    merge(input, l, mid, r);
  }

  private void merge(int[] input, int l, int mid, int r) {
    int[] firstHalf = Arrays.copyOfRange(input, l, mid + 1);
    int[] secondHalf = Arrays.copyOfRange(input, mid + 1, r + 1);

    int i = 0;
    int j = 0;
    int saveIndex = l;

    while (i < firstHalf.length && j < secondHalf.length) {
      if (firstHalf[i] <= secondHalf[j]) {
        input[saveIndex] = firstHalf[i];
        i++;
      } else {
        input[saveIndex] = secondHalf[j];
        j++;
      }
      saveIndex++;
    }

    while (i < firstHalf.length) {
      input[saveIndex] = firstHalf[i];
      i++;
      saveIndex++;
    }

    while (j < secondHalf.length) {
      input[saveIndex] = secondHalf[j];
      j++;
      saveIndex++;
    }
  }
```
