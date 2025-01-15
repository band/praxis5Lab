```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CO2 Data Fetch Test</title>
    <style>
        body {
            font-family: sans-serif;
            max-width: 800px;
            margin: 20px auto;
            padding: 0 20px;
        }
        #status {
            padding: 10px;
            margin: 10px 0;
            border-radius: 4px;
        }
        .success {
            background-color: #d4edda;
            color: #155724;
        }
        .error {
            background-color: #f8d7da;
            color: #721c24;
        }
    </style>
</head>
<body>
    <h1>CO2 Data Fetch Test</h1>
    <button onclick="fetchData()">Fetch Data</button>
    <div id="status"></div>

    <script>
        // Replace this URL with your actual Render.com proxy URL
        const PROXY_URL = 'https://your-proxy-name.onrender.com/api/co2-data';
        
        async function fetchData() {
            const statusDiv = document.getElementById('status');
            statusDiv.className = '';
            statusDiv.textContent = 'Fetching data...';

            try {
                const response = await fetch(PROXY_URL);
                if (!response.ok) {
                    throw new Error(`HTTP error! status: ${response.status}`);
                }
                const data = await response.text();
                
                // Log data to console instead of displaying
                console.log('Data fetched successfully');
                console.log('First 500 characters:', data.substring(0, 500));
                
                statusDiv.className = 'success';
                statusDiv.textContent = 'Data fetched successfully! Check the console for details.';
            } catch (error) {
                console.error('Error:', error);
                statusDiv.className = 'error';
                statusDiv.textContent = `Error fetching data: ${error.message}`;
            }
        }
    </script>
</body>
</html>

```

To use this file:

1. Save it as `index.html`
2. Replace `your-proxy-name` in the `PROXY_URL` constant with your actual Render.com proxy URL
3. Open it in a web browser

The page will:
- Show a simple button to trigger the data fetch
- Display the fetch status
- Log the raw data to the console instead of displaying it
- Handle and display any errors that occur

To test locally, you can use Python's built-in server:
```bash
python -m http.server 8000
```

Then visit `http://localhost:8000` in your browser.

Remember to update the `PROXY_URL` with your actual Render.com
deployment URL (it will look something like
`https://co2-proxy-xyz.onrender.com/api/co2-data`).
