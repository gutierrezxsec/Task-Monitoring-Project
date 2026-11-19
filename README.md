# RD Task Monitoring System

A task monitoring system built for to monitor employees task. The admin assigns tasks through a web app, employees receive them by email and update their progress in a shared Google Sheet, and the admin tracks everything on a dashboard.
---

## The problem

Before this system, the admin assigned tasks to employees by email. Once a task was sent, there was no way to see whether it was started or finished. That made it hard to follow up and caused mistakes with office work and documents.

## The solution

The system keeps one central record of every task:

- The **admin** adds tasks and monitors progress from a web dashboard.
- The **employee** receives the task by email and updates its status in their department's sheet.
- The **dashboard** reflects those updates, so the admin can see what is pending, ongoing, or done without chasing anyone.

---

## How the three parts work together

| Part | Who uses it | What it does |
|---|---|---|
| **Web app** | Admin only | Log in, add tasks, and view the dashboard |
| **Email** | Employees | Receive the task details and a link to their section sheet |
| **Google Sheets** | Employees (and the system) | Stores all tasks and lets employees update their status |

<img width="500" alt="RDTMS-process-flow" src="https://github.com/user-attachments/assets/ae810cab-7cd3-4709-9b1c-1f1e8b61557a" />


## Step-by-step walkthrough

### 1. The admin signs in

Only the admin uses the website. The login page is limited to authorized personnel, and the session has a countdown timer shown on the dashboard.

<img width="1000" alt="Login Page" src="https://github.com/user-attachments/assets/017c9dfa-241a-4760-aad6-59ecc9832ea6" />

### 2. The admin adds a task

From the dashboard, the admin clicks **Add Task** and fills in the details:

- **Task Description**, **Priority**, and **Deadline**
- **Date Assigned** and **Section** (the department receiving the task)
- **Send email notification**, with the recipient and an auto-filled subject
- An optional **file attachment** (up to 5 MB), which is uploaded to Google Drive with the link included in the email

The Task ID and Date Issued are generated automatically.

<img width="1000" alt="Add task" src="https://github.com/user-attachments/assets/940979e1-1336-4fc8-94a1-d09c79c874f3" />

### 3. The task is saved to the Google Sheet

When the task is submitted, it is written to the **MASTER** sheet, which is the central record, and to the matching **section sheet**. The workbook has one tab per department (for example MIS, CSF, Planning, Admin, HR, and others) plus an ARCHIVE tab for older tasks.

<img width="1000" alt="Task added" src="https://github.com/user-attachments/assets/8abf33d6-384d-49a7-9bbd-df14d5068559" />

### 4. The employee receives an email

The assigned employee gets an email with the task ID, description, section, priority, deadline, and date assigned. It includes an **Open Section Sheet** link and tells them to log their progress there. If a file was attached, it comes with the email.

<img width="1000" alt="Tasked arrived in email" src="https://github.com/user-attachments/assets/d3a00c41-fe6d-44cd-9769-b91884585375" />

### 5. The task appears on the admin's dashboard

The dashboard shows summary cards for **Total**, **Pending**, **On-going**, and **Done** tasks, with a task list below. The admin can filter by status or section, search tasks, refresh the data, and open the **Performance** view. A newly added task starts as **Pending**.

<img width="1000" alt="dashboard added task" src="https://github.com/user-attachments/assets/7f84f774-b809-4e6e-902c-2727e13ec600" />

### 6. The employee opens their section sheet

Each department has its own task sheet that shows only that section's tasks. Employees can edit three things only: **Status** (Pending, On-going, or Done), **Date Completed**, and **Remarks**.

<img width="1000" alt="CSF task sheet" src="https://github.com/user-attachments/assets/b4b1f0b9-12ed-414a-818c-7bd7a4531509" />

### 7. The employee marks the task as done

After finishing the work, the employee changes the status to **Done** and fills in the completion date and remarks.

<img width="1000" alt="Done the task" src="https://github.com/user-attachments/assets/6237eb89-72ba-465e-9937-f5de5d7a0bbf" />


### 8. The dashboard updates

The change is synced from the section sheet to MASTER, and the dashboard shows the task as **Done**. The Pending count goes down and the Done count goes up, so the admin can see the task is finished.
<img width="1000" alt="Dashboard update done" src="https://github.com/user-attachments/assets/c15908f5-f932-41ea-922c-53a7975b5824" />

---

## Why the Google Sheet is the central control

All employees share one workbook, and the MASTER sheet is the single source of truth. Employees only work in their own section tab, and the system keeps MASTER and the dashboard in sync, using real-time updates when a section sheet is edited plus a scheduled check every 5 minutes as a backup.

## Built with

- Google Apps Script (backend and web app)
- Google Sheets (database)
- HTML, CSS, and JavaScript (dashboard interface)
- Gmail through Apps Script (email notifications)
- Google Drive (file attachments)

## Status and future improvements

The system is a working first version, and it is open to improvement. 

### Planned improvements and Recommendation

- Faster loading when there are hundreds of tasks (filtering and lighter data loading)
- More reliable syncing between section sheets and the MASTER sheet
- Safer, faster deleting when several tasks are removed quickly
- Archive filtering by month and year
- Cleanup of old file attachments in Google Drive
- A cleaner, easier-to-read dashboard layout

### Possible tech stack upgrade

Google Sheets and Apps Script let employees work in a tool they already use, which made this a practical starting point. As the number of tasks grows, a future version could store task data in a proper database with a backend API, while keeping a simple sheet or form for employees. That would improve speed, searching, and handling large amounts of data.
