# Logistics

## Introduction to logistics metadata

Many countries have electronic logistics management information (eLMIS) systems in place, while others rely on paper-based methods and Excel sheets for logistics data management. Where eLMIS are already implemented, often they are optimized for data management at warehouses and do not extend to facility level for routine reporting. As a result, logistics data at health service delivery level are often unavailable for triangulated analysis with health services and other programmatic data. Many countries use DHIS2 for facility-level logistics reporting to increase visibility of stock data and health services data for programme managers, district health staff and other key data users. Because DHIS2 is widely used national scale for facility level reporting and subnational analysis, there is an opportunity to strengthen interoperability with upstream logistics data systems and improve the collection and use of last-mile logistics data. Typical use of DHIS2 for logistics data includes facility stock reporting (data inputs: monthly or daily stock reports) and outputs (indicators, charts and dashboards to visualize stock availability, distribution and use).

DHIS2 does not intend to replace fit-for-purpose electronic logistics management information systems. The metadata packages and design principles documented here are intended to disseminate field-based practices and common metadata standards for capturing logistics data at health facilities and other service delivery points that might not be covered by an eLMIS. These efforts aim to:

1. Facilitate analysis of health services and stock data in HMIS dashboards to improve programmatic decision making; and,
2. Improve interoperability between DHIS2 as an end-user logistics data capture solution and upstream LMIS.

## WHO HMIS-LMIS integrated analysis

To improve analysis of health services data alongside stock data, the WHO Global TB Programme, Global Malaria Programme, and Global HIV Programme convened in 2020 to provide guidance for integrated analysis of key stock and health services data for HMIS dashboards. This collaboration resulted in the development of a common logistics data framework applied across health programmes for aggregate facility reporting in DHIS2. Concepts from aggregate facility stock data reporting as part of the WHO EPI package, which has been implemented in countries since 2017, were used to inform the design of a common aggregate reporting framework for all health stock items.

Aggregate DHIS2 metadata packages for HIV, TB, Malaria and EPI programmes contain datasets for routine facility stock reporting and dashboards that enables triangulation of stock and health services data. These metadata packages provide a reference configuration in DHIS2 to support the adoption of WHO-recommended logistics indicators and their triangulation with the HMIS for analytic purposes.

The key objectives of the WHO-recommended integrated HMIS-LMIS packages for aggregate HMIS are to:

1. Promote good practices for integrated analysis and triangulation across service delivery data and key logistics data for a given health programme;
2. Establish guidance/standards for key stock/logistics data that can be a) reported from health facilities into DHIS2 in the absence of an alternative LMIS that reaches facility level ORb) imported/received from a functional electronic logistics information system.

To support integrated analysis in national DHIS2-based HMIS, aggregate metadata packages for vertical health programmes include:

1. Dashboards with visualizations and charts combining health services (HMIS) indicators and key logistics performance indicators (LMIS)

2. Indicators and predictors to generate calculated values as part of the common logistics metadata framework and core performance monitoring indicators for logistics as part of overall programme management

3. Data sets and data elements for facility reporting of logistics data for vertical health programmes, pre-configured for a set of typical stock items monitored for each health programme

## Common logistics metadata framework

### Core logistics metadata

DHIS2 logistics metadata included in the WHO metadata packages for core HMIS (aggregate) is designed to be harmonized conceptually across different health programmes. This has been accomplished by following a common logistics data framework based on consensus across WHO health programmes and logistics subject matter expert inputs.

The common logistics metadata framework has been applied as follows, with DHIS2 metadata concepts noted in the right-hand column. The same logistics metadata is configured for each health stock item, as relevant to each health programme (e.g. malaria RDTs, HIV test kits, GenXpert cartridges, etc).

| Logistics Data Concept         | Definition                                                   | DHIS2 Configuration Concept                                  |
| ------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Opening balance (calculated)   | The opening balance reflects the true number of usable stock items at the beginning of the reporting period.The opening balance of the current period is equal to the last period's physical 'Stock on hand' count. If there are no discrepancies in data reporting or stock items, the opening balance would also be equal to the previous period's 'Closing Balance (calculated)'. | Data Element is populated by a predictor. As this field is automatically calculated by DHIS2, it is not editable by the data entry user. |
| Stock received (recorded)      | Total quantity of stocks received during the reporting period. These may also be referred to as 'stock receipts'. | Data Element; entered manually by data entry user in Stock Form. |
| Stock issued (recorded)        | The quantities of stock physically distributed from the pharmacy and which are either directly dispensed to patients or issued to wards, outpatient departments or other services as part of patient service delivery. Stock issued is sometimes referred to as "consumption" or "used". | Data Element; entered manually by data entry user in Stock Form. |
| Stock discarded (recorded)     | The quantity of stock that was discarded (removed from stock) for any reason that (such as expiry or damage). These stock losses are known and recorded; they may be considered "accounted losses". These stock losses are sometimes referred to as "wastage." Stocks discarded is distinct from missing/lost stock because the numbers of these stock items discarded are recorded. The concept of 'stock discarded' can be further disaggregated as needed for programme specific analysis. For example, in the EPI package, stock discarded for certain vaccines may be disaggregated by reason such as frozen or broken. | Data Element; entered manually by data entry user in Stock Form. |
| Stock redistributed (recorded) | The quantity of stock redistributed back into the supply chain (for example, returned to district stores or donated to other health facilities) and is no longer intended for use by the patients of the reporting health facility. This refers to stock that leaves the facility but was not issued to patients or used during service delivery. Stocks "redistributed" upstream, such as to the district level, are also sometimes referred to as "returns". Stock redistributed to other health facilities are sometimes considered donated. | Data Element; entered manually by data entry user in Stock Form. |
| Stock on hand (recorded)       | Quantity of stock physically available and accounted for in the pharmacy/store/facility at the end of the reporting period. If all stock items were accounted and recorded properly, the recorded 'Stock on hand' data element should equal the calculated 'Closing balance'.  However, there may be data quality errors or unaccounted stock losses which can result in a discrepancy between the 'Stock on hand' and 'Closing Balance'. Due to these considerations, the 'Stock on hand' data element is considered more accurate and reliable than the calculated closing balance. | Data Element; entered manually by data entry user in Stock Form. |
| Closing balance (calculated)   | The closing balance is calculated automatically based on the above logistics data reported by the health facility. The formula for this indicator is (Opening balance + Stock received - Stock issued - Stock discarded - Stock redistributed). The calculated closing balance does not (and cannot) take unaccounted stock losses into consideration but allows calculating the latter. | Indicator; calculated in DHIS2 on the fly                    |
| Stockout days (recorded)       | Count of the number of days during the reporting period in which the respective stock item was out of stock at any time or for any period of the day. The number of stockout days are one of the logistics performance indicators. | Data Element; entered manually by data entry user in Stock Form. |

### Core logistics indicators

The WHO HIV, TB and Malaria programmes further recommended common logistics indicators to be included in the HMIS dashboard packages for programmatic performance monitoring. The following indicators have been configured and included in aggregate packages for each stock item included in the metadata package according to WHO guidance:

|          Indicator Name           |                    Indicator description                     |
| :-------------------------------: | :----------------------------------------------------------: |
|       Stock discrepancy (%)       | The difference between the calculated closing balance and the recorded stock on hand. The stock discrepancies are automatically calculated by subtracting the calculated closing balance from the recorded stock on hand. Discrepancies may be caused by mistakes during data entry, miscounting, pilfering or mislaying stocks. Most times the resulting value is negative (<0) →  the stock discrepancy then corresponds to losses which are unaccounted for and cannot be explained. Occasionally the stock discrepancy may assume positive values ("excess stocks", >0) - e.g. if the recorded quantity of stock issued is larger than the physically issued quantity or if received stocks were not recorded. |
|          Stock discarded          | Stock discarded (wastage that is accounted for) can be used to monitor stock losses. In the DHIS2 metadata design, the 'Stock discarded' indicator is the same as the stock discarded data element reported in the health facility stock report. It can be aggregated upwards through the hierarchy to determine total stock discarded for a district or at national level. |
| Facilities with stockout days (%) | Proportion of facilities reporting at least one stock-out day among all facilities that submitted a stock report. Numerator = count of org units for which stock out days are reported for a given stock item. Denominator = Number of facilities that reported during the reporting period. |
| Coverage time by facility (ratio) | Numerator: Opening balance + stock received Usable stock / Issued + Discarded + Redistributed = nb. of months, where usable stock = opening balance + received |
|    Stock-out days by facility     | Total number of stock-out days reported by the facility during the period of analysis for any given stock item |
All the core indicators are configured **by item** depending on the health program.

The metadata package enables programmes to monitor critical logistics performance management indicators within the HMIS. The **number of stockout days** is a key performance indicator for assessing the quality of demand planning, forecasting, stock replenishment calculations, ordering as well as the reliability and timeliness of upstream logistics services for delivering health products. All health products should be in stock at all times and any stockout needs to be addressed and resolved urgently.

**Stock losses** (or "wastage") is the second critical component for programmatic stock performance monitoring.  Stock losses are either "Stocks discarded" because they were damaged, expired or became unusable for other reasons (losses that can be accounted for) or "Stock discrepancy" which represent the unexplained or unaccounted losses for a given stock item. These two types of losses (discarded and discrepancy) are included in the core logistics indicators for each stock item and can be triangulated to understand stock performance.
