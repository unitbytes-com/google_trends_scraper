# google-trends-scraper

![Google Trends Scraper Actor Logo](https://images.apifyusercontent.com/oYyezynONTeIZJZbuoM0mrzdKFbdCiB-8HkdYEaJ_Ew/rs:fill:250:250/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vM1ByZFpVREtZWFVYWkxXTTMtYWN0b3ItcXA2bUtTU2NZb3V0WXFDT2EtN21NQXoyNUMxaS1nb29nbGVfdHJlbmRzX2FjdG9yLmpwZw.webp) 

# **Google Trends Scraper**  
Fetch real-time trending searches, interest over time, interest by region, and related queries/topics with a single, configurable Apify actor.

***

## Overview

Struggling to scrape data from Google Trends? This easy-to-use, reliable scraper gives you access to all the data you need. Try it free for 1 day—with no credit card required—and only pay if you love it.

`google-trends-scraper` wraps the [Google Trends Scraper actor on Apify](https://apify.com/unitbytes/google-trends-scraper?fpr=939u3w&fp_sid=20251002), providing:

- **Trending Now** (realtime hot searches)  
- **Interest Over Time** (time series for keywords)  
- **Interest By Region** (geographic breakdown)  
- **Related Queries & Topics** (top & rising searches)  

***

## Filters for Trending Data    
 
- **web** to get Trending Data based on web searchs  
- **images** to get Trending Data based on image searchs  
- **news** to get Trending Data based on news searchs  
- **shopping** to get Trending Data based on shopping searchs  
- **youtube** to get Trending Data based on youtube searchs  

## Quickstart

### Apify CLI

```bash
npx apify run UnitBytes/google-trends-scraper \
  --input '{"scrape_type":"trending_now","common_geo":"US","trending_hours":24}'
```

### HTTP API

```bash
curl -X POST https://api.apify.com/v2/acts/unitbytes~google-trends-scraper/runs \
     -H "Content-Type: application/json" \
     -d '{"scrape_type":"trending_now","common_geo":"US","trending_hours":24}'
```

***

## Detailed Usage

### Node.js

```javascript
import { ApifyClient } from 'apify-client';

// Initialize the ApifyClient with your Apify API token
// Replace the '<YOUR_API_TOKEN>' with your token
const client = new ApifyClient({
    token: '<YOUR_API_TOKEN>',
});

// Prepare Actor input
const input = {
    "keywords": [
        "Web scraping"
    ]
};

// Run the Actor and wait for it to finish
const run = await client.actor(\"unitbytes/google-trends-scraper\").call(input);

// Fetch and print Actor results from the run's dataset (if any)
console.log('Results from dataset');
console.log(`💾 Check your data here: https://console.apify.com/storage/datasets/${run.defaultDatasetId}`);
const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach((item) => {
    console.dir(item);
});

```


### MCP
```
{
    "mcpServers": {
        "apify": {
            "command": "npx",
            "args": [
                "mcp-remote",
                "https://mcp.apify.com/?tools=UnitBytes/google-trends-scraper",
                "--header",
                "Authorization: Bearer <YOUR_API_TOKEN>"
            ]
        }
    }
}
```

### Python

```python
from apify_client import ApifyClient

# Initialize the ApifyClient with your Apify API token
# Replace '<YOUR_API_TOKEN>' with your token.
client = ApifyClient("<YOUR_API_TOKEN>")

# Prepare the Actor input
run_input = { "keywords": ["Web scraping"] }

# Run the Actor and wait for it to finish
run = client.actor(\"unitbytes/google-trends-scraper\").call(run_input=run_input)

# Fetch and print Actor results from the run's dataset (if there are any)
print("💾 Check your data here: https://console.apify.com/storage/datasets/" + run["defaultDatasetId"])
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(item)

```

***

## Example Inputs & Outputs

| Use Case                               | Input JSON                                                                                                   |
|----------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Realtime trending (US, 24h)            | `{"scrape_type":"trending_now","common_geo":"US","trending_hours":24}`                                       |
| Interest over time (US)                | `{"scrape_type":"interest_over_time","keywords":["data science"],"predefined_timeframe":"today 12-m"}`       |
| Related queries (global)               | `{"scrape_type":"related_queries","keywords":["python"],"predefined_timeframe":"today 12-m"}`                |

Each run writes one dataset item containing:
- `scrape_type`  
- `data` (results array or object)  
- `input_summary` (geo, timeframe, resolution, etc.)  
- `error` & `error_message`  

***

## Best Practices

- **Rate Limits:** Use shorter timeframes or proxies to avoid `429` errors.  
- **Data Volume:** Limit `geo_resolution` to `COUNTRY` or `REGION` before scaling to `CITY`/`DMA`.  
- **Time Range:** The `trending_now` type supports 1–191 hours.  
- **Empty Results:** Ensure keywords have sufficient search volume in chosen geo/timeframe.  

***

## Contributing

Contributions are welcome! Please open issues or submit pull requests for:

- Bug fixes  
- New examples (Node.js, Python, shell)  
- Improved documentation or tutorials  

Refer to [CONTRIBUTING.md](./CONTRIBUTING.md) for details.

***

## License & Support

This project is licensed under the MIT License.  
For actor support, visit the [Apify Store listing](https://apify.com/unitbytes/google-trends-scraper?fpr=939u3w&fp_sid=20251002) or contact [radwanfaris13@gmail.com](mailto:radwanfaris13@gmail.com).

*Happy scraping!*