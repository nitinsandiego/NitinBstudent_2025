---
toc: false
layout: post
title: College Board Quiz Review
type: issues
permalink: /collegeboardquizreview
courses: {csa: {week: 13}}
comments: true
---

**My Score**: 36/40 or 90%

![alt text](images/Screenshot 2024-11-18 at 9.08.21 AM.png)

**Evidence of Work through quiz**

![image](images/Screenshot 2024-11-15 at 10.19.31 PM.png)
![image](images/Screenshot 2024-11-15 at 10.23.43 PM.png)
![image](images/Screenshot 2024-11-15 at 10.44.51 PM.png)
![image](images/Screenshot 2024-11-16 at 11.58.04 AM.png)
![image](images/Screenshot 2024-11-16 at 2.38.43 PM.png)
![image](images/Screenshot 2024-11-16 at 3.15.35 PM.png)
![image](images/Screenshot 2024-11-16 at 3.27.36 PM.png)
![image](images/Screenshot 2024-11-16 at 3.29.44 PM.png)
![image](images/Screenshot 2024-11-16 at 3.35.10 PM.png)
![image](images/Screenshot 2024-11-16 at 3.43.47 PM.png)
![image](images/Screenshot 2024-11-16 at 10.54.55 PM.png)
![image](images/Screenshot 2024-11-16 at 10.58.39 PM.png)

## Corrections

**Question 4**
![alttext](images/Screenshot 2024-11-18 at 9.13.09 AM.png)
I chose B or 2.3333333, while the correct answer was 2 or C. The reason B was incorrect because this would be the result if the division used was floating point division, instead of integer division. This would be the case if either x or y were of type double instead of type int or if either value was typecast as a double in the expression. 
C is correct because when we evaluate the express(x < 10) && (y < 0) for x having the value 7 and y having the value 3, x < 10 evaluates to true, since 7 is less than 10, and y < 0 evaluates to false, since 3 is not less than 0. The logic operator && evaluates to true when both conditions are true and evaluates to false otherwise. Since the second condition is false, the boolean expression is false. As a result, the compiler will skip the first output statement and execute the statement in the else. The expression x / y is integer division for 7 / 3, which is 2.

**Question 19**
![alttext](images/Screenshot 2024-11-18 at 9.19.13 AM.png)
I chose A or `(a != b) || (b < 7)`, while the correct answer was B or `(a != b) || (b <= 7)`. A is wrong because the opposite of greater than is less than or equal. Therefore, the opposite of `(b > 7)` is `(b <= 7)`. B is correct because De Morgan’s Law states that !(p && q) is equivalent to !p || !q. By applying De Morgan’s Law to this expression, we negate the first expression !(!(a !=b)) and the second expression !(b >7) to form !(!(a != b)) || !(b > 7). In the first expression the two consecutive not operators (!) cancel each other out giving us (a != b). In the second expression, the opposite of > is <= giving us (b <= 7). The equivalent expression is (a != b) || (b <= 7).

**Question 22**
![alttext](images/Screenshot 2024-11-18 at 6.32.13 PM.png)
I chose A or Line 2 will not compile because variables of type Book may not refer to variables of type AudioBook, while the correct answer was B or Line 4 will not compile because variables of type Book may only call methods in the Book class. A was wrong because objects of subclasses can be assigned to variables of the type of superclass. In this case, the array elements are of type Book and can be assigned objects of type Book or any subclass of Book. B is correct since the books array has been declared of type Book, at compile time all objects stored in books are considered Book object regardless of their actual type. Therefore, any methods that are called on elements of books must be declared in Book. In order to call the pagesPerMinute() method on Book[0], we would need to use typecasting to let the compiler know that the object stored in the books array at this index is actually an AudioBook object.

**Question 23**
![alttext](images/Screenshot 2024-11-18 at 6.38.00 PM.png)
I chose A or ["baboon", "zebra", "bass", "cat", "bear", "koala"], while the correct answer was B or ["bear", "zebra", "bass", "cat", "koala", "baboon"]. A was incorrect because this would be the correct answer if the remove occurred before the size was calculated in the statement animals.add(animals.size()-k, animals.remove(k)). B is correct because The manipulate method contains a for loop with a loop control variable k that starts at the right most index of animals, decrements by 1 each time, until k is equal to 0. In the first iteration, when k is 5, if the element of animals at 5 (“baboon”) starts with a “b”, which it does, then this value is removed from the list and inserted at index 1. The list would then be {“bear”, “baboon”, “zebra”, “bass”, “cat”, “koala”}. In the second iteration, when k is 4, the element of animals at 4 (“cat”) does not start with a “b” and no changes are made to the list. In the third iteration, when k is 3, the element of animals at 3 (“bass”) starts with a “b”. This value is removed from the list and inserted at index 3. Since it was already at index 3, the list would not change. In the fourth iteration, when k is 2, the element of animals at 2 (“zebra”) does not start with a “b” and no changes are made to the list.  In the fifth iteration, when k is 1, the element of animals at 1 (“baboon”) starts with a “b”. It is removed from the list and inserted at index 5. The list would then be {“bear”, “zebra”, “bass”, “cat”, “koala”, “baboon”}.  Finally, k decrements to 0 which is not greater than 0 so the loop terminates.

## Reflection

I got a 36/40 on the quiz which is a 90%. I think I did very well, but also I think I took a long time. I think I need to work on going faster through the questions, which will better prepare me for the AP Exam. Based on the questions I got wrong, I think I need to improve on Units 2, 3, 4, 5 and 6. This test was a good introduction on how the AP test will be like, and I think I need to work on my speed and accuracy. I think I need to work on my speed and accuracy, and I will do this by practicing more questions and reviewing the concepts I am weak on. 