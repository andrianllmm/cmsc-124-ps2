# Vector and Scalar Evaluation

## Tracing the sample

We trace `c(Ada = 8, Grace = NA, Linus = 12, Barbara = 4)` through both cleaners. Both return `c(Ada = 16, Grace = 0, Linus = 20, Barbara = 8)`.

In `clean_scores_vector()`, Grace's `NA` becomes 0 in `out[is.na(out)] <- 0`, stays 0 after `out * 2`, and is left alone by `out[out > 20] <- 20`. The function never names position 2. In `clean_scores_scalar()`, Grace is handled on the second pass, where `is.na(out[[i]])` is `TRUE` and the doubling branch is skipped.

## Whole-vector operations

Every line of `clean_scores_vector()` acts on all four elements at once. `is.na(out)` builds a four-element logical mask, `out * 2` doubles every element, and `out > 20` builds a second mask. Each mask then drives one subassignment. Order still matters here: the `NA` mask runs before the doubling, so `NA * 2` is never computed.

## Visible evaluation order

The first place appears in the line `for(i in seq_along(out))`. In this case, the `for` loop follows a strict left-to-right execution order, where it explicitly forces the orders from the first index to `length(out)`.

We also have the line `if(is.na(out[[i]]))`, where the missing-value decision happens during a specific pass. For Grace, the loop stores 0 on the second pass, at a line where a debugger could stop. The double brackets only isolate one element and keep the names attached when writing back.

## Careless recycling

Suppose the doubling were written as `out * c(2, 1)`. On the sample, Ada and Linus get doubled while Grace and Barbara get multiplied by 1, so Barbara ends at 4 instead of 8. Four is a multiple of two, so R gives no warning and the answer is quietly wrong.

## Which to keep

The `clean_scores_vector` implementation would be the more optimal choice to keep in an R program considering that R revolves around the use of vectors in its operations. Compared to `clean_scores_scalar`, the vector implementation calls `is.na` once on the whole vector, which runs in compiled code, while the scalar version calls it once per element. For instance, the line `out[is.na(out)] <- 0` replaces every missing value through one whole-vector subassignment without using an `if`/`else` statement.

Of course, the trade-off is that the element-by-element order is hidden inside compiled code instead of being visible like in the scalar implementation. Each step, such as `is.na(out)`, `out * 2`, and `out > 20`, also allocates a temporary vector as long as the input, which might turn troublesome with bigger sets of data.
