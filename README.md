# Telegram Stories Downloader API

A powerful FastAPI-based service for downloading Telegram stories. Fetch active, pinned, and archived stories with ease.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/SmartStoryDownloader)

## Features

- Download active, pinned, and archived Telegram stories
- Fetch story metadata including captions, timestamps, and media types
- Automatic file hosting via tmpfiles.org
- Built with FastAPI and Pyrogram
- Optimized for serverless deployment on Vercel
- Fast and efficient with uvloop integration

## API Endpoints

### Base URL
```
https://your-deployment.vercel.app
```

### 1. Get Current Stories
Fetch all currently active stories from a user.

```http
GET /api/current?username={username}
```

**Example:**
```bash
curl "https://your-deployment.vercel.app/api/current?username=ISmartCoder"
```

**Response:**
```json
{
  "success": true,
  "username": "ISmartCoder",
  "count": 2,
  "stories": [
    {
      "story_id": 9,
      "type": "Active",
      "date": "2026-01-08 14:30:00",
      "timestamp": 1736348400,
      "caption": "Example caption",
      "has_media": true
    }
  ],
  "api_dev": "@ISmartCoder",
  "api_channel": "@abirxdhackz"
}
```

### 2. Get All Stories
Fetch all stories including active, pinned, and archived.

```http
GET /api/all?username={username}
```

**Example:**
```bash
curl "https://your-deployment.vercel.app/api/all?username=ISmartCoder"
```

**Response:**
```json
{
  "success": true,
  "username": "ISmartCoder",
  "total_count": 15,
  "stories": [
    {
      "story_id": 9,
      "type": "Active",
      "date": "2026-01-08 14:30:00",
      "timestamp": 1736348400,
      "caption": "Example caption",
      "has_media": true
    },
    {
      "story_id": 7,
      "type": "Pinned",
      "date": "2026-01-07 10:15:00",
      "timestamp": 1736245500,
      "caption": "",
      "has_media": true
    }
  ],
  "api_dev": "@ISmartCoder",
  "api_channel": "@abirxdhackz"
}
```

### 3. Download Specific Story
Download a specific story by its ID.

```http
GET /api/special?username={username}&storyid={story_id}
```

**Example:**
```bash
curl "https://your-deployment.vercel.app/api/special?username=ISmartCoder&storyid=9"
```

**Response:**
```json
{
  "success": true,
  "username": "ISmartCoder",
  "story_id": 9,
  "type": "Active",
  "media_type": "video",
  "date": "2026-01-08 14:30:00",
  "timestamp": 1736348400,
  "caption": "Example caption",
  "download_url": "https://tmpfiles.org/dl/12345/video.mp4",
  "expires_in": "60 minutes",
  "api_dev": "@ISmartCoder",
  "api_channel": "@abirxdhackz"
}
```

## Deployment

### Deploy to Vercel

1. Fork this repository
2. Create a new project on [Vercel](https://vercel.com)
3. Import your forked repository
4. Add the required environment variable:
   - `SESSION_STRING`: Your Telegram session string
5. Deploy

### Get Telegram Session String

You need a Telegram session string to authenticate with the API. You can generate one using:

1. Install Pyrogram: `pip install pyrofork`
2. Run this script:

```python
from pyrogram import Client

api_id = "YOUR_API_ID"
api_hash = "YOUR_API_HASH"

with Client("my_account", api_id=api_id, api_hash=api_hash) as app:
    print(app.export_session_string())
```

3. Get your API credentials from [my.telegram.org](https://my.telegram.org)

### Environment Variables

Create a `config.py` file or set environment variables:

```python
SESSION_STRING = "your_session_string_here"
```

## Local Development

### Prerequisites

- Python 3.10+
- Telegram API credentials
- Telegram session string

### Installation

1. Clone the repository:
```bash
git clone https://github.com/SmartStoryDownloader
cd SmartStoryDownloader
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create `config.py`:
```python
SESSION_STRING = "your_session_string_here"
```

4. Run the server:
```bash
python api.py
```

The API will be available at `http://localhost:4747`

## Project Structure

```
.
â”œâ”€â”€ api.py              # Main FastAPI application
â”œâ”€â”€ config.py           # Configuration file
â”œâ”€â”€ requirements.txt    # Python dependencies
â”œâ”€â”€ pyproject.toml     # Project metadata
â””â”€â”€ README.md          # This file
```

## Dependencies

- fastapi: Modern web framework for building APIs
- uvicorn: ASGI server implementation
- pyrofork: Telegram MTProto API framework
- tgcrypto: Cryptography for Telegram
- aiohttp: Async HTTP client/server
- uvloop: Fast event loop implementation
- python-dateutil: Date utilities

## Error Handling

The API returns appropriate HTTP status codes:

- `200`: Success
- `400`: Bad request (invalid parameters)
- `404`: Story not found
- `500`: Server error

All error responses include:
```json
{
  "success": false,
  "error": "Error description",
  "api_dev": "@ISmartCoder",
  "api_channel": "@abirxdhackz"
}
```

## Rate Limiting

Be mindful of Telegram's rate limits. Excessive requests may result in temporary restrictions.

## Notes

- Downloaded files are temporarily hosted on tmpfiles.org and expire after 60 minutes
- The API supports photos, videos, and documents
- Stories are automatically searched in active, pinned, and archived collections

## Credits

- **Developer**: [@ISmartCoder](https://t.me/ISmartCoder)
- **Channel**: [@abirxdhackz](https://t.me/abirxdhackz)

## License

This project is open source and available under the MIT License.

## Support

For issues, questions, or contributions, please visit:
- GitHub: [github.com/SmartStoryDownloader](https://github.com/SmartStoryDownloader)
- Telegram: [@ISmartCoder](https://t.me/ISmartCoder)

## Disclaimer

This tool is for educational purposes only. Make sure you comply with Telegram's Terms of Service and respect users' privacy.