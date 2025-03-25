# Usage Guide

## Basic Usage

### 1. Initialize Components

```python
from notion_connect import NotionAPI, TaskParser, TaskAnalyzer

api = NotionAPI()
parser = TaskParser()
analyzer = TaskAnalyzer()
```

### 2. Parse Tasks

```python
# Parse from different formats
task_md = parser.parse_task('# Task Title\nDescription', format='markdown')
task_yaml = parser.parse_task('title: Task\ndescription: Details', format='yaml')
task_json = parser.parse_task('{"title": "Task"}', format='json')
```

### 3. Analyze Tasks

```python
analysis = analyzer.analyze_task(task)
print(f'Categories: {analysis["categories"]}')
print(f'Priority Score: {analysis["priority_score"]}')
print(f'Estimated Duration: {analysis["estimated_duration"]["estimated_hours"]} hours')
```

### 4. Sync with Notion

```python
# Create a task
task_id = api.create_task(task)

# Update a task
api.update_task(task_id, {"status": "In Progress"})

# Batch operations
tasks = [task1, task2, task3]
api.batch_create_tasks(tasks)
```

## Advanced Usage

### Working with Dependencies

```python
# Create tasks with dependencies
tasks = [
    {"title": "Task 1", "dependencies": []},
    {"title": "Task 2", "dependencies": ["Task 1"]},
    {"title": "Task 3", "dependencies": ["Task 2"]}
]

# Get critical path
critical_path = parser.get_critical_path(tasks)
print(f'Critical Path: {critical_path}')
```

### Template Management

```python
# Create a template
template = {
    "title": "Bug Fix Template",
    "description": "Template for bug fixes",
    "properties": {
        "priority": "High",
        "type": "Bug"
    }
}

# Create task from template
task = api.create_from_template(template, {
    "title": "Fix Login Issue",
    "description": "Users cannot log in"
})
```

### Batch Processing

```python
# Configure batch settings
api.configure_batch({
    "size": 100,
    "concurrent_requests": 5,
    "rate_limit": 3  # requests per second
})

# Process multiple tasks
results = api.batch_process(tasks, operation='create')
```

### Error Handling

```python
from notion_connect.exceptions import (
    NotionAPIError,
    ValidationError,
    RateLimitError
)

try:
    api.create_task(task)
except RateLimitError:
    print("Rate limit exceeded. Waiting...")
except ValidationError as e:
    print(f"Invalid task: {e}")
except NotionAPIError as e:
    print(f"API error: {e}")
```