# Procurement Master Tracker (Excel-Ready)

This package is designed as a multi-sheet Excel tracker for complex projects. Each CSV file is intended to be a separate worksheet in one workbook.

## Recommended workbook sheet order
1. `01_Suppliers_Directory.csv`
2. `02_Products_Master.csv`
3. `03_RFQ_Log.csv`
4. `04_Communication_Log.csv`
5. `05_Quotations_Comparison.csv`
6. `06_PO_Register.csv`
7. `07_Shipment_Log.csv`
8. `08_Delivery_Critical_Items.csv`
9. `09_Dashboard_KPIs.csv`

## Data model and linking keys
- **Supplier master key:** `Supplier_ID`
- **Product master key:** `Product_ID`
- **RFQ key:** `RFQ_ID`
- **Quote key:** `Quote_ID`
- **Purchase order key:** `PO_ID`
- **Shipment key:** `Shipment_ID`
- **Line level key:** `PO_Line_ID`

Use these keys consistently to link suppliers to offers, POs, shipments, and products.

## Suggested status controls
- Supplier status: `Approved`, `Conditional`, `Blocked`, `Inactive`
- RFQ status: `Draft`, `Issued`, `Partially Received`, `Closed`, `Cancelled`
- Quote status: `Received`, `Under Evaluation`, `Negotiating`, `Shortlisted`, `Rejected`, `Awarded`
- PO status: `Draft`, `Issued`, `Acknowledged`, `Partially Delivered`, `Delivered`, `Closed`, `On Hold`
- Shipment status: `Planned`, `Booked`, `In Transit`, `At Port`, `Customs Clearance`, `Delivered`, `Delayed`
- Criticality: `High`, `Medium`, `Low`
- Risk level: `High`, `Medium`, `Low`

## Practical operating routine (daily)
1. Update `04_Communication_Log` first after supplier interactions.
2. Update `03_RFQ_Log` and `05_Quotations_Comparison` when offers are received/revised.
3. Update `06_PO_Register` immediately after PO issuance or supplier acknowledgment.
4. Update `07_Shipment_Log` for ETD/ETA changes and customs milestones.
5. Review `08_Delivery_Critical_Items` in daily standup for expediting decisions.
6. Refresh `09_Dashboard_KPIs` for weekly management reporting.

## KPI formulas to use in Excel
- **On-time delivery %** = `On_Time_Deliveries / Total_Deliveries`
- **PO cycle time (days)** = `PO_Issue_Date - RFQ_Release_Date`
- **Quote turnaround (days)** = `Quote_Received_Date - RFQ_Issue_Date`
- **Critical overdue lines** = count of lines where `Criticality="High"` and `Days_To_Need_Date<0` and `Delivery_Status<>"Delivered"`
- **Spend by supplier** = sum of `Total_Line_Value_USD` grouped by `Supplier_ID`

## Notes
- Currency in this template is normalized in USD for comparability.
- Keep original commercial currencies in quotation fields where needed.
- Add conditional formatting for overdue dates and high risks.
