# Invoice Chasing Agent - MVP Specification

## Project Overview

- **Project Name:** Invoice Chasing Agent
- **Type:** Single-page web application (prototype)
- **Core Functionality:** AI agent simulation that tracks outstanding invoices, manages escalation lifecycle, and logs all actions taken
- **Target Users:** Property managers, small landlords who need an "assistant" to handle invoice follow-ups

---

## UI/UX Specification

### Layout Structure

**Page Sections:**
1. **Header** - Agent identity, status indicator, current date/time
2. **Add Invoice Panel** - Collapsible form to add new invoices
3. **Active Invoices Table** - Main workspace showing all tracked invoices
4. **Activity Log** - Right sidebar showing agent's thinking and actions
5. **Footer** - Minimal, shows storage status

**Responsive Breakpoints:**
- Desktop (≥1024px): 3-column layout (form | table | log)
- Tablet (768-1023px): 2-column (table + log below)
- Mobile (<768px): Single column stack

### Visual Design

**Color Palette:**
- Background: `#0D1117` (deep charcoal)
- Surface: `#161B22` (elevated cards)
- Border: `#30363D` (subtle dividers)
- Primary accent: `#58A6FF` (electric blue)
- Success: `#3FB950` (resolved green)
- Warning: `#D29922` (escalation amber)
- Danger: `#F85149` (overdue red)
- Text primary: `#E6EDF3`
- Text secondary: `#8B949E`

**Typography:**
- Headings: "JetBrains Mono", monospace - 600 weight
- Body: "IBM Plex Sans", sans-serif - 400 weight
- Agent log: "JetBrains Mono", monospace - 400 weight, 13px

**Spacing System:**
- Base unit: 8px
- Card padding: 24px
- Section gaps: 32px
- Element spacing: 16px

**Visual Effects:**
- Cards: 1px border with subtle glow on hover
- Status badges: Pill-shaped with glow matching status color
- Agent reasoning: Typewriter effect on new entries
- Timestamps: Relative time ("2 mins ago") with hover for exact

### Components

**Invoice Card/Row:**
- Client name (prominent)
- Amount (formatted currency)
- Due date with countdown badge
- Contact info (email/phone icons)
- Current status badge (Pending/Reminder/Final/Resolved)
- "Take Action" button - triggers agent sequence
- Expandable: shows full reasoning log

**Add Invoice Form:**
- Client name (text input)
- Email (email input)
- Phone (tel input)
- Amount (number input)
- Due date (date picker)
- Submit button with loading state

**Activity Log Entry:**
- Timestamp (exact)
- Thinking bubble (agent's reasoning)
- Action taken (what was "sent")
- Result (simulated response)

**Status Badges:**
- Pending: Blue outline
- Reminder Sent: Amber filled
- Final Notice: Red filled
- Resolved: Green filled

---

## Functionality Specification

### Core Features

1. **Add Invoice**
   - Form validation (required fields)
   - Auto-generate unique ID
   - Initial status: "Pending"
   - Save to LocalStorage

2. **Invoice Tracking State Machine**
   ```
   Pending → Reminder Sent (after due date) 
         → Escalated (7 days after reminder)
         → Final Notice (14 days after reminder)
         → Resolved (manual override or payment)
   ```

3. **Agent Action Engine**
   - "Take Action" button triggers agent sequence
   - Agent evaluates: "Is this overdue? How many days?"
   - Agent determines: which escalation level
   - Agent generates: personalized message
   - Agent logs: full reasoning + action + result

4. **Message Templates (Simulated)**
   - Reminder: "Friendly reminder about invoice..."
   - Firm: "This is a second notice regarding..."
   - Final: "Final notice - payment required within 7 days..."

5. **Activity Logging**
   - Every action logged with timestamp
   - Shows agent thinking process
   - Shows what "message" was sent
   - Simulated response generation

6. **Data Persistence**
   - All invoices in LocalStorage
   - All activity logs in LocalStorage
   - Auto-save on every change

### User Interactions

- Click "Add Invoice" → Expand form
- Fill form + Submit → Add to table + log "New invoice added"
- Click "Take Action" → Run agent logic → Update status → Log entry
- Click row → Expand to show full history
- Click "Mark Resolved" → Set status to Resolved → Log entry

### Edge Cases

- Duplicate invoice check (same client + amount)
- Past due date handling (immediate action)
- Empty state: Show "No invoices yet" with CTA

---

## Acceptance Criteria

1. ✅ Can add a new invoice with all required fields
2. ✅ Invoice appears in table immediately
3. ✅ "Take Action" button runs agent logic and updates status
4. ✅ Activity log shows agent reasoning and actions
5. ✅ Status changes reflect in badge/row
6. ✅ Data persists after page refresh
7. ✅ Responsive layout works on mobile
8. ✅ UI feels professional, not generic AI aesthetic
9. ✅ Timestamps update to relative time
10. ✅ Deployable to GitHub Pages (single HTML)
