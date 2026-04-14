# RobotMission.UI

React + TypeScript frontend for managing robot missions. The application displays missions in a table, lets users create or edit a mission, and deletes missions through a REST API.

![RobotMission.UI screenshot](./Taurob-Frontend.png)

## Overview

This project is a Create React App application that uses Redux Toolkit for state management and Bootstrap-based UI components. The main workflow is centered on mission management:

- Load missions from the backend API
- Load available robots for mission assignment
- Create a new mission
- Edit an existing mission
- Delete a mission
- Show success and error feedback with toast notifications

## Features

- TypeScript-based React application
- Redux Toolkit async thunks for mission CRUD operations
- Bootstrap and React Bootstrap UI
- Data table for mission listing with pagination
- Toast notifications for API feedback
- Environment-based API configuration via `REACT_APP_API_URL`

## Tech Stack

- React 18
- TypeScript
- Redux Toolkit
- React Redux
- React Bootstrap
- Bootstrap 5
- react-data-table-component
- react-toastify
- react-scripts 5

## Project Structure

```text
src/
	app/
		hooks.ts            # Typed Redux hooks
		store.ts            # Redux store configuration
	features/
		missions/
			Missions.tsx      # Main missions screen
			missionsSlice.ts  # Async thunks and reducer state
			*.test.tsx        # Existing test placeholders
	services/
		missionService.ts   # Mission API client
		robotService.ts     # Robot API client
	utils/
		models.ts           # Shared response and domain models
	App.tsx               # App shell
	index.tsx             # Root render, Provider, ToastContainer
```

## Prerequisites

- Node.js 18 LTS or newer
- npm 9 or newer
- A reachable backend API that exposes the mission and robot endpoints

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Create or update `.env` in the project root:

```env
REACT_APP_API_URL=http://localhost:5000
```

The current repository already contains an `.env` file. Update it if your backend is running on a different host.

### 3. Start the development server

```bash
npm start
```

The app will usually be available at `http://localhost:3000`.

## Available Scripts

### `npm start`

Runs the app in development mode.

### `npm build`

Creates an optimized production build in the `build/` directory.

### `npm test`

Runs the test runner.

Note: in a fresh checkout you must run `npm install` first. In the current workspace, `npm test` could not run because `react-scripts` was not installed yet.

### `npm eject`

Ejects the Create React App configuration. This is irreversible and usually unnecessary.

## API Integration

The frontend expects the backend base URL from `REACT_APP_API_URL` and calls endpoints under that base path.

### Mission endpoints used by the UI

- `GET /Api/Mission`
- `GET /Api/Mission/{id}`
- `POST /Api/Mission`
- `PUT /Api/Mission`
- `DELETE /Api/Mission/{id}`

### Robot endpoints used by the UI

- `GET /Api/Robot`
- `GET /Api/Robot/{id}`

The robot service also includes create, update, and delete methods, although the current UI screen focuses on mission management.

## Data Model Expectations

The mission screen expects mission responses to include robot details in the payload. A mission item is effectively treated as:

```ts
{
	id: number;
	name: string;
	description: string;
	robotId: number;
	robotResponse: {
		id: number;
		name: string;
		modelname: string;
		description: string;
	};
}
```

API responses are wrapped in a shared response envelope with fields such as:

- `data`
- `statusCode`
- `resultCode`
- `errorDetail`
- `errorDescription`
- `errors`

## State Management

Mission state is managed in `src/features/missions/missionsSlice.ts` with Redux Toolkit async thunks:

- `getMissionsList`
- `getMissionById`
- `createMission`
- `updateMission`
- `deleteMission`

The UI reads mission state through typed Redux hooks from `src/app/hooks.ts` and renders the table or form accordingly.

## UI Notes

- The application currently exposes a single primary screen: mission management.
- Mission creation and editing happen in the same form.
- Robot selection is populated dynamically from the API.
- Notifications are shown through `react-toastify`.

## Testing Status

Test files exist in the repository, but some are placeholders from the default scaffold and may require updates to reflect the current UI behavior.

## Known Limitations

- The UI is focused on missions; robot management is service-only at the moment.
- Error handling relies on the backend response contract being consistent.
- Styling is functional and minimal rather than fully customized.

## License

This project is licensed under the MIT License. See `LICENSE` for details.


