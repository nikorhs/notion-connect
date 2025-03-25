# Installation Guide

## Prerequisites

- Python 3.8 or higher
- pip package manager
- Git (optional)

## Installation Steps

### 1. Install from PyPI

```bash
pip install notion-connect
```

### 2. Install from Source

```bash
git clone https://github.com/nikorhs/notion-connect.git
cd notion-connect
pip install -e .
```

### 3. Install NLP Dependencies

```bash
python -m spacy download en_core_web_sm
```

## Verifying Installation

```python
from notion_connect import NotionAPI

api = NotionAPI()
print(api.version)  # Should print the current version
```

## Troubleshooting

### Common Issues

1. **Missing Dependencies**
   ```bash
pip install -r requirements.txt
   ```

2. **Spacy Model Issues**
   ```bash
python -m spacy validate
   ```

3. **Version Conflicts**
   ```bash
pip install --upgrade notion-connect
   ```