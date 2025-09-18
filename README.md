[check.html](https://github.com/user-attachments/files/22401321/check.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DepEd Legal Section - Complaint Inventory System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Include Chart.js library for creating graphs -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        body {
            font-family: 'Inter', sans-serif;
            background-image: url("1b57fed7-3de8-4009-aac6-9e821635db67.jpg");
            background-size: cover;
            background-position: center;
            background-repeat: no-repeat;
            background-attachment: fixed;
            background-color: #f3f4f6; /* Fallback color */
            color: #1a202c;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
            background-color: rgba(255, 255, 255, 0.9);
            border-radius: 0.75rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .tab-content {
            display: none;
        }
        .tab-content.active {
            display: block;
        }
        .tab-button.active {
            border-bottom: 2px solid #1e40af;
            color: #1e40af;
            font-weight: 600;
        }
        .card {
            background-color: white;
            border-radius: 0.75rem;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 2rem;
        }
        .table-container {
            overflow-x: auto;
        }
        td, th {
            white-space: nowrap;
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-800">

    <div class="container py-8">
        <!-- Header -->
        <header class="text-center mb-8">
            <div class="flex items-center justify-between">
                <img src="https://placehold.co/96x96/60A5FA/FFFFFF?text=DepEd" alt="DepEd Negros Island Region Logo" class="h-24 mr-4">
                <div class="text-center flex-grow">
                    <h1 class="text-3xl font-bold text-gray-900 mb-2">DEPARTMENT OF EDUCATION - NEGROS ISLAND REGION</h1>
                    <h2 class="text-xl font-medium text-blue-800">Legal Section - Complaint Inventory System</h2>
                </div>
                <img src="https://placehold.co/96x96/2B6CB0/FFFFFF?text=National" alt="DepEd National Logo" class="h-24 ml-4">
            </div>
        </header>

        <!-- Tabs Navigation -->
        <nav class="bg-white rounded-lg p-2 mb-8 shadow-sm">
            <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                <button class="tab-button active flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('dashboard')">🏠 Dashboard</button>
                <button class="tab-button flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('complaints')">📝 Complaint Management</button>
                <button class="tab-button flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('reports')">📊 Reports</button>
                <button class="tab-button flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('users')">⚙️ User Management</button>
            </div>
        </nav>

        <!-- Main Content -->
        <main>
            <!-- Dashboard Tab -->
            <div id="dashboard" class="tab-content active">
                <div class="card">
                    <h3 class="text-2xl font-semibold mb-6">SYSTEM OVERVIEW</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                        <div class="bg-blue-50 p-6 rounded-lg shadow-sm text-center">
                            <p class="text-4xl font-bold text-blue-800 flex items-center justify-center space-x-2" id="totalComplaintsCount">
                                <span>0</span>
                                <span>⚖️</span>
                            </p>
                            <p class="text-blue-600 mt-2">Total Complaints</p>
                        </div>
                        <div class="bg-yellow-50 p-6 rounded-lg shadow-sm text-center">
                            <p class="text-4xl font-bold text-yellow-800 flex items-center justify-center space-x-2" id="ongoingComplaintsCount">
                                <span>0</span>
                                <span>⏰</span>
                            </p>
                            <p class="text-yellow-600 mt-2">Ongoing</p>
                        </div>
                        <div class="bg-green-50 p-6 rounded-lg shadow-sm text-center">
                            <p class="text-4xl font-bold text-green-800 flex items-center justify-center space-x-2" id="resolvedComplaintsCount">
                                <span>0</span>
                                <span>✅</span>
                            </p>
                            <p class="text-green-600 mt-2">Resolved</p>
                        </div>
                        <div class="bg-gray-50 p-6 rounded-lg shadow-sm text-center">
                            <p class="text-4xl font-bold text-gray-800 flex items-center justify-center space-x-2" id="cancelledComplaintsCount">
                                <span>0</span>
                                <span>❌</span>
                            </p>
                            <p class="text-gray-600 mt-2">Cancelled</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Complaints Tab -->
            <div id="complaints" class="tab-content">
                <div class="card mb-8">
                    <h3 class="text-2xl font-semibold mb-6">Add New Complaint</h3>
                    <form id="addComplaintForm" class="space-y-4">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                            <div>
                                <label for="complainant" class="block text-sm font-medium text-gray-700">Complainant's Name</label>
                                <input type="text" id="complainant" name="complainant" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                            </div>
                            <div>
                                <label for="respondent" class="block text-sm font-medium text-gray-700">Respondent's Name</label>
                                <input type="text" id="respondent" name="respondent" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                            </div>
                        </div>
                        <div>
                            <label for="complaintType" class="block text-sm font-medium text-gray-700">Type of Complaint</label>
                            <select id="complaintType" name="complaintType" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                                <option value="">Select Type</option>
                                <option value="Administrative">Administrative</option>
                                <option value="School Site Issues">School Site Issues</option>
                                <option value="Local Complaints">Local Complaints</option>
                                <option value="Change of School Records">Change of School Records</option>
                                <option value="Child/Sexual Abuse">Child/Sexual Abuse</option>
                            </select>
                        </div>
                        <div>
                            <label for="place" class="block text-sm font-medium text-gray-700">Place of Complaint</label>
                            <input type="text" id="place" name="place" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                        </div>
                         <div>
                            <label for="division" class="block text-sm font-medium text-gray-700">Division of Complaint</label>
                            <select id="division" name="division" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                                <option value="">Select Division</option>
                                <option value="Bacolod City">Bacolod City</option>
                                <option value="Bago City">Bago City</option>
                                <option value="Bais City">Bais City</option>
                                <option value="Bayawan City">Bayawan City</option>
                                <option value="Cadiz City">Cadiz City</option>
                                <option value="Canlaon City">Canlaon City</option>
                                <option value="Dumaguete City">Dumaguete City</option>
                                <option value="Escalante City">Escalante City</option>
                                <option value="Guihulngan City">Guihulngan City</option>
                                <option value="Himamaylan City">Himamaylan City</option>
                                <option value="Kabankalan City">Kabankalan City</option>
                                <option value="La Carlota City">La Carlota City</option>
                                <option value="Negros Occidental">Negros Occidental</option>
                                <option value="Negros Oriental">Negros Oriental</option>
                                <option value="Sagay City">Sagay City</option>
                                <option value="San Carlos City">San Carlos City</option>
                                <option value="Silay City">Silay City</option>
                                <option value="Sipalay City">Sipalay City</option>
                                <option value="Siquijor">Siquijor</option>
                                <option value="Tanjay City">Tanjay City</option>
                                <option value="Victorias City">Victorias City</option>
                            </select>
                        </div>
                        <div>
                            <label for="details" class="block text-sm font-medium text-gray-700">Details</label>
                            <textarea id="details" name="details" rows="3" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500"></textarea>
                        </div>
                        <div>
                            <label for="status" class="block text-sm font-medium text-gray-700">Initial Status</label>
                            <select id="status" name="status" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                                <option value="Ongoing">Ongoing</option>
                                <option value="Resolved">Resolved</option>
                                <option value="Cancelled">Cancelled</option>
                            </select>
                        </div>
                        <div>
                            <label for="attachment" class="block text-sm font-medium text-gray-700">File Reference</label>
                            <input type="text" id="attachment" name="attachment" placeholder="e.g., scan_of_birth_cert.pdf" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                            <p class="mt-1 text-xs text-gray-500">Note: This system does not save the file itself. Please provide a filename or description for reference.</p>
                        </div>
                        <div class="text-right">
                            <button type="submit" class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                                Add Complaint
                            </button>
                        </div>
                    </form>
                </div>

                <div class="card">
                    <h3 class="text-2xl font-semibold mb-4">CURRENT COMPLAINTS</h3>
                    <!-- Search Bar -->
                    <div class="mb-4">
                        <label for="complaintSearch" class="block text-sm font-medium text-gray-700">Search for a Complainant or Respondent</label>
                        <input type="text" id="complaintSearch" placeholder="Type a name to search..." class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                    </div>
                    <div class="table-container">
                        <table class="min-w-full divide-y divide-gray-200">
                            <thead class="bg-gray-50">
                                <tr>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">ID</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Complainant</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Respondent</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Type</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Place</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Division</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Date Filed</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Status</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">File Reference</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Flags</th>
                                    <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Actions</th>
                                </tr>
                            </thead>
                            <tbody id="complaintsTableBody" class="bg-white divide-y divide-gray-200">
                                <!-- Complaints will be dynamically added here -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>

            <!-- Reports Tab -->
            <div id="reports" class="tab-content">
                <div class="card mb-8">
                    <h3 class="text-2xl font-semibold mb-6">Complaint Trends by Type and Month</h3>
                    <div class="relative h-96">
                        <canvas id="complaintsChart"></canvas>
                    </div>
                </div>
                <div class="card">
                    <h3 class="text-2xl font-semibold mb-6">Generate Report</h3>
                    <form id="reportForm" class="space-y-4">
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                            <div>
                                <label for="reportStatus" class="block text-sm font-medium text-gray-700">Filter by Status</label>
                                <select id="reportStatus" name="reportStatus" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                                    <option value="all">All</option>
                                    <option value="Ongoing">Ongoing</option>
                                    <option value="Resolved">Resolved</option>
                                    <option value="Cancelled">Cancelled</option>
                                </select>
                            </div>
                            <div>
                                <label for="startDate" class="block text-sm font-medium text-gray-700">Start Date</label>
                                <input type="date" id="startDate" name="startDate" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                            </div>
                            <div>
                                <label for="endDate" class="block text-sm font-medium text-gray-700">End Date</label>
                                <input type="date" id="endDate" name="endDate" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                            </div>
                        </div>
                         <div>
                            <label for="reportDivision" class="block text-sm font-medium text-gray-700">Filter by Division</label>
                            <select id="reportDivision" name="reportDivision" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                                <option value="all">All Divisions</option>
                                <option value="Bacolod City">Bacolod City</option>
                                <option value="Bago City">Bago City</option>
                                <option value="Bais City">Bais City</option>
                                <option value="Bayawan City">Bayawan City</option>
                                <option value="Cadiz City">Cadiz City</option>
                                <option value="Canlaon City">Canlaon City</option>
                                <option value="Dumaguete City">Dumaguete City</option>
                                <option value="Escalante City">Escalante City</option>
                                <option value="Guihulngan City">Guihulngan City</option>
                                <option value="Himamaylan City">Himamaylan City</option>
                                <option value="Kabankalan City">Kabankalan City</option>
                                <option value="La Carlota City">La Carlota City</option>
                                <option value="Negros Occidental">Negros Occidental</option>
                                <option value="Negros Oriental">Negros Oriental</option>
                                <option value="Sagay City">Sagay City</option>
                                <option value="San Carlos City">San Carlos City</option>
                                <option value="Silay City">Silay City</option>
                                <option value="Sipalay City">Sipalay City</option>
                                <option value="Siquijor">Siquijor</option>
                                <option value="Tanjay City">Tanjay City</option>
                                <option value="Victorias City">Victorias City</option>
                            </select>
                        </div>
                        <div class="text-right">
                            <button type="submit" class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                                Generate Report
                            </button>
                        </div>
                    </form>
                    
                    <div id="reportOutput" class="mt-8 p-6 bg-gray-50 rounded-lg shadow-inner hidden">
                        <h4 class="text-lg font-semibold mb-4 text-gray-900">Generated Report</h4>
                        <div id="reportContent" class="prose max-w-none text-gray-700"></div>
                        <div class="flex justify-end mt-4">
                            <button onclick="printReport()" class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-gray-600 hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500">
                                Print Report
                            </button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- User Management Tab -->
            <div id="users" class="tab-content">
                <div class="card mb-8">
                    <h3 class="text-2xl font-semibold mb-6">User Management (Simple)</h3>
                    <p class="mb-4 text-gray-600">This is a simple user management for a local application. Data is not synchronized and is stored in your browser's local storage.</p>
                    <form id="addUserForm" class="space-y-4">
                        <div>
                            <label for="newUsername" class="block text-sm font-medium text-gray-700">New User Name</label>
                            <input type="text" id="newUsername" name="newUsername" required class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                        </div>
                        <div class="text-right">
                            <button type="submit" class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                                Add User
                            </button>
                        </div>
                    </form>
                </div>
                <div class="card">
                    <h3 class="text-2xl font-semibold mb-4">System Users</h3>
                    <ul id="userList" class="space-y-2">
                        <!-- User list will be dynamically added here -->
                    </ul>
                </div>
            </div>

        </main>
    </div>

    <!-- Modal for showing message/alert -->
    <div id="modal" class="hidden fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full z-50">
        <div class="relative top-20 mx-auto p-5 border w-96 shadow-lg rounded-md bg-white">
            <div class="mt-3 text-center">
                <h3 class="text-lg leading-6 font-medium text-gray-900" id="modal-title"></h3>
                <div class="mt-2 px-7 py-3">
                    <p class="text-sm text-gray-500" id="modal-message"></p>
                </div>
                <div class="items-center px-4 py-3">
                    <button id="modal-ok-button" class="px-4 py-2 bg-blue-500 text-white text-base font-medium rounded-md w-full shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500">OK</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Global data object
        let data = {
            users: [],
            complaints: []
        };
        let complaintsChart = null; // Variable to hold the chart instance

        // DOM elements
        const complaintsTableBody = document.getElementById('complaintsTableBody');
        const addComplaintForm = document.getElementById('addComplaintForm');
        const reportForm = document.getElementById('reportForm');
        const reportOutput = document.getElementById('reportOutput');
        const reportContent = document.getElementById('reportContent');
        const userList = document.getElementById('userList');
        const addUserForm = document.getElementById('addUserForm');
        const complaintSearch = document.getElementById('complaintSearch');
        const modal = document.getElementById('modal');
        const modalTitle = document.getElementById('modal-title');
        const modalMessage = document.getElementById('modal-message');
        const modalOkButton = document.getElementById('modal-ok-button');

        // Helper function to show custom modal
        function showModal(title, message) {
            modalTitle.textContent = title;
            modalMessage.textContent = message;
            modal.classList.remove('hidden');
        }

        // Event listener for modal OK button
        modalOkButton.addEventListener('click', () => {
            modal.classList.add('hidden');
        });

        // Function to load data from localStorage
        function loadData() {
            try {
                const storedData = localStorage.getItem('deped_inventory_system');
                if (storedData) {
                    data = JSON.parse(storedData);
                    console.log('Data loaded successfully.');
                }
            } catch (error) {
                console.error('Error loading data from localStorage:', error);
                showModal('Error', 'An error occurred while loading data from your browser storage. Some features may not work correctly.');
            }
        }

        // Function to save data to localStorage
        function saveData() {
            try {
                localStorage.setItem('deped_inventory_system', JSON.stringify(data));
                console.log('Data saved successfully.');
            } catch (error) {
                console.error('Error saving data to localStorage:', error);
                showModal('Error', 'An error occurred while saving data to your browser storage. Changes may not be saved.');
            }
        }

        // Function to render complaint table
        function renderComplaints(searchText = '') {
            complaintsTableBody.innerHTML = '';
            const normalizedSearchText = searchText.toLowerCase().trim();
            const sortedComplaints = data.complaints.sort((a, b) => new Date(b.dateFiled) - new Date(a.dateFiled));

            const filteredComplaints = sortedComplaints.filter(complaint => {
                const complainantName = complaint.complainant.toLowerCase();
                const respondentName = complaint.respondent.toLowerCase();
                return complainantName.includes(normalizedSearchText) || respondentName.includes(normalizedSearchText);
            });

            const complaintsToRender = normalizedSearchText ? filteredComplaints : sortedComplaints;

            complaintsToRender.forEach(complaint => {
                const row = document.createElement('tr');
                row.className = 'bg-white';
                const flagHtml = complaint.type === 'Administrative' ? 
                    `<span class="bg-red-100 text-red-800 text-xs font-semibold px-2 py-1 rounded-full">WITH ADMINISTRATIVE COMPLAINT</span>` : 
                    `<span>-</span>`;

                row.innerHTML = `
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${complaint.id}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.complainant}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.respondent}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.type}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.place}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.division || 'N/A'}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.dateFiled}</td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm">
                        <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${getStatusClass(complaint.status)}">${complaint.status}</span>
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-blue-600 hover:underline cursor-pointer" onclick="showFileReference('${complaint.attachment}')">
                        ${complaint.attachment || 'N/A'}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">
                        ${flagHtml}
                    </td>
                    <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                        <button onclick="editComplaint('${complaint.id}')" class="text-blue-600 hover:text-blue-900 mr-2">Edit</button>
                        <button onclick="deleteComplaint('${complaint.id}')" class="text-red-600 hover:text-red-900">Delete</button>
                    </td>
                `;
                complaintsTableBody.appendChild(row);
            });
            updateDashboard();
        }

        // Helper function for status colors
        function getStatusClass(status) {
            switch (status) {
                case 'Ongoing': return 'bg-yellow-100 text-yellow-800';
                case 'Resolved': return 'bg-green-100 text-green-800';
                case 'Cancelled': return 'bg-gray-100 text-gray-800';
                default: return 'bg-gray-100 text-gray-800';
            }
        }

        // Function to handle add complaint form submission
        addComplaintForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const formData = new FormData(e.target);
            const complaint = {
                id: Date.now().toString(), // Simple unique ID
                complainant: formData.get('complainant'),
                respondent: formData.get('respondent'),
                type: formData.get('complaintType'),
                place: formData.get('place'),
                division: formData.get('division'),
                details: formData.get('details'),
                status: formData.get('status'),
                dateFiled: new Date().toISOString().slice(0, 10),
                attachment: formData.get('attachment')
            };
            data.complaints.push(complaint);
            saveData();
            renderComplaints();
            e.target.reset();
            showModal('Success', 'Complaint added successfully.');
        });

        // Function to edit complaint status
        function editComplaint(id) {
            const complaint = data.complaints.find(c => c.id === id);
            if (complaint) {
                const newStatus = prompt(`Current status for ${complaint.complainant} vs ${complaint.respondent} is "${complaint.status}". Enter new status (Ongoing, Resolved, Cancelled):`);
                if (newStatus && ['Ongoing', 'Resolved', 'Cancelled'].includes(newStatus)) {
                    complaint.status = newStatus;
                    saveData();
                    renderComplaints();
                } else if (newStatus !== null) {
                    showModal('Invalid Status', 'Please enter a valid status: Ongoing, Resolved, or Cancelled.');
                }
            }
        }

        // Function to delete complaint
        function deleteComplaint(id) {
            if (confirm('Are you sure you want to delete this complaint?')) {
                data.complaints = data.complaints.filter(c => c.id !== id);
                saveData();
                renderComplaints();
                showModal('Deleted', 'Complaint deleted successfully.');
            }
        }

        // Function to show file reference details
        function showFileReference(filename) {
            if (filename) {
                showModal('File Reference', `This system tracks the reference "${filename}". To view the file, please open it manually from your computer.`);
            } else {
                showModal('No File Reference', 'No file reference was provided for this complaint.');
            }
        }

        // Function to update dashboard counts
        function updateDashboard() {
            document.getElementById('totalComplaintsCount').innerHTML = `<span>${data.complaints.length}</span> <span>⚖️</span>`;
            document.getElementById('ongoingComplaintsCount').innerHTML = `<span>${data.complaints.filter(c => c.status === 'Ongoing').length}</span> <span>⏰</span>`;
            document.getElementById('resolvedComplaintsCount').innerHTML = `<span>${data.complaints.filter(c => c.status === 'Resolved').length}</span> <span>✅</span>`;
            document.getElementById('cancelledComplaintsCount').innerHTML = `<span>${data.complaints.filter(c => c.status === 'Cancelled').length}</span> <span>❌</span>`;
        }
        
        // Function to render the complaints chart categorized by type
        function renderComplaintsChart() {
            const complaintTypes = ['Administrative', 'School Site Issues', 'Local Complaints', 'Change of School Records', 'Child/Sexual Abuse'];
            const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
            const typeColors = {
                'Administrative': '#EF4444', // Red-500
                'School Site Issues': '#3B82F6', // Blue-500
                'Local Complaints': '#22C55E', // Green-500
                'Change of School Records': '#F59E0B', // Amber-500
                'Child/Sexual Abuse': '#8B5CF6' // Purple-500
            };

            const monthlyData = {};
            months.forEach(month => {
                monthlyData[month] = {};
                complaintTypes.forEach(type => {
                    monthlyData[month][type] = 0;
                });
            });

            data.complaints.forEach(complaint => {
                if (complaint.dateFiled) {
                    const monthIndex = new Date(complaint.dateFiled).getMonth();
                    const monthName = months[monthIndex];
                    if (monthlyData[monthName] && monthlyData[monthName][complaint.type] !== undefined) {
                        monthlyData[monthName][complaint.type]++;
                    }
                }
            });

            const datasets = complaintTypes.map(type => {
                return {
                    label: type,
                    data: months.map(month => monthlyData[month][type]),
                    backgroundColor: typeColors[type],
                    borderColor: typeColors[type],
                    borderWidth: 1
                };
            });

            const chartConfig = {
                type: 'bar',
                data: {
                    labels: months,
                    datasets: datasets
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        x: {
                            stacked: true,
                        },
                        y: {
                            stacked: true,
                            beginAtZero: true
                        }
                    },
                    plugins: {
                        title: {
                            display: true,
                            text: 'Number of Complaints per Month by Type'
                        }
                    }
                }
            };

            const ctx = document.getElementById('complaintsChart').getContext('2d');
            
            // Destroy existing chart if it exists to prevent duplicates
            if (complaintsChart) {
                complaintsChart.destroy();
            }

            complaintsChart = new Chart(ctx, chartConfig);
        }

        // Function to handle report generation
        reportForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const formData = new FormData(e.target);
            const statusFilter = formData.get('reportStatus');
            const divisionFilter = formData.get('reportDivision');
            const startDate = formData.get('startDate');
            const endDate = formData.get('endDate');

            let filteredComplaints = data.complaints;

            if (statusFilter !== 'all') {
                filteredComplaints = filteredComplaints.filter(c => c.status === statusFilter);
            }

            if (divisionFilter !== 'all') {
                filteredComplaints = filteredComplaints.filter(c => c.division === divisionFilter);
            }

            if (startDate) {
                filteredComplaints = filteredComplaints.filter(c => new Date(c.dateFiled) >= new Date(startDate));
            }
            if (endDate) {
                filteredComplaints = filteredComplaints.filter(c => new Date(c.dateFiled) <= new Date(endDate));
            }

            let reportHtml = `
                <p class="font-bold">Report Filters:</p>
                <ul>
                    <li><strong>Status:</strong> ${statusFilter === 'all' ? 'All' : statusFilter}</li>
                    <li><strong>Division:</strong> ${divisionFilter === 'all' ? 'All Divisions' : divisionFilter}</li>
                    <li><strong>Date Range:</strong> ${startDate || 'N/A'} to ${endDate || 'N/A'}</li>
                </ul>
                <h5 class="mt-4 font-bold text-lg">Summary</h5>
                <p>Total Complaints Found: ${filteredComplaints.length}</p>
                <h5 class="mt-4 font-bold text-lg">Details</h5>
                <table class="w-full mt-2 text-sm">
                    <thead>
                        <tr>
                            <th class="border px-4 py-2 text-left">ID</th>
                            <th class="border px-4 py-2 text-left">Complainant</th>
                            <th class="border px-4 py-2 text-left">Respondent</th>
                            <th class="border px-4 py-2 text-left">Type</th>
                            <th class="border px-4 py-2 text-left">Division</th>
                            <th class="border px-4 py-2 text-left">Status</th>
                            <th class="border px-4 py-2 text-left">Date Filed</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${filteredComplaints.map(c => `
                            <tr>
                                <td class="border px-4 py-2">${c.id}</td>
                                <td class="border px-4 py-2">${c.complainant}</td>
                                <td class="border px-4 py-2">${c.respondent}</td>
                                <td class="border px-4 py-2">${c.type}</td>
                                <td class="border px-4 py-2">${c.division || 'N/A'}</td>
                                <td class="border px-4 py-2">${c.status}</td>
                                <td class="border px-4 py-2">${c.dateFiled}</td>
                            </tr>
                        `).join('')}
                    </tbody>
                </table>
            `;

            reportContent.innerHTML = reportHtml;
            reportOutput.classList.remove('hidden');
        });

        // Function to print the report
        function printReport() {
            const printContents = document.getElementById('reportOutput').innerHTML;
            const originalContents = document.body.innerHTML;
            document.body.innerHTML = `<div class="p-8">${printContents}</div>`;
            window.print();
            document.body.innerHTML = originalContents;
            window.location.reload(); // Reload to restore event listeners
        }

        // Function to render user list
        function renderUsers() {
            userList.innerHTML = '';
            if (data.users.length === 0) {
                const emptyItem = document.createElement('li');
                emptyItem.className = 'text-gray-500';
                emptyItem.textContent = 'No users added yet.';
                userList.appendChild(emptyItem);
            } else {
                data.users.forEach(user => {
                    const listItem = document.createElement('li');
                    listItem.className = 'flex items-center justify-between bg-white rounded-md p-3 shadow-sm';
                    listItem.innerHTML = `
                        <span class="text-gray-800">${user.name}</span>
                        <button onclick="deleteUser('${user.id}')" class="text-red-500 hover:text-red-700 ml-4 focus:outline-none">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd" />
                            </svg>
                        </button>
                    `;
                    userList.appendChild(listItem);
                });
            }
        }

        // Function to handle add user form submission
        addUserForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const newUsername = document.getElementById('newUsername').value;
            if (newUsername) {
                const newUser = {
                    id: Date.now().toString(),
                    name: newUsername
                };
                data.users.push(newUser);
                saveData();
                renderUsers();
                e.target.reset();
                showModal('Success', 'User added successfully.');
            }
        });

        // Function to delete user
        function deleteUser(id) {
            if (confirm('Are you sure you want to delete this user?')) {
                data.users = data.users.filter(u => u.id !== id);
                saveData();
                renderUsers();
                showModal('Deleted', 'User deleted successfully.');
            }
        }

        // Tab switching logic
        function showTab(tabId) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));
            document.getElementById(tabId).classList.add('active');
            document.querySelector(`.tab-button[onclick="showTab('${tabId}')"]`).classList.add('active');
            
            // Render chart only when the reports tab is active
            if (tabId === 'reports') {
                renderComplaintsChart();
            }
        }

        // Add search event listener
        complaintSearch.addEventListener('input', (e) => {
            const searchText = e.target.value;
            renderComplaints(searchText);
        });

        // Initialize the app on page load
        loadData();
        renderComplaints();
        renderUsers();
        showTab('dashboard'); // Default tab on load

        // Add a global confirm function to avoid alert()
        window.confirm = (message) => {
          return new Promise((resolve) => {
            const modal = document.getElementById('modal');
            const modalTitle = document.getElementById('modal-title');
            const modalMessage = document.getElementById('modal-message');
            const modalOkButton = document.getElementById('modal-ok-button');
            const modalCancelButton = document.createElement('button');

            // Setup
            modalTitle.textContent = 'Confirmation';
            modalMessage.textContent = message;
            modalOkButton.textContent = 'OK';
            modalOkButton.classList.remove('w-full');
            modalOkButton.classList.add('w-1/2', 'mr-2');

            modalCancelButton.textContent = 'Cancel';
            modalCancelButton.className = 'px-4 py-2 bg-gray-500 text-white text-base font-medium rounded-md w-1/2 shadow-sm hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-gray-500';

            modalOkButton.parentNode.appendChild(modalCancelButton);

            modal.classList.remove('hidden');

            // Listeners
            modalOkButton.onclick = () => {
              modal.classList.add('hidden');
              modalCancelButton.remove();
              modalOkButton.classList.remove('w-1/2', 'mr-2');
              modalOkButton.classList.add('w-full');
              resolve(true);
            };
            modalCancelButton.onclick = () => {
              modal.classList.add('hidden');
              modalCancelButton.remove();
              modalOkButton.classList.remove('w-1/2', 'mr-2');
              modalOkButton.classList.add('w-full');
              resolve(false);
            };
          });
        };

        // Expose functions to the global scope for onclick attributes
        window.showTab = showTab;
        window.editComplaint = editComplaint;
        window.deleteComplaint = deleteComplaint;
        window.showFileReference = showFileReference;
        window.printReport = printReport;
        window.deleteUser = deleteUser;

    </script>
</body>
</html>
