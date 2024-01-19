# google-org-chart
google visualization chart - organization chart
this is a project for orgnization chart


// Load the SQL.js library
const sql = window.SQL;

async function openDatabase() {
    return await new sql.Database(sql.FS.readFile('mydata.db'));
}

async function searchDatabase(searchTerm) {
    const db = await openDatabase();

    // Replace with your actual table name and column to search
    const result = await db.exec(`SELECT * FROM my_table WHERE my_column LIKE '%${searchTerm}%'`);

    const resultsDiv = document.getElementById('results');
    resultsDiv.innerHTML = ''; // Clear previous results

    for (const row of result.rows) {
        const rowDiv = document.createElement('div');
        rowDiv.textContent = JSON.stringify(row); // Display row data as JSON
        resultsDiv.appendChild(rowDiv);
    }
}

// Event listener for the search button
document.getElementById('search-button').addEventListener('click', () => {
    const searchTerm = document.getElementById('search-input').value;
    searchDatabase(searchTerm);
});
