# TEMPO - Appointment and Request Management System

A complete, functional, responsive web-based Appointment and Request Management System for schools with blue-themed design.

[GitHub repository - jrnxrnel](https://github.com/jrnxrnel/Tempo_Appointment_and_Reminder_System)

## Features

- **One Website, One Database** - All users access the same TEMPO application
- **Four User Roles**: Student, Registrar Admin, Finance Admin, Guidance Admin
- **Registrar Module**: Document request submission and management
- **Finance Module**: Payment status verification (in-person payments)
- **Guidance Module**: Appointment scheduling and management
- **In-App Notifications**: Real-time notifications inside the website
- **Role-Based Access Control**: Strict permissions on frontend and backend
- **Responsive Design**: Works on desktop, tablet, and mobile

## Tech Stack

- **Frontend**: Next.js 15 (App Router), React 18, TypeScript, Tailwind CSS
- **Backend**: Next.js API Routes
- **Database**: SQLite with Prisma ORM
- **Authentication**: JWT with HTTP-only cookies, bcryptjs for password hashing

## Color Theme

- Primary Blue: `#2563EB`
- Dark Blue: `#1E3A8A`
- Light Blue: `#DBEAFE`
- Very Light Blue: `#EFF6FF`
- Success Green: `#16A34A`
- Warning Yellow: `#EAB308`
- Error Red: `#DC2626`

## Getting Started

### Prerequisites

- Node.js 18+ and npm

### Installation

1. Navigate to the project directory:
```bash
cd tempo-app
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
```bash
cp .env.example .env
```
Edit `.env` and set a secure `JWT_SECRET`. Appointment reminders run in-app at the configured `APPOINTMENT_REMINDER_INTERVAL_MINUTES` interval and search the next `APPOINTMENT_REMINDER_WINDOW_HOURS` hours (defaults: 60 minutes and 24 hours).

4. Generate Prisma client and run migrations:
```bash
npx prisma generate
npx prisma migrate dev --name init
```

5. Seed the database with admin accounts:
```bash
npm run prisma:seed
```

6. Start the development server:
```bash
npm run dev
```

7. Open [http://localhost:3000](http://localhost:3000) in your browser

## Default Admin Accounts

After seeding:
- **Registrar Admin**: registrar@tempo.edu / Registrar123!
- **Finance Admin**: finance@tempo.edu / Finance123!
- **Guidance Admin**: guidance@tempo.edu / Guidance123!

Students can register through the web interface at `/register`.

## User Roles & Permissions

### Student
- Register and log in
- Submit document requests to Registrar
- Track request status and payment status
- Book Guidance appointments
- View and manage notifications
- Can only access their own records

### Registrar Admin
- View and manage all document requests
- Update request statuses (Submitted, Under Review, Requirements Needed, Awaiting Payment, Processing, Ready for Pickup, Released, Rejected)
- View request history
- Send notifications to students

### Finance Admin
- View payment records for Registrar document requests
- Verify in-person payments (Paid/Verified, Payment Issue, Awaiting Payment)
- Record verification date and responsible admin
- Notify students of payment updates
- **Note**: No online payment processing

### Guidance Admin
- Create and manage appointment schedules
- Approve/reject/reschedule/cancel appointments
- Mark appointments as completed or missed
- View appointment history
- Send notifications to students
- **Note**: Confidential counseling notes not exposed in lists

## Key Workflows

### Document Request Flow
1. Student submits request → Status: Submitted
2. Registrar reviews → Updates status (Under Review, Requirements Needed, etc.)
3. If payment required → Finance verifies in-person payment
4. Registrar processes and marks Ready for Pickup/Released
5. Students receive notifications at each step

### Appointment Flow
1. Guidance Admin creates available schedules
2. Student books available slot → Status: Pending
3. Guidance Admin approves/rejects/reschedules
4. Student receives notifications
5. Mark as Completed/Missed after appointment

## Security Features

- Password hashing with bcryptjs
- JWT authentication with HTTP-only cookies
- Role-based access control on all routes
- Students can only access their own records
- Admin accounts created via seed only (no public registration)
- Input validation on frontend and backend
- Environment variables for secrets

## Database Schema

Includes tables for: Users, Roles, StudentProfiles, DocumentRequests, DocumentRequestStatusHistory, PaymentRecords, PaymentStatusHistory, AppointmentSchedules, Appointments, AppointmentStatusHistory, Notifications

## Limitations & Notes

- **No Email/SMS**: All notifications are in-app only
- **No Online Payments**: Finance verifies in-person payments only
- **Appointment Reminders**: An in-app background job creates one reminder notification per upcoming pending or confirmed appointment.
- **Admin Setup**: Use the seed script to create admin accounts

## Testing

Test all functionality:
- Authentication (register, login, logout)
- Student: submit requests, book appointments, view notifications
- Registrar: manage requests, update statuses
- Finance: verify payments
- Guidance: manage schedules, handle appointments
- Permissions (role restrictions)
- Status transitions
- Notifications

## Support

For issues or questions, refer to the system documentation.
