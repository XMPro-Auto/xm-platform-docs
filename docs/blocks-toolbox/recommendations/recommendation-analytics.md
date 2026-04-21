
# Alert Analytics

Alert Analytics is an area in which the number of Alerts for an Identifier over a period of time can be compared - with an optional [alert ranking](../../concepts/recommendation/rule.md#alert-ranking) filter.

The Identifiers of an Alert is defined in the [Run Recommendation Agent](https://xmpro.gitbook.io/integrations/run-recommendation/how-to-use/configuration#entity) of the Recommendation's Data Stream. The Entity Identifier is mandatory, whereas the Asset, KPI, and Process Identifiers are optional.

The analytics section compares the currently viewed period of alerts with the previous period and displays the difference as a percentage. The statistics compared are:

1. The number of Alerts generated
2. The number of Alerts that were auto escalated
3. The number of Alerts marked as false positive
4. The number of Alerts resolved.

Below the breakdown, there is a stacked bar chart of the number of Alerts for the Identifier over time.

Below that is a horizontal bar of the number of Alerts for the Identifier in the selected period, separated by Rule.

![Alert Analytics](../../images/blocks-toolbox-recommendations-alert-analytics.png)
_Fig 1: The recommendation analytics for Entity ID 1 over the last 30 days and for all alert rankings._

## Alert Analytics Properties

### Behavior

#### Type

The identifier options are Asset, Process, KPI, and Entity.

#### ID

The Identifier used to filter and show analytics on all Recommendation Alerts.
