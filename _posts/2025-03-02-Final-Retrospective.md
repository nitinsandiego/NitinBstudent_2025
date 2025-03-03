---
toc: True
layout: post
title: Final Retrospective
type: issues
courses: {csa: {week: 24}}
---

# MC Work

My score: 36/39

While my score is good, I believe I have a lot of things to work on still. One, my timing was very poor and I spent too much time working out each problem. Even though each problem is complex and requieres a lot of thinking and working out, I must practice even more to work through them faster and be ready for the AP Exams.

# FRQ Work

## Question 1 Answers

### Part A

```java
public static int arraySum(int[] arr) {
    int sum = 0;
    for (int i = 0; i < arr.length; i++) {
        sum += arr[i];
    }
    return sum;
}
```

### Part B

```java
public static rowSums(int[][] arr2D) {
    int[] sums = new int[arr2D.length];
    for (int i = 0; i < arr2D.length; i++) {
        sums[i] = arraySum(arr2D[i]);
    }
    return sums;
}
```

### Part C

```java
public static boolean isDiverse(int[][] arr2D) {
    int[] sums = rowSums(arr2D);
    for (int i = 0; i < sums.length; i++) {
        for (int j = i + 1; j < sums.length; j++) {
            if (sums[i] == sums[j]) {
                return false;
            }
        }
    }
    return true;
}
```

## Question 2 Answers

```java
public class HiddenWord {
    private String word;

    public HiddenWord(String word) {
        this.word = word;
    }

    public String getHint(String guess) {
        String hint = "";
        for (int i = 0; i < guess.length(); i++) {
            if (guess.charAt(i) == word.charAt(i)) {
                hint += guess.charAt(i);
            } else if (word.indexOf(guess.charAt(i)) != -1) {
                hint += "+";
            } else {
                hint += "*";
            }
        }
        return hint;
    }
}
```

## Question 3 Answers

### Part A

```java
public int getValueAt(int row, int col) {
    for(SparseArrayEntry entry : entries) {
        if(entry.getRow() == row && entry.getCol() == col) {
            return entry.getValue();
        }
    }
}
```

### Part B

```java
public void removeColumn(int col) {
    int i = 0;
    while(i < entries.size()) {
        SparseArrayEntry entry = entries.get(i);
        if e.getCol() == col {
            entries.remove(i);
        } else if e.getCol() > col {
            entries.set(i, new SparseArrayEntry(e.getRow(), e.getCol() - 1, e.getValue()));
            i++;
        } else {
            i++;
        }
    }
}
```

## Question 4 Answers

### Part A

```java 
public interface NumberGroup {
    boolean contains(int num);
}
```

### Part B

```java
public class Range implements NumberGroup {
    private int min;
    private int max;

    public Range(int min, int max) {
        this.min = min;
        this.max = max;
    }

    public boolean contains(int num) {
        return num >= min && num <= max;
    }
}
```

### Part C

```java
public boolean contains(int num) {
    for(NumberGroup group : groupList) {
        if(group.contains(num)) {
            return true;
        }
    }
    return false;
}
```