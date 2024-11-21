# Project Roadmap and Code Overview
## Introduction
**This document outlines the roadmap and architecture for a web application designed to manage categories, subcategories, and "duas" (prayers). It highlights the backend and frontend functionalities, key components, and data flow.**
## Project Live [Link](https://duah-ruqyah.vercel.app/)
### Backend
##### Server Setup (server.js)
- Framework: Express.js is used to create a REST API.
- Database: SQLite is used via better-sqlite3 for efficient query handling.
- Middleware:
- cors: Enables cross-origin requests.
- Endpoints:
/categories: Fetches categories, subcategories, and duas by querying the SQLite database.
- Error Handling: Captures errors and responds with a status code of 500.
#### Data Management (data.js)
- Functionality: getCategoriesWithDetails retrieves and structures category, subcategory, and dua data from the database.
- SQL Query:
Joins category, sub_category, and dua tables.
    - Handles relationships:
    - Categories can have subcategories.
    - Subcategories and categories can both have duas.
    - Orders data by cat_id, subcat_id, and dua_id.
- Data Transformation:
    - Constructs a nested object structure to group subcategories under categories and duas under subcategories or directly under categories.
Avoids duplicate entries.
#### TypeScript Definitions (definitions.ts)
- Defines interfaces for:
- Category: Represents a category and its metadata.
- SubCategory: Represents a subcategory, linked to a category.
- Dua: Represents a prayer with translations, references, and audio.
### Frontend
#### Page Layout (page.tsx)
- Structure:
    - Uses flexbox to create a responsive layout with a Sidebar, MainContext, and RightSidebar.
#### Main Context (MainContext.tsx)
- Purpose:
    - Fetches categories from the backend using fetchCategories.
Renders the Header and MainCard components.
- Data Flow:
    - Fetches category data at runtime and passes it to MainCard.
#### MainCard Component (MainCard.tsx)
- State Management:
    - Manages:
        - Currently expanded category.
        - Selected category and subcategory.
        - Displayed duas.
- User Interactions:
    - Clicking a category expands its subcategories and displays its duas.
    - Clicking a subcategory filters and displays its associated duas.
- Helper Functions:
    - getAllCategoryDuas: Gathers all duas for a category, including those in its subcategories.
#### Category Sidebar (CategorySidebar.tsx)
- Purpose:
    - Lists categories and subcategories.
    - Allows users to expand categories and view associated subcategories.
- Search Functionality:
    - Input field to filter categories (to be implemented).
- UI Highlights:
    - Selected category and subcategory are visually highlighted.
    - Uses icons for category representation.
## Data Flow
### Backend:

Server listens on port 3001.
Endpoint /categories queries SQLite database.
Returns a nested JSON structure of categories, subcategories, and duas.
Frontend:

Fetches data via fetchCategories.
Passes the data through MainContext to MainCard.
Renders interactive components (CategorySidebar, ContentList) for user navigation.
Roadmap
>Milestone: Core Features
Complete current functionalities:
Fetching categories, subcategories, and duas.
Displaying data interactively in the frontend.
