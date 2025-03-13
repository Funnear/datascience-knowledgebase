# "Hypothesis testing is Proof by Contradiction. Why other mathematical proof methods are not used in Data Science?"

## Methods_of_proof:

References:
- https://en.wikipedia.org/wiki/Mathematical_proof#Methods_of_proof

## Observational errors

Alpha and Beta in Hypothesis testing are some measures of some kinds of errors.

References:
- https://en.wikipedia.org/wiki/Observational_error

This article is missing "method error", I remember it from Uni lessons, interrogated ChatGPT about it:
> The mathematical term “погрешность метода” translates to “method error” or “error of the method” in English.
> It refers to the inherent error introduced by a numerical or analytical method when approximating a solution. In numerical analysis, this often includes truncation error (from approximations) and discretization error (from numerical methods).

In essence, if we don't have the entire population to observe, we are approximating the data.

In regular sciences there is a whole discipline "Metrology" that is taking care of all these errors, their causes and defines classes of accuracy for equipment and methods. Is there an analogy of metrology in Data Science applicable to the data collection phase?

To disambiguate terminology ChatGPT has generated a multilingual synonyms table for us. As you can see from it English and Spanish is missing a special word for `погрешность / Fehler` to avoid confusing it with `ошибка / Irrtum`. For me погрешность is a small deviation from accuracy, while `ошибка` is something critically incorrect that completely shifts perspective from truth to lies. 

| German         | Russian     | English                | Spanish     |
|---------------|--------------|------------------------|-------------|
| Irrtum        | ошибка       | error/mistake          | error       |
| Fehler        | погрешность  | error                  | error       |
| Abweichung    | отклонение   | deviation              | desviación  |
| Ungenauigkeit | неточность   | inaccuracy/imprecision | imprecisión |
| Verzerrung    | искажение    | distortion             | distorsión  |
| Differenz     | разница      | difference             | diferencia  |


## Logical Fallacies and Cognitive Biases

A lot of jokes about false statistics come from logical fallacies, in my opinion. But those fallacies are also reasons for collecting wrong statistics and making false hypothesis.

References:
- These are more scientific, they lead to mistakes in conclusions from analysis:
  - https://en.wikipedia.org/wiki/List_of_fallacies
  - https://www.yourlogicalfallacyis.com
- These are more or less psychological (and normal, wide-spread, natural) - they form biases:
  - https://www.yourbias.is

