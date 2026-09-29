# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands
All commands must be run from the `server` directory.

- Development: `cd server && npm run dev`
- Start Server: `cd server && npm start`
- Run All Tests: `cd server && npm test`
- Run Detailed Grading Tests: `cd server && npm run grade`
- Run Single Test: `cd server && npx jest tests/<filename>.test.js`

## Architecture
The project is a Movie Rating API built with Express and MongoDB.

- **Entry Point**: `server/src/index.js` and `server/src/app.js` (bootstrap and middleware configuration).
- **Database**: MongoDB connection handled in `server/src/config/db.js`.
- **Models**: Mongoose schemas in `server/src/models/` (e.g., `User.js`, `Rating.js`).
- **Controllers**: Business logic in `server/src/controllers/` following the pattern: `validation (Joi) -> DB call -> JSON response`.
- **Routes**: API endpoint definitions in `server/src/routes/` which delegate requests to the controllers.

## Key Implementation Patterns
- **Validation**: Uses `Joi` for request body validation in controllers.
- **Error Handling**: Unexpected errors are passed to the next middleware using `next(err)`.
- **Response Format**: Consistently returns objects (e.g., `{ ratings: [...] }`, `{ rating: <doc> }`).
- **Routing Order**: Specific routes (like `/summary`) must be defined before parameterized routes (like `/:id`) to avoid collision.
