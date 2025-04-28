# GitHub Copilot Instructions for Python Development (FastAPI, NiceGUI, Okta)

## Overview

This document provides guidelines for GitHub Copilot to generate Python code for our project, which utilizes FastAPI, NiceGUI, and Okta for authentication. The goals are to produce code that is readable, maintainable, secure, robust, and aligns with established best practices and our chosen technology stack.

**Crucial:** When dealing with FastAPI, NiceGUI, or Okta APIs, **always consult the latest documentation using "MCP Context7"** (or the designated up-to-date knowledge source) to ensure correct usage, parameters, and security patterns. Do not rely solely on potentially outdated training data.

## Core Python Principles

1.  **PEP 8 & Flake8 Compliance (Highest Priority):**
    * Strict adherence to [PEP 8](https://www.python.org/dev/peps/pep-0008/).
    * Code must pass `flake8` checks without errors/warnings.
    * Focus on naming conventions (snake_case, PascalCase), line length (~88 chars preferred), import order, and whitespace.

2.  **Object-Oriented Programming (OOP):**
    * **Strongly favor OOP** for structuring the application, especially for:
        * FastAPI route logic separation (e.g., service classes).
        * NiceGUI component composition and state management.
        * Encapsulating Okta authentication logic.
    * Use classes, encapsulation (`_` or `__`), inheritance, and polymorphism effectively.
    * Define clear interfaces and responsibilities.

3.  **Design Patterns:**
    * Apply relevant design patterns (e.g., Repository, Service Layer, Dependency Injection, Strategy for auth flows) where they enhance structure, testability, and maintainability.
    * Comment on the use of specific patterns.

4.  **Readability & Maintainability:**
    * Write clear, concise, self-explanatory code. Use meaningful names.
    * Keep functions/methods short and focused (SRP).
    * Prefer explicit over implicit.

5.  **Docstrings & Comments:**
    * **Mandatory comprehensive docstrings** (Google/NumPy style) for all public modules, classes, functions, methods. Explain purpose, args, returns, exceptions.
    * Use inline comments (`#`) only for non-obvious logic.

6.  **Type Hinting:**
    * **Mandatory:** Use Python type hints ([PEP 484](https://www.python.org/dev/peps/pep-0484/)) for all function signatures and key variables. Leverage Pydantic models extensively in FastAPI.

7.  **Error Handling:**
    * Implement robust error handling (`try...except`). Catch specific exceptions.
    * Use FastAPI's exception handling mechanisms (`HTTPException`) for API errors.
    * Provide user-friendly error feedback in the NiceGUI frontend.

8.  **Asynchronous Code (FastAPI):**
    * Use `async` and `await` correctly for all I/O-bound operations within FastAPI routes and services to ensure non-blocking behavior.

## Framework-Specific Guidelines

### FastAPI

* **Structure:** Use FastAPI's `APIRouter` to organize endpoints. Separate business logic into service classes/functions, injected into route functions using FastAPI's dependency injection system (`Depends`).
* **Models:** Define request/response models using Pydantic for automatic data validation and serialization.
* **Dependencies:** Leverage dependency injection (`Depends`) for database connections, authentication logic, service classes, etc.
* **Async:** Ensure all route functions interacting with I/O (DB, external APIs like Okta) are `async def`.
* **Security:** Implement security dependencies for protected routes, integrating with the Okta authentication logic. **Consult "MCP Context7"** for current FastAPI security best practices.
* **Testing:** Generate code that is testable using FastAPI's `TestClient`.

### NiceGUI

* **Structure:** Use classes to structure UI components and manage related state. Separate UI building code from event handling logic.
* **Binding:** Utilize NiceGUI's binding (`bind_value`, `bind_visibility`, etc.) for reactive UI updates based on application state.
* **Event Handling:** Define clear event handlers (`on_click`, `on_change`). Use methods within UI classes. Avoid complex lambdas.
* **State Management:** Manage state within component classes or use a dedicated state management approach for complex applications. State changes should trigger UI updates, often interacting with the FastAPI backend.
* **Integration:** UI elements should trigger calls to the FastAPI backend (using libraries like `httpx`) for data fetching or actions requiring authentication. Handle responses and errors gracefully in the UI. **Consult "MCP Context7"** for current NiceGUI API details.

### Okta Authentication (Authorization Code Flow)

* **Library:** Use a standard, well-maintained library for Okta integration (e.g., `Authlib`, `python-jose`, or Okta's official SDK if suitable). **Verify library choice and usage via "MCP Context7".**
* **Flow Implementation:**
    * Implement the Authorization Code Flow correctly: Redirect to Okta, handle the callback, exchange code for tokens, validate tokens (ID token especially).
    * Store tokens securely (e.g., secure server-side session, **avoiding** client-side storage like localStorage for sensitive tokens).
    * Implement token refresh mechanisms.
* **Configuration:** Load Okta configuration (Client ID, Client Secret, Issuer URL, Scopes) securely from environment variables or a configuration management system (e.g., using Pydantic's `BaseSettings`). **Never hardcode credentials.**
* **FastAPI Integration:** Create FastAPI dependencies (`Depends`) to verify authentication status (e.g., check for valid session/token) and extract user information for protected routes.
* **NiceGUI Integration:**
    * Provide login/logout buttons in the UI.
    * Login button should initiate the Okta flow (redirecting via a FastAPI endpoint).
    * UI should react to authentication state changes (e.g., show user info, enable/disable elements).
    * Logout should clear the session/tokens securely on the backend and potentially redirect.
* **Security:** Pay close attention to CSRF protection, secure handling of secrets, token validation (issuer, audience, signature, expiry), and secure redirects. **Consult "MCP Context7"** for the latest Okta security recommendations and API usage for the chosen flow.

## Specific Instructions Summary

* **Prioritize:** PEP 8/Flake8, OOP, Readability, Type Hints, Docstrings.
* **Consult:** **"MCP Context7"** for up-to-date API documentation and security best practices for FastAPI, NiceGUI, and Okta.
* **FastAPI:** Use Pydantic, `async`/`await`, Dependency Injection, `APIRouter`.
* **NiceGUI:** Use classes, binding, clear event handlers, integrate with FastAPI backend.
* **Okta:** Implement Authorization Code Flow securely, manage tokens server-side, integrate with FastAPI dependencies and NiceGUI UI actions. Load configuration securely. Validate tokens thoroughly.

By following these guidelines, you will assist in creating a high-quality, secure, and maintainable application using our chosen technology stack.