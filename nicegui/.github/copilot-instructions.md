# GitHub Copilot Instructions for Python Development

## Overview

This document provides guidelines for GitHub Copilot (and similar AI code assistants) to ensure generated Python code aligns with our project's standards. The primary goals are to produce code that is readable, maintainable, robust, and follows established best practices, including the use of specific frameworks like NiceGUI.

## Core Principles

Please adhere to the following principles when generating Python code:

1.  **PEP 8 & Flake8 Compliance (Highest Priority):**
    * All generated code **must** strictly adhere to [PEP 8](https://www.python.org/dev/peps/pep-0008/) style guidelines.
    * Code should pass `flake8` checks without errors or warnings.
    * Pay close attention to naming conventions (snake_case for variables/functions, PascalCase for classes), line length (typically 79 or 88 characters, check project config), import ordering, and proper whitespace usage.

2.  **Object-Oriented Programming (OOP):**
    * **Favor OOP** for structuring code, especially when dealing with state management, complex logic, or entities that have both data and behavior. This is particularly relevant for structuring NiceGUI applications.
    * Utilize classes, encapsulation (private attributes via convention `_` or `__`), inheritance, and polymorphism where they enhance clarity, reusability, and maintainability.
    * Define clear interfaces and responsibilities for classes.

3.  **Design Patterns:**
    * Actively consider and apply relevant, established software design patterns (e.g., Factory, Singleton, Strategy, Observer, Decorator, Adapter) when they provide a clear benefit for solving recurring problems, improving flexibility, or enhancing structure.
    * If a specific design pattern is implemented, **add a brief comment** explaining which pattern is used and why it's appropriate in that context.

4.  **Readability & Maintainability:**
    * Write clear, concise, and self-explanatory code.
    * Use meaningful variable and function names.
    * Keep functions and methods short and focused on a single responsibility (Single Responsibility Principle - SRP).
    * Avoid overly complex or "clever" code that sacrifices readability. Simple and explicit is often better.

5.  **Docstrings & Comments:**
    * **Mandatory:** Provide comprehensive docstrings for all public modules, classes, functions, and methods. Use a standard format like Google style or NumPy style.
    * Docstrings should explain the purpose, arguments, return values, and any exceptions raised.
    * Use inline comments (`#`) sparingly to explain non-obvious logic or complex sections. Do not comment on the obvious.

6.  **Type Hinting:**
    * **Mandatory:** Use Python's type hints ([PEP 484](https://www.python.org/dev/peps/pep-0484/)) for all function signatures (arguments and return types) and complex variable assignments. This improves code clarity and enables static analysis.

7.  **Error Handling:**
    * Implement robust error handling using `try...except` blocks.
    * Catch specific exceptions rather than broad `Exception` types where possible.
    * Handle potential errors gracefully (e.g., logging, returning specific values, raising custom exceptions).

8.  **Testing:**
    * While you might not write the tests themselves, generate code that is easily testable. This often involves dependency injection, clear interfaces, and avoiding tight coupling.

## Framework-Specific Guidelines

### NiceGUI

* **Usage:** When generating web UIs or interactive applications, prefer using the `nicegui` framework.
* **Structure:**
    * Structure NiceGUI applications using classes where appropriate to encapsulate UI elements and related logic/state.
    * Separate UI definition functions/methods from the core application logic or event handlers where feasible.
    * Utilize NiceGUI's built-in elements and layout managers effectively (`ui.row`, `ui.column`, `ui.card`, etc.).
* **Event Handling:** Define event handlers (`on_click`, `on_change`, etc.) as separate methods or functions for clarity. Use lambda functions only for very simple, single-line actions.
* **State Management:** Manage UI state explicitly, often within the class structure or using dedicated state management approaches if the application becomes complex.
* **Best Practices:** Follow standard NiceGUI patterns, such as using `ui.run()` correctly and binding properties for reactivity.

## Specific Instructions Summary

* **Always prioritize PEP 8 / Flake8 compliance.**
* **Use classes and OOP principles for structure and state management, especially with NiceGUI.**
* **Apply design patterns where appropriate and comment on their use.**
* **Write clear, readable, and maintainable code.**
* **Include comprehensive docstrings and type hints.**
* **Implement specific and robust error handling.**
* **Keep functions small and focused.**
* **Follow NiceGUI best practices when generating UI code.**

By following these guidelines, you will help us maintain a high-quality, consistent, and professional codebase.
