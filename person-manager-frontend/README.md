# Person Manager Frontend

This is the frontend application for the Person Manager, built with Svelte and Vite, styled with Tailwind CSS.

## Prerequisites

- Node.js (version 14 or higher)
- npm or yarn

## Installation

1. Clone the repository:
   ```
   git clone <repository-url>
   cd person-manager-frontend
   ```

2. Install dependencies:
   ```
   npm install
   ```

## Running the Application

### Development Mode
```
npm run dev
```
This will start the development server with hot module replacement (HMR).

The application will be available at `http://localhost:5173` by default.

### Build for Production
```
npm run build
```
This will create an optimized production build in the `dist` directory.

### Preview Production Build
```
npm run preview
```
This will serve the production build locally for testing.

## Project Structure

- `src/App.svelte` - Main application component
- `src/main.js` - Application entry point
- `src/app.css` - Global styles with Tailwind CSS
- `public/` - Static assets
- `vite.config.js` - Vite configuration
- `tailwind.config.js` - Tailwind CSS configuration
- `svelte.config.js` - Svelte configuration

## Technologies Used

- Svelte - Reactive component framework
- Vite - Build tool and development server
- Tailwind CSS - Utility-first CSS framework
- PostCSS - CSS processing tool
- Autoprefixer - CSS vendor prefixing

## Connecting to Backend

Make sure the backend API is running (see backend README) and update any API endpoints in the frontend code to point to the correct backend URL.
