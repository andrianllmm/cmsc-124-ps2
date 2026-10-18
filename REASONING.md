# Reasoning Before Execution

Write the rule behind each case before you commit your predictions. Replace
every placeholder line below with one to three sentences that name the rule
producing that case's value, type, length, and dimensions. One rule is enough.
After you run and find a miss, add a short correction entry under that case in a

## P01

c() goes up the ladder to the highest type. As per the coercion hierarchy, 3.5 (double) has a higher precedence than TRUE (logical) and 2L (integer). So TRUE becomes 1 and 2L becomes 2, ending with a total length of 3 and no dimensions.

## P02

The value "2" contains a string, making it a character. The hierarchy follows the highest precedence so in this case it makes everything turn into a character, wherein 1L becomes "1" and TRUE becomes "TRUE". The value becomes ["1","2","TRUE"] with a length of 3 and no dimension.

## P03

Both c(10L,20L,30L,40L) and c(1L,2L) contain L in its value so it stays as an integer. Through recycling, the shorter vector recycles the longer vector so that 1 gets added to positions 1 and 3, and 2 is added to 2 and 4. The result becomes 11,22,31,42 with length 4 and no dimension.

## P04

Through indexing by position, c(3L, 1L) is depicted as index 3 and 1, which extracts the 3rd and 1st element of vector c(first = 8L, second = 5L, third = 9L), in the order the index asks for. Two elements were picked so the length is 2 and the type is integer due to the values containing L.

## P05

Negative index drops elements based on the specified indices through exclusion indexing, so -2L removes 7L and leaves 4L and 9L. With a length of 2 with no dimensions, all values are integers.

## P06

The logical OR (|) is TRUE if at least one value is TRUE so NA is TRUE due to (TRUE | NA is TRUE). 12 becomes true as well since it's over 10, so the two values out of the other four get picked. Everything is L or NA\__integer_, so the type is integer with length 2.

## P07

A factor stores integer codes underneath, and is paired with level label metadata, therefore the type is integer. Levels are
the given ones, low then high. We eventually have the length 3 based on the factor vector with no dimensions.

## P08

A list holds heteregenous data types without taking note of coercion, keeping the types separate. Therefore, the length only reads 2 elements, scores and label. The type becomes list, has a length of 3, has no dimension, and the scores stays its own vector, [3,5].

## P09

A data frame is a list of equal-length columns with rows and dimensions, so the type becomes a list and the length is the number of
columns, 2. Each column contains two values, so there are 2 rows by 2 columns, 2x2.

## P10

Matrix is stored by columns as 1 to 6, so 10 goes to the 1st, 3rd, 5th and 20 to the 2nd, 4th, 6th. Since recycling occurs, the resulting values become 11,22,13,24,15,26. Everything's an integer, with a length of 6 and a dimension of 2x3.

## P11

There's an NA and no na.rm, so the mean is just NA. 8, 10, and NA*real* are all doubles, and mean() returns a double since the output always shows a floating-point value, so the NA becomes a double as well. With NA, the length is 1 and has no dimension.

## P12

na.rm = TRUE drops the NA as it removes missing values, so the mean of 8 and 10 is 9. mean() returns a double, so it's double even though 9 is a whole number. Since 9 is the only value returned, the length is 1 and has no dimension.

## P13

Subassignment happens for this case, where a value of higher precision (2.5) is assigned to the integer vector (1:3). R widens the whole thing to double so that the new value fits. We end up with a length of 3 and no dimension.

## P14

[7,NA,12,4]
[14,0,24,8]
[14,0,15,8]

NA becomes 0 due to the ifelse() condition, then the rest get doubled, then 24 gets capped to 15 through conditional subassignments. No L is found within the values and it uses NA*real*, so the type becomes double. The length becomes 4 and there is no dimension

## P15

An array is an atomic vector with a dim attribute. 1:8 is integer, and array() just adds the 2x2x2 dim, which leads to resulting value 8. Values stay in storage order, with a length of 8 and dimension 2x2x2.

## P16

Since R uses 1-based indexing, index 0L selects nothing, so it returns an empty vector of the same type, integer.
Length is also 0 and has no dimension.
