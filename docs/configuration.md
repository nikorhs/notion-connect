# Configuration Guide

## Environment Setup

### 1. Create Environment File

Create a `.env` file in your project root:

```env
NOTION_API_KEY=your_notion_api_key
NOTION_DATABASE_ID=your_database_id
LOG_LEVEL=INFO
CACHE_TTL=3600
BATCH_SIZE=100
MAX_RETRIES=3
```

### 2. Configuration Options

| Option | Description | Default | Required |
|--------|-------------|---------|----------|
| NOTION_API_KEY | Your Notion integration token | - | Yes |
| NOTION_DATABASE_ID | Target database ID | - | Yes |
| LOG_LEVEL | Logging level (DEBUG, INFO, WARNING, ERROR) | INFO | No |
| CACHE_TTL | Cache time-to-live in seconds | 3600 | No |
| BATCH_SIZE | Maximum batch size for API calls | 100 | No |
| MAX_RETRIES | Maximum retry attempts for failed requests | 3 | No |

## Notion Setup

1. Create a Notion integration at https://www.notion.so/my-integrations
2. Note down the integration token
3. Create a database in Notion
4. Share the database with your integration
5. Copy the database ID from the URL

## Advanced Configuration

### Custom Logger Setup

```python
from notion_connect import configure_logging

configure_logging(
    log_file='app.log',
    log_level='DEBUG',
    format='%(asctime)s - %(name)s - %(levelname)s - %(message)s'
)
```

### Cache Configuration

```python
from notion_connect import configure_cache

configure_cache(
    ttl=3600,  # Time to live in seconds
    max_size=1000,  # Maximum number of items in cache
    strategy='lru'  # Cache eviction strategy
)
```