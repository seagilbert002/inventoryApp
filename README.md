# Mobile Inventory Management App

This repository contains the complete Android application code developed as part of a Mobile Architecture & Programming course. This project demonstrates the design and implementation of a functional mobile app, applying development best practices and user-centered design principles.

## Project Overview

The mobile application was developed with the primary goal of providing users with a simple yet effective tool for managing personal or small business inventory. This app addresses the core user need for **easy and efficient inventory tracking**, enabling users to seamlessly add, update, and remove items from a digital inventory list. This ensures accurate, real-time counts of their assets. Additionally, it provides **user authentication** to secure individual inventory data and offers an **optional notification system** for critical inventory levels, such as when stock runs low or reaches zero.

**Note:** The authentication is a mockup only and is non-functional at the moment.

## UI Design and User-Centered Approach

To support these user needs and create a user-centered UI, the app features several essential screens, each designed with usability in mind:

1.  **Login Screen (`activity_main.xml`):** This is the app's entry point, offering clear fields for email and password, alongside prominent "Login" and "New User" buttons. The intuitive layout prioritizes ease of access, guiding both existing and new users seamlessly into the application.
2.  **Registration Screen (`activity_register.xml`):** Designed for simplicity and clarity, this screen allows new users to create accounts with clearly labeled fields for email, password, and password confirmation. The focus here is on a straightforward and secure signup process.
3.  **Inventory List Screen (`activity_inventory.xml`):** Serving as the central hub, this screen efficiently displays all inventory items within a `RecyclerView`. Each item is presented in a visually distinct card (`inv_list_row.xml`), making the list easy to scan and interact with. A Floating Action Button (FAB) provides an intuitive and accessible way to add new items. Additionally, an "SMS Permission" button (located at the bottom of the main screen) allows users to manage permissions for receiving low inventory alerts via SMS. The overall layout prioritizes the inventory list, making it easily scrollable and placing key actions within convenient reach.
4.  **Add Item Screen (`activity_add_item.xml`):** This screen features clear input fields for "Item Name" and "Item Quantity," enhanced with greyed-out placeholder hints that guide user input without being intrusive. A prominent "Add" button facilitates the submission of new inventory entries.
5.  **Edit/Delete Item Screen (`activity_edit_delete.xml`):** This screen is thoughtfully accessible via a long-press gesture on any inventory item, preventing accidental modifications on the main list. It allows users to modify an item's details (name, quantity) or permanently delete it.
6.  **SMS Permission Screen (`activity_sms_permission.xml`):** This dedicated screen transparently explains the purpose of SMS notifications, explicitly asks for necessary permissions, and provides immediate visual feedback on the permission status. This user-centered approach respects user privacy by making permission requests clear, optional, and easy to manage.

The UI designs are successful because they offer clear calls to action and structure information in a way that is highly consumable and interactive. The logical separation of functionalities across distinct activities (`Login`, `Inventory`, `Add`, `Edit/Delete`, `Permissions`) contributes significantly to an intuitive navigation flow and enhanced user experience.

## Coding Approach and Strategies

My approach to coding this app involved building modular components and robustly linking them to create a cohesive and functional application.

* **Database Abstraction (`DatabaseHelper.java`):** All SQLite database operations (Create, Read, Update, Delete - CRUD - for both user accounts and inventory items) were meticulously encapsulated within a dedicated `DatabaseHelper` class. This crucial abstraction centralizes database logic, making data persistence easier to manage and debug, and ensuring that any future changes to the database schema or underlying storage mechanism are localized to a single class. This technique is fundamental for any app requiring reliable local data persistence.
* **Activity-Specific Responsibilities:** Each `Activity` within the application was designed with a clear, singular responsibility, focusing solely on the UI interactions and logical operations pertaining to its specific screen. This adherence to the Single Responsibility Principle keeps classes concise, highly focused, and significantly improves code maintainability.
* **RecyclerView and Adapter Pattern:** For the dynamic display of the inventory list, `RecyclerView` was employed in conjunction with a custom `InventoryAdapter` and `InventoryItem` data model. This powerful pattern efficiently handles potentially large datasets by recycling views, which dramatically optimizes performance and ensures a smooth scrolling experience. It's an indispensable technique for modern Android list-based UIs.
* **Runtime Permission Handling:** SMS permissions, being sensitive, were handled explicitly through Android's `ActivityCompat.requestPermissions` and `onRequestPermissionsResult` methods. This demonstrates proper implementation of runtime permission requests, crucial for modern Android versions, ensuring user consent and allowing the app to gracefully degrade functionality if permissions are denied.
* **Code Quality and Readability:** Throughout the codebase, extensive in-line comments were used to clarify complex logic and non-obvious functionalities. Coupled with descriptive naming conventions (e.g., `emailEditText`, `loginButton`, `COL_USER_EMAIL`), these practices significantly enhance code readability, making the codebase easier for other developers (or my future self) to understand and maintain.

These strategies collectively promote a clean architecture, streamline the debugging process, and ensure the application is scalable and adaptable for future feature additions or modifications.

## Testing and Validation

To be honest I wish there had been an opportunity for more rigorous testing. In the future I will adopt a test first strategy that I unfortunately lacked in the particular project. Ultimately, my testing strategy was one of UAT only where I moved through the app inputing nonsense and correct responses to see what would happen.

## Innovation and Challenges

One particular area where I had to innovate to overcome a significant challenge was the **seamless integration of the local SQLite database operations with the dynamic UI updates of the RecyclerView and the reactive SMS notification trigger.** The complexity arose from ensuring data consistency across these components while maintaining a smooth user experience.

The innovation involved:
* Careful and efficient management of `Cursor` objects retrieved from the `DatabaseHelper` to dynamically populate and refresh the `RecyclerView` adapter, ensuring the UI always reflected the current database state.
* Implementing the `notifyDataSetChanged()` method in the `onResume()` lifecycle method of `InventoryActivity`. This strategic placement ensures that the inventory list is always refreshed and displays the most up-to-date database information immediately after the user adds, edits, or deletes an item in a separate activity.
* Designing the `SMSPermissionActivity` to not only manage the permission request but also to immediately initiate a check for zero-quantity inventory items upon successful permission grant. This created a direct and responsive notification system that actively reacts to changes in the app's internal inventory state, requiring careful coordination between activity lifecycles and database queries.

## Component of Success

I was particularly successful in demonstrating my knowledge, skills, and experience in the **comprehensive implementation of the SQLite database and its sophisticated integration with the RecyclerView component.**
