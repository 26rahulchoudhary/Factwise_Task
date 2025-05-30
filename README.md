# RahulChoudhary_Factwise
Team project planner tool

# Team Project Planner

A Python-based team project planner tool that helps manage users, teams, and project boards. The application provides a clean and modular implementation with proper abstractions and efficient data persistence.

## Features

1. User Management
   - Create and manage users with unique usernames
   - Update user display names
   - List all users and their details
   - View user's team memberships

2. Team Management
   - Create and manage teams with unique names
   - Assign team administrators
   - Add/remove team members (up to 50 members per team)
   - List team members and team details

3. Project Board Management
   - Create project boards for teams
   - Add tasks and assign them to team members
   - Track task status (OPEN, IN_PROGRESS, COMPLETE)
   - Close boards when all tasks are complete
   - Export board details to formatted text files

## Design Choices

1. Data Models
   - Used Pydantic for data validation and serialization
   - Strict type checking and field constraints
   - Clear separation between creation and full models

2. Storage Implementation
   - File-based JSON storage for persistence
   - Generic storage class for reusability
   - Automatic handling of datetime serialization/deserialization
   - Thread-safe file operations

3. Architecture
   - Clean separation of concerns (models, storage, business logic)
   - Abstract base classes for core functionality
   - Concrete implementations with proper validation
   - User-friendly wrapper class (TeamProjectPlanner)

4. Error Handling
   - Comprehensive input validation
   - Clear error messages for invalid operations
   - Proper constraint checking (unique names, member limits, etc.)

## Dependencies

- pydantic>=2.5.2: For data validation and serialization
- python-dateutil>=2.8.2: For date/time handling
- tabulate>=0.9.0: For formatted board exports

## Usage Example
## For running the tool type python interactive_panner.py on the terminal
```python
from main import TeamProjectPlanner

# Initialize the planner
planner = TeamProjectPlanner()

# Create users
user1 = planner.create_user("john_doe", "John Doe")
user2 = planner.create_user("jane_smith", "Jane Smith")

# Create a team
team = planner.create_team("Development Team", "Main development team", user1_id)
team_id = json.loads(team)["id"]

# Add users to team
planner.add_users_to_team(team_id, [user2_id])

# Create a board and add tasks
board = planner.create_board("Sprint 1", "First sprint board", team_id)
board_id = json.loads(board)["id"]

task1 = planner.add_task("Implement API", "Create REST API endpoints", user1_id, board_id)
task2 = planner.add_task("Write tests", "Add unit tests", user2_id, board_id)

# Update task status
planner.update_task_status(task1_id, "COMPLETE")
planner.update_task_status(task2_id, "COMPLETE")

# Close and export board
planner.close_board(board_id)
export_result = planner.export_board(board_id)
```

## Assumptions and Rationale

1. File Storage
   - JSON format chosen for human-readable persistence
   - Separate files for users, teams, boards, and tasks
   - UUIDs used for unique identifiers

2. Task Management
   - Tasks belong to a single board
   - Only team members can be assigned tasks
   - Task titles must be unique within a board

3. Board Management
   - Boards can only be closed when all tasks are complete
   - Each team can have multiple boards
   - Board names must be unique within a team

4. Team Structure
   - Single admin per team
   - Maximum 50 members per team
   - Users can be members of multiple teams





