### **Project Submission: Shiptivitas Full-Stack Kanban Board**

**Contributor:** Sherif Ibrahim
**Date:** September 9, 2025

#### **Project Overview**

This submission details the end-to-end development of a persistent, full-stack Kanban board for the Shiptivitas application. The project was completed in two major phases: first, the creation of a robust frontend with complex drag-and-drop logic, and second, the integration of this frontend with a backend API to ensure data persistence.

#### **Phase 1: Frontend Implementation and Core Logic**

The initial objective was to build a fully interactive Kanban board in React.

- **Core Challenge & Solution:** The primary technical hurdle was integrating the `dragula` library (which directly manipulates the DOM) with React's declarative, state-driven rendering. My solution established **React as the single source of truth** by using `drake.cancel(true)` within the `drop` event. This strategy prevents DOM conflicts by allowing Dragula only to report the user's action, while React exclusively handles the rendering, thus eliminating synchronization bugs.

- **Key Contributions:**
  - **State Management:** Architected the state to correctly handle three swimlanes (`backlog`, `inProgress`, `complete`) and ensured all tasks loaded into the "Backlog" by default.
  - **Unified Drop Logic:** Developed a single, robust state update function that correctly handles both reordering cards within a lane and moving cards between different lanes.
  - **Accurate Positioning:** Implemented logic to use the `sibling` element from the Dragula event to calculate the precise drop location, ensuring cards land exactly where the user places them.

#### **Phase 2: Backend Integration and State Persistence**

The second phase focused on connecting the frontend to the provided backend API, transforming the application from a static UI into a persistent, data-driven tool.

- **Refactoring for Data Flow:**

  - **Lifted State:** I refactored the application by "lifting state" from the `Board.js` component up to the main `App.js` component. This centralized all data management and API communication in `App.js`, a best practice for React applications.
  - **Presentational Components:** `Board.js` was converted into a "dumb" presentational component, receiving all its data and functions (like `onCardMove`) via props. This separation of concerns makes the codebase cleaner and easier to maintain.

- **API Communication:**
  - **Initial Data Fetch:** Implemented a `fetch` call in `App.js`'s `componentDidMount` to make a `GET` request to `/api/v1/clients`. This populates the board with live data from the database on initial load, replacing the previous hardcoded data.
  - **Saving Changes:** The `handleCardMove` function in `App.js` was created to send a `PUT` request to `/api/v1/clients/:id` whenever a card is moved. This request includes the card's new `status` and `priority`, instructing the backend to update the database.
  - **Data Synchronization:** The frontend state is updated using the complete, authoritative list of clients sent back from the server after a successful `PUT` request. This ensures the UI is always perfectly in sync with the database.

#### **Final Outcome**

The result is a fully functional, persistent, and robust Kanban board. The application now successfully fetches data from a server, and reliably saves all changes back to the database, providing a seamless and stateful user experience.
