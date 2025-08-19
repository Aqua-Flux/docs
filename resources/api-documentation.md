# API Documentation

FLUX provides a comprehensive API for developers to integrate with the protocol.

## Base URL

```
https://api.aquaflux.tech
```

## Endpoints

### Get FLUX Price

```
GET /api/v1/price
```

Returns the current FLUX price and 24-hour change.

**Response:**
```json
{
  "success": true,
  "data": {
    "price_usd": 0.18,
    "price_change_24h": 2.5,
    "last_updated": "2024-01-15T12:00:00Z"
  }
}
```

### Get Portfolio Data

```
GET /api/v1/portfolio
```

Returns current portfolio composition and performance.

**Response:**
```json
{
  "success": true,
  "data": {
    "total_value_usd": 100000,
    "composition": {
      "pools": [...],
      "tokens": [...]
    },
    "performance": {
      "current_apr": 87.5,
      "daily_return": 239.73
    }
  }
}
```

### Get Complete Data

```
GET /api/v1/data
```

Returns comprehensive protocol data in one call.

**Response:**
```json
{
  "success": true,
  "data": {
    "token": {...},
    "price": {...},
    "supply": {...},
    "portfolio": {...},
    "market": {...}
  }
}
```

### Get Market Sentiment

```
GET /api/v1/sentiment
```

Returns Fear & Greed Index data and portfolio strategy.

**Response:**
```json
{
  "success": true,
  "data": {
    "index": 45,
    "classification": "Fear",
    "strategy": "Balanced allocation"
  }
}
```

### Get Performance Metrics

```
GET /api/v1/performance
```

Returns detailed performance and APR calculations.

**Query Parameters:**
- `detailed` (boolean) - Include projections and suggestions

**Response:**
```json
{
  "success": true,
  "data": {
    "current_apr": "87.50%",
    "expected_returns": {
      "daily_usd": "239.73",
      "monthly_usd": "7291.67",
      "yearly_usd": "87500.00"
    }
  }
}
```

## Integration Endpoints

### CoinGecko Compatible

```
GET /api/token-info
```

Returns token information in CoinGecko format.

### Chainlink Compatible

```
GET /api/price-feed
```

Returns price data in Chainlink format.

## Rate Limits

- 100 requests per minute per IP
- 1000 requests per hour per IP

## Response Headers

All API responses include:
- `X-API-Version` - Current API version
- `X-RateLimit-Limit` - Rate limit ceiling
- `X-RateLimit-Remaining` - Remaining requests
- `Cache-Control` - Caching directives

## WebSocket Events

Connect to real-time updates:

```javascript
const ws = new WebSocket('wss://api.aquaflux.tech/ws');

ws.on('message', (data) => {
  const event = JSON.parse(data);
  console.log('Event:', event.type, event.data);
});
```

Events:
- `price_update` - FLUX price changes
- `portfolio_update` - Portfolio rebalancing
- `mint` - New FLUX minted
- `burn` - FLUX redeemed

## Example Usage

### JavaScript/TypeScript

```javascript
// Fetch current FLUX price
const response = await fetch('https://api.aquaflux.tech/api/v1/price');
const data = await response.json();
console.log('FLUX Price:', data.data.price_usd);
```

### Python

```python
import requests

# Get portfolio data
response = requests.get('https://api.aquaflux.tech/api/v1/portfolio')
data = response.json()
print(f"Portfolio Value: ${data['data']['total_value_usd']}")
```

### cURL

```bash
# Get complete protocol data
curl https://api.aquaflux.tech/api/v1/data
```

## Error Handling

Errors return appropriate HTTP status codes:

```json
{
  "success": false,
  "error": "Error message",
  "timestamp": 1234567890
}
```

Status Codes:
- `200` - Success
- `400` - Bad Request
- `429` - Rate Limited
- `500` - Server Error

## Support

For API support or questions:
- [Telegram](https://t.me/aquaflux_tech)