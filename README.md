# Classroom & Seminar Hall Reservation System (UniReserve)

A modern, responsive web-based Classroom & Seminar Hall Reservation System designed for colleges and universities. The application streamlines room scheduling for students and faculty while providing administrators with a powerful approval and space management dashboard.

---

## 🚀 Key Features

1. **User Authentication & Role-Based Access Control**
   - Student and faculty registration with institutional ID numbers and departments.
   - Secure login with role-specific navigation guards (Student, Faculty, Admin).
   - Instant Demo Role Switcher for seamless testing and grading presentations.

2. **Room Discovery & Filters**
   - Search by room name or room code (e.g. `SH-101`, `Turing`).
   - Filter by space type (Seminar Hall, Classroom, Auditorium, Computer Lab, Conference Room).
   - Filter by academic building and minimum seating capacity.
   - Filter by facilities (Smart Boards, Air Conditioning, Sound Systems, Projectors).

3. **Real-Time Booking Conflict Prevention**
   - Interactive booking form with instant time-slot validation.
   - Strict algorithm: prevents overlapping reservations where `(StartA < EndB) and (EndA > StartB)`.
   - Secondary validation check on the database level and at the moment of administrator approval.

4. **Visual Room & Campus Timelines**
   - Hourly schedule view (08:00 AM – 08:00 PM) for any selected room.
   - College-wide daily occupancy schedule displaying all confirmed events.

5. **Administrator Management & Approval Workflow**
   - Review pending reservation requests with full applicant details and event context.
   - One-click Approve or Decline with mandatory constructive rejection notes.
   - Room Management CRUD: Add new rooms, update seating capacities, edit AV equipment, or toggle maintenance status.
   - Reservation analytics and 1-click CSV export.

6. **Official Printable Booking Pass**
   - Formatted printable reservation slip with institutional header, QR/Token reference, and digital verification seal.

---

## 🛠️ Technology Stack

- **Frontend:** Next.js 14 (App Router), React.js, TypeScript
- **Styling:** Tailwind CSS, Lucide React Icons
- **Backend / Database:** Supabase (PostgreSQL, Row Level Security, Triggers)
- **State & Storage:** Context API with dual-engine support (Live Supabase or Smart Local Demo Mode)
- **Deployment:** Vercel ready

---

## ⚡ Quick Start: How to Run

### 1. Prerequisites
- [Node.js](https://nodejs.org/) (v18.17.0 or later, v20+ recommended)
- npm, pnpm, or yarn

### 2. Install Dependencies
```bash
npm install
```

### 3. Start the Development Server
```bash
npm run dev
```

Open your browser and navigate to:
```
http://localhost:3000
```

---

## 👥 Instant Demo Accounts (Zero Setup Required)

The system includes pre-configured demo profiles so you can immediately explore and test all functionality without entering any API keys:

| Role | Name | Demo Email | Password | Access Capabilities |
| :--- | :--- | :--- | :--- | :--- |
| **Admin** | Dr. Sarah Jenkins | `admin@college.edu` | `DemoPass123!` | Approve/Reject requests, Add/Edit rooms, Analytics |
| **Faculty** | Prof. David Miller | `faculty@college.edu` | `DemoPass123!` | Browse & Book rooms, View schedules, Print passes |
| **Student** | Alex Rivera | `student@college.edu` | `DemoPass123!` | Student requests, Track status, My Bookings |

> **Pro Tip:** In the top navigation bar and on the login page, you can click the **Demo Role buttons** (`Admin`, `Faculty`, `Student`) to switch roles in a single click!

---

## 🗄️ Supabase PostgreSQL Setup (Optional for Live Production)

If you wish to connect your own live Supabase project:

1. Create a free project at [supabase.com](https://supabase.com).
2. Go to your **Project Settings -> API** and copy your **Project URL** and **Anon Key**.
3. Create a `.env.local` file in the project root:
   ```env
   NEXT_PUBLIC_SUPABASE_URL=https://your-project-ref.supabase.co
   NEXT_PUBLIC_SUPABASE_ANON_KEY=your-anon-public-key
   ```
4. In the Supabase Dashboard, open the **SQL Editor**:
   - Run the script located in `supabase/schema.sql` (Creates `profiles`, `rooms`, `bookings` tables, RLS policies, and conflict triggers).
   - Run the script located in `supabase/seed.sql` (Populates initial seminar halls and classrooms).
5. Restart your development server (`npm run dev`). The top bar will display a green `🟢 Supabase Connected` badge.

---

## 📂 Project Directory Structure

```text
├── src/
│   ├── app/
│   │   ├── layout.tsx                 # Root layout with Providers
│   │   ├── globals.css                # Tailwind directives & print styles
│   │   ├── page.tsx                   # Landing page with College Reservation overview
│   │   ├── login/page.tsx             # Login page with demo role quick-fill
│   │   ├── register/page.tsx          # Student/Faculty registration form
│   │   ├── dashboard/
│   │   │   ├── layout.tsx             # User layout with responsive sidebar
│   │   │   ├── page.tsx               # User dashboard & quick metrics
│   │   │   ├── rooms/page.tsx         # Room explorer with multi-attribute filters
│   │   │   ├── book/page.tsx          # Dedicated booking form with conflict check
│   │   │   ├── my-bookings/page.tsx   # User's bookings, status badges & print pass
│   │   │   ├── schedule/page.tsx      # Daily campus room occupancy schedule
│   │   │   └── profile/page.tsx       # User profile & account details
│   │   └── admin/
│   │       ├── layout.tsx             # Admin layout & permission guard
│   │       ├── page.tsx               # Admin control center & stats
│   │       ├── requests/page.tsx      # All requests table, approve/reject modal & CSV
│   │       ├── rooms/page.tsx         # Room management (CRUD)
│   │       └── reports/page.tsx       # Analytics & utilization reports
│   ├── components/
│   │   ├── layout/                    # Topbar, Sidebar, Navigation
│   │   ├── rooms/                     # RoomCard, RoomFilters, RoomScheduleModal, RoomFormModal
│   │   ├── bookings/                  # BookingForm, BookingPassModal
│   │   ├── admin/                     # StatsCard, ApprovalActionModal
│   │   └── ui/                        # Modal, Badge
│   ├── context/
│   │   ├── AuthContext.tsx            # Supabase Auth + LocalStorage demo fallback
│   │   └── ReservationContext.tsx     # Centralized booking & room state store
│   └── lib/
│       ├── types.ts                   # TypeScript interfaces
│       ├── constants.ts               # Buildings, room types, facilities, seed data
│       ├── conflictChecker.ts         # Booking time overlap prevention logic
│       ├── utils.ts                   # Date/Time formatting & CSV export helper
│       └── supabase/client.ts         # Browser Supabase client
├── supabase/
│   ├── schema.sql                     # PostgreSQL tables, RLS & triggers
│   └── seed.sql                       # Sample rooms & test data
├── .env.example
├── tailwind.config.ts
├── tsconfig.json
└── package.json
```

