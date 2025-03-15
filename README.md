# Server-side GTM Tag Template - Forward Event Data to HTTP Endpoints

This tag template forwards the event data to any HTTP endpoints for debugging (example use cases: Forward to Cloud Functions & write to BigQuery dataset, Send to webhook.site to debug Shopify checkout events, etc.)

## Features

- **Simple Configuration**: Just add your endpoint URL and you're ready to go
- **Automatic Data Collection**: Captures all event data using GTM's `getAllEventData()`
- **Key Sanitization**: Automatically replaces hyphens with underscores in all keys
- **Debug Logging**: Detailed request and response logging in preview/debug mode
- **Standard HTTP Status Handling**: Success for 200-299 status codes

## Use Cases

- **Debug Event Data**: Forward to webhook.site or similar services to inspect real-time event data
- **Data Warehousing**: Send to Cloud Functions to process and store in BigQuery
- **Custom Analytics**: Forward to your own analytics endpoints
- **Event Monitoring**: Track specific events across your website or app
- **Server-side Integration**: Connect with third-party APIs

## Setup Instructions

1. **Import the Template**: Add this template to your GTM server container
2. **Create a New Tag**: Select this template type
3. **Configure the Endpoint**: Enter the URL where you want to send the data
4. **Set Triggers**: Configure when this tag should fire
5. **Test in Preview Mode**: Use the preview mode to verify data is being sent correctly

## Technical Details

- **Request Method**: Fixed as POST
- **Content Type**: application/json
- **Payload**: Includes all event data with the endpoint URL added as `http_endpoint_url`
- **HTTP Status**: Success (200-299) triggers gtmOnSuccess, others trigger gtmOnFailure

## Examples

### Debugging with webhook.site

1. Go to [webhook.site](https://webhook.site)
2. Copy your unique URL
3. Paste the URL into the template's endpoint URL field
4. Preview your container to see real-time event data

### Sending to Google Cloud Functions

```javascript
// Example Cloud Function to receive the data
exports.processEventData = (req, res) => {
	const eventData = req.body;

	// Process the data (e.g., write to BigQuery)
	console.log('Received event data:', eventData);

	// Send a success response back to GTM
	res.status(200).send('Success');
};
```

## Limitations

- Only supports POST requests
- Does not support custom headers
- Does not support custom request timeouts

## Troubleshooting

- **No Data Received**: Verify your endpoint URL is correct and accessible
- **Missing Event Data**: Check triggers to ensure the tag fires at the right time
- **Errors in Debug Mode**: Review the response status and body in the preview console

## Version History

- **1.0.0**: Initial release
