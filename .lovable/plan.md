

# CoreInventory — Industrial Inventory Management System

## Overview
A dark-themed, industrial-aesthetic inventory management frontend with red accent borders, monospace data displays, and a "Control Room" feel. All data is local (Zustand store with dummy JSON data). No backend.

---

## Pages & Features

### 1. Global Layout
- **Collapsible sidebar** (icon-only when collapsed) with red glow active states
- Menu sections: Dashboard, Operations (Receipts, Delivery Orders, Inventory Adjustment), Products, Move History, Settings (Warehouse, Locations), Profile, Logout
- **Top header bar** with sidebar trigger, page title, and low-stock alert badge
- Dark `#090909` background, `1px` red-tinted borders

### 2. Authentication Pages
- **Login page**: Logo, Login ID, Password, Sign In button, "Forgot Password?" link, "Sign Up" link. Validates against dummy credentials, shows error toast on failure, redirects to dashboard on success
- **Signup page**: Login ID, Email, Password, Confirm Password with validation rules (uppercase, lowercase, number, min 8 chars, uniqueness check). Redirects to login on success
- Auth state managed via Zustand store (no real backend)

### 3. Dashboard
- 5 KPI cards: Total Products, Low Stock (red alert pulse), Pending Receipts, Pending Deliveries, Scheduled Transfers
- Receipt summary card ("4 to receive, 1 late, 6 operations")
- Delivery summary card ("4 to deliver, 2 waiting, 6 operations")
- Operation status breakdown: Late / Waiting / On Schedule

### 4. Product Management
- Table view with columns: Product, SKU, Category, Available Stock, Location, Actions (Edit/Delete)
- Search bar, category filter dropdown, sort by stock
- Create/Edit product dialog with fields: Product Name, SKU, Category, Unit of Measure, Initial Stock
- Delete confirmation dialog
- Low stock items highlighted in red

### 5. Receipts Page (Incoming Stock)
- List table: Reference (WH/IN/XXXX auto-increment), From, To, Contact, Scheduled Date, Status
- Create Receipt form: Reference (auto), Source vendor, Destination warehouse, Responsible, Schedule Date, Products sub-table (Product + Quantity) with "Add Product" row
- Buttons: Validate, Cancel, Print
- Status flow: Draft → Ready → Done. Validation auto-increases product stock
- Kanban view toggle option

### 6. Delivery Orders Page (Outgoing Stock)
- Same structure as Receipts but with WH/OUT/XXXX references
- Validation auto-decreases stock
- Status flow: Draft → Ready → Done
- Kanban view toggle option

### 7. Inventory Adjustment Page
- Form: Select Product, Warehouse, Location — shows System Quantity (read-only), Counted Quantity input
- Auto-calculates Adjustment (Counted - System)
- Adjustment log table below

### 8. Move History Page
- Table: Reference, Date, Contact, From, To, Quantity, Status
- Search by reference, search by contact, filter by date range, filter by product

### 9. Settings Page
- **Warehouse management**: CRUD table (Name, Short Code, Address)
- **Location management**: CRUD table (Location Name, Warehouse, Description)

### 10. Profile Page
- Display: Name, Email, Role
- Change password form
- Edit Profile and Logout buttons

---

## State Management (Zustand)
- `useAuthStore`: user session, login/logout, signup
- `useInventoryStore`: products, operations (receipts/deliveries), stock updates, adjustments, move history
- `useSettingsStore`: warehouses, locations

All stores initialized with realistic dummy data.

## UI Components
- `KPICard` — with alert variant (red pulse)
- `StatusBadge` — Draft, Waiting, Ready, Done, Cancelled
- `ProductTable`, `OperationTable`, `MoveHistoryTable`
- `OperationForm` — reusable for receipts and deliveries
- `KanbanBoard` — card columns by status
- All styled with the Core-Industrial design system: sharp corners (4px), red borders, Geist Mono for data, dark surfaces

## Design Tokens
- Background: `#090909`, Cards: `#111`, Borders: `red-900/20`
- Accent: vivid red (`#ef4444`), Text: white/zinc scale
- Font: Geist Mono for data, Geist Sans for UI
- No soft shadows, no pastels, no pill buttons

