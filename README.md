 day5-technical- Day 5 Assignment — Technical Writing

 Exercise A: User Manual Procedure

Creating and Activating a Python Virtual Environment and Installing a Package (Linux)

 Prerequisites

Before starting, you will need:
- A Linux terminal (this includes ChromeOS built-in Linux/Crostini environment)
- Python 3 installed (version 3.3 or later, since the `venv` module is built in)
- An internet connection (to install a package from PyPI)

Steps

1. Open the terminal.
   Open your Linux terminal application.
   Expected result: A terminal window appears with a command prompt ready for input.

2. Navigate to your project folder.
   Type `cd path/to/your/folder` and press Enter.
   *Expected result:* The prompt updates to show you are now inside that folder.

3. Create the virtual environment.
   Type `python3 -m venv env` and press Enter.
   Expected result: No error is shown, and a new folder named `env` appears inside your project folder.

4. Activate the virtual environment.
   Type `source env/bin/activate` and press Enter.
   Expected result:* The terminal prompt changes to show `(env)` at the beginning of the line, indicating the environment is now active.

5. Confirm the environment is active.
   Type `pip list` and press Enter.
   Expected result: A short list of only the default packages (like `pip` and `setuptools`) is shown, confirming this is a clean, isolated environment.

6. Install a package.
   Type `pip install requests` and press Enter.
   Expected result: Terminal output shows "Collecting requests," followed by download progress, then "Successfully installed requests-x.x.x."

7. Verify the installation.
   Type `pip show requests` and press Enter.
   Expected result: Details about the installed package (name, version, location) are displayed.

 Screenshot Description

A screenshot after Step 4 would be useful: it should show the terminal window with the prompt clearly displaying `(env)` at the start of the line, proving the virtual environment is active before any packages are installed.

Troubleshooting Note

The most common error beginners hit is typing `python` instead of `python3`, resulting in a "command not found" error, since many Linux systems only recognize `python3` by default. If this happens, try `python3` inste

 Exercise B: API Reference Entry
`POST /api/v1/projects/{project_id}/tasks`

Creates a new task within the specified project. The request must be made by an authenticated user.
 Description

This endpoint allows an authenticated user to add a new task to a project. A task must have a title and can optionally include a description, an assignee, a due date, and a priority level.

Request Parameters

Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `project_id` | integer | Yes | The unique ID of the project the task belongs to. |

Body Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `title` | string | Yes | The name of the task. |
| `description` | string | No | Additional details about the task. |
| `assignee_id` | integer | No | The user ID of the person the task is assigned to. |
| `due_date` | string (ISO 8601 date) | No | The date the task is due, e.g. `2026-09-15`. |
| `priority` | string | No | One of `low`, `medium`, or `high`. Defaults to `medium` if not provided. |

 Request Headers

| Header | Required | Description |
|--------|----------|-------------|
| `Authorization` | Yes | Bearer token used to authenticate the user, e.g. `Bearer <access_token>`. |
| `Content-Type` | Yes | Must be `application/json`. |

 Example Request Body

json
{
  "title": "Prepare client presentation",
  "description": "Draft slides covering Q3 progress",
  "assignee_id": 42,
  "due_date": "2026-09-15",
  "priority": "high"
}


 Response Codes

| Status Code | Meaning |
|-------------|---------|
| `201 Created` | The task was created successfully. |
| `400 Bad Request` | The request body is missing a required field (such as `title`) or contains an invalid value (e.g. an invalid `priority`). |
| `401 Unauthorized` | The request is missing a valid authentication token. |
| `403 Forbidden` | The authenticated user does not have permission to add tasks to this project. |
| `404 Not Found` | The specified `project_id` does not exist. |

Example Successful Response (201 Created)

json
{
  "id": 501,
  "project_id": 17,
  "title": "Prepare client presentation",
  "description": "Draft slides covering Q3 progress",
  "assignee_id": 42,
  "due_date": "2026-09-15",
  "priority": "high",
  "status": "open",
  "created_at": "2026-08-28T14:22:00Z"
}
