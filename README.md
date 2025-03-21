# Autocomplete-Scraper

This project extracts all possible names from an undocumented autocomplete API. The script systematically queries the API, handles rate limits, and efficiently gathers data using a breadth-first search approach.

## API Exploration Findings
- **Base URL:** `http://35.200.185.69:8000/v1/autocomplete?query=`
- **Response Format:**
  ```json
  {
    "version": "v1",
    "count": 10,
    "results": ["example1", "example2", ...]
  }
  ```
- **Max Results Per Request:** 10 (suggesting pagination may be needed)
- **Rate Limiting:** Returns HTTP `429 Too Many Requests`, requiring backoff handling.
- **Search Behavior:** Expanding query prefixes (e.g., `a -> aa, ab, ac...`) yields more results.

## Approach
1. **BFS Query Expansion:**
   - Start with `a-z` and progressively append characters from discovered names.
2. **Rate Limit Handling:**
   - If `429` occurs, wait and retry with an exponential backoff.
3. **Efficient Storage:**
   - Store found names in a JSON file (`names.json`) and update periodically.

## Requirements
- Python 3
- `requests` library

## Usage
1. Install dependencies (if not already installed):
   ```bash
   pip install requests
   ```
2. Run the script:
   ```bash
   python scraper.py
   ```
3. Extracted names will be saved in `names.json`.

## Results
- **Total Requests Made:** 27
- **Total Unique Names Retrieved:** 260
- **Execution Time:** 24 seconds

## Future Enhancements
- Optimize query selection for faster discovery.
- Implement multi-threading for parallel requests.
- Explore alternative strategies for expanding queries.

## Author
Pradnya Devendra Ukey

