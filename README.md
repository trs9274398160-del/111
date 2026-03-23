The system consists of multiple interconnected modules (Overview, Categories, Spend Matrix, Financial Metrics, Upload, and Data Engine). Currently, there are critical functional, data, and UX issues that must be resolved, along with enhancements to make the system fully automated, accurate, and professionally usable for decision-making.

1. OVERVIEW PAGE (CORE DASHBOARD RESTRUCTURE)
Current Issues:
Page is too cluttered, lengthy, and visually gimmicky
Important insights are not easily readable
Navigation is not intuitive
Required Fixes & Enhancements:
1.1 Property Visibility
Remove dependency on “View All Properties”
Display all property names upfront in a clean horizontal or grid layout
Each property should act as a clickable drill-down trigger
1.2 Drill-Down Structure (VERY IMPORTANT)

Implement a 3-level hierarchy:

LEVEL 1 → Group Overview (Total Spend)
LEVEL 2 → Property Level (on click)
LEVEL 3 → Category Breakdown (17 categories per property)
LEVEL 4 → Top Items (Top 20 items per category)

👉 Data should remain hidden by default and expand only on click
👉 This ensures clean UI + deep analytics

1.3 Remove Unnecessary Visuals

Delete:

❌ Top 10 Items by Value
❌ Food vs Non-Food Split

Reason: These are adding noise, not decision value

1.4 Financial Metrics Placement
Metrics must appear below the overview section (not side-by-side)
Must include:
Operating Cost per Property
Food Cost %
Cost per Dish
1.5 Design Guidelines
White background (clean UI)
Minimal colors (use highlight colors only for insights)
No over-animation
Focus on clarity > decoration
2. FINANCIAL METRICS (CRITICAL LOGIC FIX)
Current Issues:
System uses group-level food cost incorrectly
Sales input field is broken (only 1 digit allowed)
2.1 Correct Financial Logic
❌ Current (WRONG):
Operating Cost = Group Food Cost / Property Sales
✅ Correct:
Operating Cost (Property A) = Property A Procurement Cost / Property A Sales
2.2 Mandatory Rules
Each property must be 100% isolated in calculation
No shared/global variables in formulas
2.3 Sales Input Fix
Fix input field:
Must accept full numeric values (e.g., 1250000)
Remove input restriction bug
Allow paste + typing
2.4 Validation Layer

Add:

If Sales = 0 → Show warning (avoid divide error)
If data missing → Show “Incomplete Data”
3. UPLOAD MODULE (MAJOR FAILURE AREA)
Current Issues:

Error:

Cannot read properties of undefined (reading 'toLocaleString')
Only total amount is fetched
Missing:
Item details
Category mapping
Spend matrix
Property name
3.1 Root Problem
Improper parsing logic
Undefined/null values not handled
3.2 Required Fixes
A. Data Extraction Must Capture:
Property Name (from top/header of Excel)
Item Name
Category
Quantity
Rate
Amount
B. Data Mapping Logic

Convert raw Excel → structured JSON:

{
  property: "Treat Hotel Nashik",
  category: "Dairy",
  item: "Butter",
  qty: 50,
  rate: 450,
  amount: 22500
}
C. Fix Error (toLocaleString)

Before applying:

value.toLocaleString()

👉 Add check:

if (value !== undefined && value !== null)
D. Upload Behavior
Fully automatic parsing
No manual mapping required
Must support multiple property uploads
E. Validation
If file structure incorrect → show clear error
If missing columns → highlight issue
4. SPEND MATRIX (DATA VISIBILITY ISSUE)
Current Issues:
Data incomplete
Values not readable
Fixes:
4.1 Format Conversion

Convert:

1250000 → 12.5 L
12500000 → 1.25 Cr
4.2 Data Accuracy

Ensure:

Category totals match item totals
Property totals match category totals
4.3 UI Fix
Bigger fonts
Better spacing
Clear headers
5. CATEGORIES PAGE
Fix:
Remove:
❌ “Category by Property” section

👉 Reason:

Redundant
Confusing
6. DATA ENGINE (BACKEND LOGIC – VERY IMPORTANT)
6.1 Full Data Flow
Excel Upload → Parse → Clean Data → Map Categories →
Store Structured Data → Generate Dashboards → Apply Calculations
6.2 Required Capabilities
✅ Auto Update System
Add new property → auto reflect everywhere
✅ Auto Calculation
No manual formula update
✅ Auto Save
No “Save As” needed
7. BRANDING
Add:
Group Logo (top left or center)
Group Name (clear, bold)

👉 Should appear on:

Overview
Reports
Dashboard
8. GLOBAL RULES
No broken inputs
No partial data loading
No incorrect aggregation
All calculations must follow financial logic
UI must be clean + professional + decision-focused
9. FINAL OBJECTIVE

Build a system that behaves like:

👉 Procurement Intelligence Dashboard + Financial Analyzer + Automated Reporting Tool
