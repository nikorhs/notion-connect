# API Reference

## Core Classes

### NotionAPI

Main class for interacting with the Notion API.

```python
class NotionAPI:
    def __init__(self, api_key: Optional[str] = None):
        """Initialize the Notion API client."""

    def create_task(self, task: Task) -> str:
        """Create a new task in Notion."""

    def update_task(self, task_id: str, properties: Dict) -> None:
        """Update an existing task."""

    def batch_create_tasks(self, tasks: List[Task]) -> List[str]:
        """Create multiple tasks in batch."""
```

### TaskParser

Handles parsing of tasks from various formats.

```python
class TaskParser:
    def parse_task(self, content: str, format: str = "auto") -> Task:
        """Parse task content into a Task object."""

    def get_critical_path(self, tasks: List[Task]) -> List[str]:
        """Calculate the critical path of tasks."""
```

### TaskAnalyzer

Provides AI-powered task analysis.

```python
class TaskAnalyzer:
    def analyze_task(self, task: Task) -> Dict:
        """Perform comprehensive task analysis."""

    def predict_category(self, task: Task) -> List[str]:
        """Predict task categories."""
```

## Data Types

### Task

```python
Task = TypedDict('Task', {
    'title': str,
    'description': str,
    'status': str,
    'priority': Optional[str],
    'due_date': Optional[datetime],
    'tags': List[str],
    'subtasks': List['Task'],
    'dependencies': List[str]
})
```

### Analysis Result

```python
AnalysisResult = TypedDict('AnalysisResult', {
    'categories': List[str],
    'priority_score': float,
    'complexity': Dict[str, Union[float, str]],
    'estimated_duration': Dict[str, Union[float, str]],
    'suggested_deadline': datetime,
    'key_entities': List[str]
})
```

## Exceptions

```python
class NotionSyncError(Exception):
    """Base exception for notion-connect."""

class ValidationError(NotionSyncError):
    """Raised when task validation fails."""

class NotionAPIError(NotionSyncError):
    """Raised when Notion API request fails."""

class RateLimitError(NotionAPIError):
    """Raised when API rate limit is exceeded."""
```