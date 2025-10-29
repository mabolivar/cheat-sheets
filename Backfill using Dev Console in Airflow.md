The following code chunk shows how to trigger multiple tasks using the airflow API in the Developer console.

Before executing, please update:

- `baseUrl`
- `cookieValue`
- `csrfToken`

```js
// Configuration
const startDate = '2025-06-10'; // PLACEHOLDER: Start date in YYYY-MM-DD format
const endDate = '2025-06-30';   // PLACEHOLDER: End date in YYYY-MM-DD format

const baseUrl = 'https://<interna_url>/dags/<job>/trigger?origin=%2Fdags%2Fcustomer__competing_widgets_logs__r__main%2Fgrid';
const method = 'POST';

// --- ACTUAL VALUES PROVIDED BY USER ---
const cookieValue = '';
const csrfToken = '';
// --- END OF ACTUAL VALUES ---

const headers = {
    'Content-Type': 'application/x-www-form-urlencoded',
    'Cookie': cookieValue,
    'Origin': 'https://ddp-prio-workflow.g8s-data-platform-prod.glovoint.com',
    'Referer': 'https://ddp-prio-workflow.g8s-data-platform-prod.glovoint.com/dags/customer__competing_widgets_logs__r__main/trigger?origin=%2Fdags%2Fcustomer__comping_widgets_logs__r__main%2Fgrid',
    'Cache-Control': 'max-age=0',
    'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image:apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7',
    'Accept-Encoding': 'gzip, deflate, br, zstd',
    'Accept-Language': 'es-ES,es;q=0.9,en;q=0.8,ca;q=0.7',
};

// Function to generate dates between start and end date
function generateDateRange(startDate, endDate) {
    const dates = [];
    const currentDate = new Date(startDate);
    const end = new Date(endDate);
    
    while (currentDate <= end) {
        dates.push(new Date(currentDate));
        currentDate.setDate(currentDate.getDate() + 1);
    }
    
    return dates;
}

// Function to format date for the request payload
function formatDateForPayload(date) {
    return date.toISOString().replace(/\.\d{3}Z$/, '+00:00');
}

// Function to make a single request
async function makeRequest(executionDate) {
    const requestPayload = `csrf_token=${encodeURIComponent(csrfToken)}&dag_id=customer__competing_widgets_logs__r__main&origin=https%3A%2F%2Fddp-prio-workflow.g8s-data-platform-prod.glovoint.com%2Fdags%2Fcustomer__competing_widgets_logs__r__main%2Fgrid&recent_configs=%7B%7D&execution_date=${encodeURIComponent(executionDate)}&run_id=&conf=%7B%7D`;
    
    try {
        const response = await fetch(baseUrl, {
            method: method,
            headers: headers,
            body: requestPayload
        });
        
        console.log(`Request for ${executionDate}:`);
        console.log('Response Status:', response.status);
        
        if (response.ok || response.redirected) {
            console.log('✅ Request successful or redirected');
        } else {
            console.log('❌ Request failed');
            const errorText = await response.text();
            console.error('Error Response Body:', errorText);
        }
        
        return { date: executionDate, status: response.status, success: response.ok || response.redirected };
    } catch (error) {
        console.error(`❌ Fetch error for ${executionDate}:`, error);
        return { date: executionDate, status: 'ERROR', success: false, error: error.message };
    }
}

// Main function to process all dates
async function processDateRange() {
    console.log(`Starting requests for date range: ${startDate} to ${endDate}`);
    
    const dates = generateDateRange(startDate, endDate);
    console.log(`Generated ${dates.length} dates to process`);
    
    const results = [];
    
    // Process dates sequentially to avoid overwhelming the server
    for (let i = 0; i < dates.length; i++) {
        const date = dates[i];
        const formattedDate = formatDateForPayload(date);
        
        console.log(`\n--- Processing date ${i + 1}/${dates.length}: ${formattedDate} ---`);
        
        const result = await makeRequest(formattedDate);
        results.push(result);
        
        // Add a small delay between requests to be respectful to the server
        if (i < dates.length - 1) {
            console.log('Waiting 1 second before next request...');
            await new Promise(resolve => setTimeout(resolve, 1000));
        }
    }
    
    // Summary
    console.log('\n=== SUMMARY ===');
    const successful = results.filter(r => r.success).length;
    const failed = results.filter(r => !r.success).length;
    
    console.log(`Total requests: ${results.length}`);
    console.log(`Successful: ${successful}`);
    console.log(`Failed: ${failed}`);
    
    if (failed > 0) {
        console.log('\nFailed dates:');
        results.filter(r => !r.success).forEach(r => {
            console.log(`- ${r.date}: ${r.status} ${r.error || ''}`);
        });
    }
    
    return results;
}

// Execute the date range processing
processDateRange().catch(error => {
    console.error('Fatal error:', error);
});
```