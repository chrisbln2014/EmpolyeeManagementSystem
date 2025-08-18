# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a modern Employee Management System (員工資料管理系統) designed for HR departments. It's a client-side web application built with React 18 that provides comprehensive employee data management capabilities including data entry, search, import/export, and local storage.

## Technical Architecture

### Single-File Application Structure
- **Primary File**: `index.html` - Contains the entire application as a single HTML file with embedded React components
- **Technology Stack**:
  - React 18 with Hooks (useState, useEffect)
  - Babel Standalone for JSX compilation
  - Tailwind CSS for styling
  - LocalStorage API for data persistence

### Key Components and Architecture
- **Main Component**: `EmployeeSurveyCRUD` - The root component managing all application state
- **State Management**: React Hooks-based state management with comprehensive form data structure
- **Data Persistence**: Browser LocalStorage for offline data storage
- **UI Views**: Three main views - list, create, edit (controlled by `currentView` state)

## Development Commands

Since this is a static web application, no build process is required:

### Running the Application
```bash
# Option 1: Open directly in browser
open index.html

# Option 2: Using Python local server
python -m http.server 8000

# Option 3: Using Node.js serve
npx serve .
```

### Development Workflow
1. Edit the `index.html` file directly
2. Refresh browser to see changes
3. No compilation or build step needed

## Core Features and Data Structure

### Employee Data Management
The application manages comprehensive employee data including:
- **Personal Information**: Employee ID, name, department, position, demographics
- **Family Information**: Dynamic children management with age groups
- **Language Skills**: Fixed languages (English, Chinese, Japanese) + custom languages
- **Travel Willingness**: Assignment preferences with location options
- **Career Planning**: Development goals and achievement projects
- **Contact Information**: Personal and emergency contact details
- **Privacy Consent**: GDPR compliance checkbox

### Data Storage Schema
Employee data is stored in LocalStorage with the following structure:
```javascript
{
  id: "timestamp_string",
  employeeId: "string", // Required, unique
  name: "string", // Required
  children: [{ id: number, age: "string" }],
  languageSkills: [{ id: number, language: "string", listening: "string", speaking: "string", reading: "string", writing: "string" }],
  fixedLanguageSkills: { "English": { listening: "string", speaking: "string", reading: "string", writing: "string" } },
  travelLocations: ["string"],
  customTravelLocations: [{ id: number, location: "string" }],
  privacyConsent: boolean // Required
}
```

## Key Implementation Patterns

### Dynamic Form Management
- Uses array-based state for dynamic sections (children, language skills, travel locations)
- Each dynamic item has a unique ID for efficient updates and removals
- Conditional rendering based on user selections (e.g., travel locations only shown when applicable)

### Data Validation
- Required fields: Employee ID, Name, Privacy Consent
- Duplicate Employee ID prevention
- Form validation before submission

### Import/Export Functionality
- JSON-based data export with metadata (export date, total employees)
- File import with validation and confirmation dialogs
- Backup and restore capabilities

## Department Options
The system supports the following departments:
- 總公司, 總管理處, 製造部, 儲運環安, 塗開處, 品保部
- 鋼材台中, 鋼材台北, 鋼材高雄, 混凝土處, 特工處
- 製造官田, 官田預塗, 中構官田, 柳營

## Browser Compatibility
- Chrome 80+, Firefox 75+, Safari 13+, Edge 80+
- Requires JavaScript ES6+ support
- Responsive design for desktop and mobile devices

## Common Development Tasks

### Adding New Form Fields
1. Add field to `formData` initial state
2. Add field to `resetForm` function
3. Create form input element with `handleInputChange`
4. Update validation logic if field is required

### Modifying Dynamic Sections
Dynamic sections (children, languages, travel locations) follow the pattern:
- Add functions: `add{Section}()` - creates new item with unique ID
- Remove functions: `remove{Section}(id)` - filters out item by ID
- Update functions: `update{Section}(id, field, value)` - updates specific field

### Styling Updates
- Uses Tailwind CSS utility classes
- Color-coded badges for different data types
- Responsive grid layouts with `md:` breakpoints
- Gradient backgrounds and modern shadow effects