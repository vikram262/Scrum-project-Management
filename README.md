# Zcrum: Agile Project Management Tool

![Zcrum Logo Placeholder](https://placehold.co/1200x400/2563eb/ffffff?text=Zcrum+Project+Management)

Zcrum is a comprehensive full-stack project management application designed to streamline team collaboration and workflow, offering functionalities akin to popular tools like Jira. It provides robust features for user authentication, organization and project management, sprint planning, and intuitive issue tracking via a Kanban board.

## Table of Contents

* [Overview](#overview)
* [Key Features](#key-features)
    * [Authentication and Authorization](#authentication-and-authorization)
    * [Organization Management](#organization-management)
    * [Project Management](#project-management)
    * [Sprint Management](#sprint-management)
    * [Issue Tracking (Kanban Board)](#issue-tracking-kanban-board)
* [Technical Stack](#technical-stack)
* [Database Schema](#database-schema)
* [Project Structure](#project-structure)
* [Setup and Installation](#setup-and-installation)
* [Usage](#usage)
* [Contributing](#contributing)
* [License](#license)

---

## Overview

Zcrum empowers teams with an intuitive platform to organize, track, and manage their work efficiently. Whether you follow agile methodologies or prefer traditional project management, Zcrum offers a versatile solution to boost productivity and foster seamless collaboration. Its user-friendly interface and powerful backend make it an ideal tool for teams of all sizes.

## Key Features

### Authentication and Authorization

Zcrum leverages Clerk.js to provide secure and flexible user authentication and authorization.

* **Multiple Sign-in Options**: Supports both Google and traditional email/password sign-in methods.
* **Seamless Onboarding**: Guides new users through an onboarding process to create or join an organization.
* **Protected Routes**: Ensures that only authenticated and authorized users can access specific parts of the application.
* **User & Organization Switching**: Allows users to easily switch between different organizations they belong to.

### Organization Management

Organizations serve as the primary containers for projects and teams within Zcrum.

* **Organization Creation**: Users can create new organizations during onboarding or via the organization switcher.
* **Project Listing**: View all projects associated with a specific organization.
* **User Management**: See all members within an organization.

### Project Management

Each organization can host multiple projects, each with its own set of sprints and issues.

* **Project Creation**: Administrators can easily create new projects with custom names and keys.
* **Project Deletion**: Admins have the ability to delete projects, ensuring data integrity with cascading deletes for associated sprints and issues.
* **Project Details**: Access a dedicated page for each project to view its sprints and manage issues.

### Sprint Management

Zcrum supports agile workflows by enabling the creation and management of sprints.

* **Sprint Creation**: Define new sprints with specific start and end dates. Sprint names are automatically generated for consistency.
* **Sprint Statuses**: Sprints transition through `PLANNED`, `ACTIVE`, and `COMPLETED` statuses.
* **Sprint Control**: Start and end sprints directly from the project board, with appropriate permission checks.

### Issue Tracking (Kanban Board)

The core of Zcrum's project management lies in its intuitive Kanban board for issue tracking.

* **Issue Creation**: Easily create new issues with titles, descriptions, assignees, and priorities.
* **Drag-and-Drop Functionality**: Visually move issues between different status columns (`TODO`, `IN_PROGRESS`, `IN_REVIEW`, `DONE`) on the Kanban board.
* **Issue Details**: Click on any issue to view and edit its details, including status and priority.
* **Filtering Options**: Filter issues by title, assignee, and priority to quickly find what you need.
* **User-Specific Issues**: View all issues assigned to or reported by the current user across their organizations.

## Technical Stack

Zcrum is built with a modern, robust, and scalable technology stack:

**Frontend:**
* **Next.js 14**: React framework for full-stack development.
* **React 18**: Core JavaScript library for UI.
* **Shadcn UI**: Reusable, accessible UI components built with Tailwind CSS.
* **Tailwind CSS 3.x**: Utility-first CSS framework for rapid styling.
* **`react-hook-form`** with **`zod`**: For form validation and management.
* **`@uiw/react-md-editor`**: Markdown editor for rich text descriptions.
* **`@hello-pangea/dnd`**: Powerful library for drag-and-drop interactions on the Kanban board.
* **`sonner`**: For elegant toast notifications.
* **`lucide-react`**: For a wide range of customizable icons.

**Backend & Database:**
* **Clerk.js**: Comprehensive user authentication and organization management.
* **Prisma ORM 5.x**: Next-generation ORM for seamless database interactions.
* **PostgreSQL**: Robust relational database for data storage.
* **Next.js Server Actions**: For efficient server-side logic and API handling.

**Development Tools:**
* **ESLint**: For maintaining code quality and consistency.

## Database Schema

The application's data is structured around the following key models, managed by Prisma:

* **`User`**: Stores user profiles, linked to Clerk.js.
    * `id`, `clerkUserId`, `email`, `name`, `imageUrl`, `createdAt`, `updatedAt`
* **`Organization`**: Represents a team or company.
    * `id`, `name`, `slug`, `imageUrl`, `createdAt`, `updatedAt`
* **`Project`**: Projects within an organization.
    * `id`, `name`, `key`, `description`, `organizationId`, `createdAt`, `updatedAt`
* **`Sprint`**: Time-boxed periods for work within a project.
    * `id`, `name`, `startDate`, `endDate`, `status` (`PLANNED`, `ACTIVE`, `COMPLETED`), `projectId`, `createdAt`, `updatedAt`
* **`Issue`**: Individual tasks or bugs.
    * `id`, `title`, `description`, `status` (`TODO`, `IN_PROGRESS`, `IN_REVIEW`, `DONE`), `order`, `priority` (`LOW`, `MEDIUM`, `HIGH`, `URGENT`), `assigneeId`, `reporterId`, `projectId`, `sprintId`, `createdAt`, `updatedAt`

Relationships are defined to ensure data integrity, including one-to-many relationships between `Organization` and `Project`, `Project` and `Sprint`, `Sprint` and `Issue`, and `User` with `Issue` (assignee/reporter). Cascading deletes are implemented for related data (e.g., deleting a project deletes its sprints and issues).

Once the application is running:

1.  **Access the Application**: Open your web browser and navigate to `http://localhost:3000`.

2.  **Sign Up / Sign In**: Create a new account or log in using your existing credentials or Google.

3.  **Onboarding**: If you're a new user, you'll be guided through creating your first organization or joining an existing one.

4.  **Organization Dashboard**: View your organization's projects and your assigned/reported issues.

5.  **Create a Project**: As an organization administrator, you can create new projects from the organization dashboard.

6.  **Manage Sprints**: Within a project, create new sprints and manage their statuses.

7.  **Track Issues**: Add new issues to sprints and update their status by dragging them across the Kanban board.

8.  **Filter Issues**: Use the available filters to quickly find specific issues.

