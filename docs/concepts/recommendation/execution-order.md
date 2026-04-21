# Execution Order

If Execution Order is enabled, the Rules will be evaluated one by one in ascending order when data is received from the [Data Stream](../data-stream/index.md). If the data doesn't match the Rule Logic, it will move on to the next Rule and evaluate again. If the data does match the Rule Logic, it will create a [Recommendation Alert](recommendation-alert.md) and stop evaluating against any subsequent Rules.

## Example

In the following Recommendation, there are three Rules. In each Rule, there is Rule Logic that evaluates whether the Average field from the received data is greater than 50, 70, and 90.

In the case that the Recommendation receives a data row in which the Average value is 86, it will:

1. Evaluate the data against the first rule: Exceeded 90°C. \
   86 is not greater than 90, so it will evaluate as false and move on.
2. Evaluate the data against the second rule: Exceeded 70°C.\
   86 is greater than 70, so it will evaluate as true.
3. Create a Recommendation Alert based on the Exceeded 70°C Rule.

![Execution Order Rules Example](../../images/execution-order-rules-example.png)
