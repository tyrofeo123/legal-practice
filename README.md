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
        .modal-content {
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-800">

    <div class="container py-8">
        <!-- Header -->
        <header class="text-center mb-8">
            <div class="flex flex-col sm:flex-row items-center justify-between">
                <img src="C:\Users\TyronVincentTrofeo\Downloads\deped logo.jpg">
                <div class="text-center flex-grow mt-4 sm:mt-0">
                    <h1 class="text-2xl sm:text-3xl font-bold text-gray-900 mb-2">DEPARTMENT OF EDUCATION NEGROS ISLAND REGION</h1>
                    <h2 class="text-lg sm:text-xl font-medium text-blue-800">Office of the Regional Director - Legal Unit</h2>
                </div>
                <img src="C:\Users\TyronVincentTrofeo\Downloads\NIR logo.jpg">
            </div>
        </header>

        <!-- Tabs Navigation -->
        <nav class="bg-white rounded-lg p-2 mb-8 shadow-sm">
            <div class="flex flex-col sm:flex-row space-y-2 sm:space-y-0 sm:space-x-4">
                <button class="tab-button active flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('dashboard')">🏠 Dashboard</button>
                <button class="tab-button flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('complaints')">📝 Complaint Management</button>
                <button class="tab-button flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('reports')">📊 Reports</button>
                <button class="tab-button flex-1 py-3 px-4 text-center rounded-lg transition-colors duration-200 hover:bg-gray-50 focus:outline-none" onclick="showTab('users')">⚙️ Account</button>
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
                                <option value="8888 Citizens' Complaint Hotline/DPAC">8888 Citizens' Complaint Hotline/DPAC</option>
                                <option value="Formal Investigation">Formal Investigation</option>
                                <option value="Preliminary Investigation">Preliminary Investigation</option>
                                <option value="School Site Issues">School Site Issues</option>
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
                <div class="card">
                    <h3 class="text-2xl font-semibold mb-6">User Account Information</h3>
                    <p class="mb-4 text-gray-600">This app is designed for multiple users to collaborate. Your unique user ID is displayed below.</p>
                    <div class="bg-gray-50 p-6 rounded-lg shadow-inner">
                        <p class="text-sm font-medium text-gray-700 mb-2">User ID:</p>
                        <p id="userIdDisplay" class="font-mono text-sm text-blue-700 break-all"></p>
                    </div>

                    <div class="mt-8">
                        <h4 class="text-xl font-semibold mb-4">Set Your Display Name</h4>
                        <p class="text-sm text-gray-600 mb-4">Choose a name that will be displayed in the system for easier identification, like "Admin_Main" or your full name.</p>
                        <div class="space-y-4">
                            <div>
                                <label for="displayNameInput" class="block text-sm font-medium text-gray-700">Display Name</label>
                                <input type="text" id="displayNameInput" placeholder="e.g., Admin_Main" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                            </div>
                            <div class="text-right">
                                <button id="saveDisplayNameButton" class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                                    Save Display Name
                                </button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

        </main>
    </div>

    <!-- General Modal for messages -->
    <div id="modal" class="hidden fixed inset-0 z-50 overflow-y-auto bg-gray-600 bg-opacity-50">
        <div class="relative w-96 p-5 mx-auto bg-white rounded-md shadow-lg modal-content">
            <div class="mt-3 text-center">
                <h3 class="text-lg font-medium leading-6 text-gray-900" id="modal-title"></h3>
                <div class="mt-2 px-7 py-3">
                    <p class="text-sm text-gray-500" id="modal-message"></p>
                </div>
                <div class="items-center px-4 py-3">
                    <button id="modal-ok-button" class="px-4 py-2 text-base font-medium text-white bg-blue-500 rounded-md w-full shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500">OK</button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal for editing status -->
    <div id="editStatusModal" class="hidden fixed inset-0 z-50 overflow-y-auto bg-gray-600 bg-opacity-50">
        <div class="relative w-96 p-5 mx-auto bg-white rounded-md shadow-lg modal-content">
            <div class="mt-3 text-center">
                <h3 class="text-lg font-medium leading-6 text-gray-900" id="edit-modal-title">Edit Complaint Status</h3>
                <div class="mt-2 px-7 py-3">
                    <p class="text-sm text-gray-500 mb-4" id="edit-modal-message"></p>
                    <label for="newStatusSelect" class="block text-sm font-medium text-gray-700">Select New Status</label>
                    <select id="newStatusSelect" class="mt-1 block w-full rounded-md border-gray-300 shadow-sm focus:border-blue-500 focus:ring-blue-500">
                        <option value="Ongoing">Ongoing</option>
                        <option value="Resolved">Resolved</option>
                        <option value="Cancelled">Cancelled</option>
                    </select>
                </div>
                <div class="items-center px-4 py-3">
                    <button id="edit-modal-save-button" class="px-4 py-2 text-base font-medium text-white bg-blue-500 rounded-md w-full shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">Save</button>
                    <button id="edit-modal-cancel-button" class="mt-2 px-4 py-2 text-base font-medium text-gray-700 bg-gray-200 rounded-md w-full shadow-sm hover:bg-gray-300 focus:outline-none focus:ring-2 focus:ring-gray-400">Cancel</button>
                </div>
            </div>
        </div>
    </div>

    <script type="module">
        import { initializeApp } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-app.js";
        import { getAuth, signInWithCustomToken, signInAnonymously, onAuthStateChanged } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-auth.js";
        import { getFirestore, collection, doc, addDoc, updateDoc, deleteDoc, onSnapshot, setDoc } from "https://www.gstatic.com/firebasejs/11.6.1/firebase-firestore.js";

        // Global data and Firebase variables
        let complaints = [];
        let complaintsChart = null;
        let unsubscribeFromComplaints = null;
        let unsubscribeFromProfile = null;
        let userId = null;
        let displayName = null;

        // Firebase Initialization
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';
        const firebaseConfig = typeof __firebase_config !== 'undefined' ? JSON.parse(__firebase_config) : {};
        const initialAuthToken = typeof __initial_auth_token !== 'undefined' ? __initial_auth_token : null;

        // DOM elements
        const complaintsTableBody = document.getElementById('complaintsTableBody');
        const addComplaintForm = document.getElementById('addComplaintForm');
        const reportForm = document.getElementById('reportForm');
        const reportOutput = document.getElementById('reportOutput');
        const reportContent = document.getElementById('reportContent');
        const complaintSearch = document.getElementById('complaintSearch');
        const userIdDisplay = document.getElementById('userIdDisplay');
        const displayNameInput = document.getElementById('displayNameInput');
        const saveDisplayNameButton = document.getElementById('saveDisplayNameButton');

        // Modal elements
        const modal = document.getElementById('modal');
        const modalTitle = document.getElementById('modal-title');
        const modalMessage = document.getElementById('modal-message');
        const modalOkButton = document.getElementById('modal-ok-button');

        // Edit status modal elements
        const editStatusModal = document.getElementById('editStatusModal');
        const editModalMessage = document.getElementById('edit-modal-message');
        const newStatusSelect = document.getElementById('newStatusSelect');
        const editModalSaveButton = document.getElementById('edit-modal-save-button');
        const editModalCancelButton = document.getElementById('edit-modal-cancel-button');

        // Helper function to show custom message modal
        function showModal(title, message) {
            modalTitle.textContent = title;
            modalMessage.textContent = message;
            modal.classList.remove('hidden');
        }

        // Helper function to show a confirm modal
        function showConfirmModal(title, message, onConfirm) {
            modalTitle.textContent = title;
            modalMessage.textContent = message;
            modal.classList.remove('hidden');
            modalOkButton.textContent = 'Yes';
            const oldListener = modalOkButton.onclick;
            modalOkButton.onclick = () => {
                modal.classList.add('hidden');
                onConfirm();
                modalOkButton.textContent = 'OK';
                modalOkButton.onclick = oldListener;
            };
        }

        // Helper function to show a modal for editing status
        function showEditStatusModal(complaintId, currentStatus, onSave) {
            editModalMessage.textContent = `Current status is: ${currentStatus}`;
            newStatusSelect.value = currentStatus;
            editStatusModal.classList.remove('hidden');

            const saveHandler = () => {
                const newStatus = newStatusSelect.value;
                onSave(complaintId, newStatus);
                editStatusModal.classList.add('hidden');
                editModalSaveButton.removeEventListener('click', saveHandler);
                editModalCancelButton.removeEventListener('click', cancelHandler);
            };

            const cancelHandler = () => {
                editStatusModal.classList.add('hidden');
                editModalSaveButton.removeEventListener('click', saveHandler);
                editModalCancelButton.removeEventListener('click', cancelHandler);
            };

            editModalSaveButton.addEventListener('click', saveHandler);
            editModalCancelButton.addEventListener('click', cancelHandler);
        }

        // Event listener for general modal OK button
        modalOkButton.addEventListener('click', () => {
            modal.classList.add('hidden');
        });

        // Function to get status class for styling
        function getStatusClass(status) {
            switch (status) {
                case 'Ongoing': return 'bg-yellow-100 text-yellow-800';
                case 'Resolved': return 'bg-green-100 text-green-800';
                case 'Cancelled': return 'bg-gray-100 text-gray-800';
                default: return 'bg-gray-100 text-gray-800';
            }
        }

        // Render functions
        function renderComplaints(searchText = '') {
            complaintsTableBody.innerHTML = '';
            const normalizedSearchText = searchText.toLowerCase().trim();
            const sortedComplaints = [...complaints].sort((a, b) => new Date(b.dateFiled) - new Date(a.dateFiled));

            const filteredComplaints = sortedComplaints.filter(complaint => {
                const complainantName = (complaint.complainant || '').toLowerCase();
                const respondentName = (complaint.respondent || '').toLowerCase();
                return complainantName.includes(normalizedSearchText) || respondentName.includes(normalizedSearchText);
            });

            const complaintsToRender = normalizedSearchText ? filteredComplaints : sortedComplaints;

            if (complaintsToRender.length === 0) {
                const noDataRow = document.createElement('tr');
                noDataRow.innerHTML = `<td colspan="10" class="px-6 py-4 text-center text-gray-500">No complaints found.</td>`;
                complaintsTableBody.appendChild(noDataRow);
            } else {
                complaintsToRender.forEach(complaint => {
                    const row = document.createElement('tr');
                    row.className = 'bg-white';

                    row.innerHTML = `
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900">${complaint.id}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.complainant || 'N/A'}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.respondent || 'N/A'}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.type || 'N/A'}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.place || 'N/A'}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.division || 'N/A'}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-gray-500">${complaint.dateFiled || 'N/A'}</td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm">
                            <span class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full ${getStatusClass(complaint.status)}">${complaint.status || 'N/A'}</span>
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm text-blue-600 hover:underline cursor-pointer" onclick="showFileReference('${complaint.attachment || 'N/A'}')">
                            ${complaint.attachment || 'N/A'}
                        </td>
                        <td class="px-6 py-4 whitespace-nowrap text-sm font-medium">
                            <button onclick="editComplaint('${complaint.id}')" class="text-blue-600 hover:text-blue-900 mr-2">Edit</button>
                            <button onclick="deleteComplaint('${complaint.id}')" class="text-red-600 hover:text-red-900">Delete</button>
                        </td>
                    `;
                    complaintsTableBody.appendChild(row);
                });
            }
            updateDashboard();
        }

        function updateDashboard() {
            const total = complaints.length;
            const ongoing = complaints.filter(c => c.status === 'Ongoing').length;
            const resolved = complaints.filter(c => c.status === 'Resolved').length;
            const cancelled = complaints.filter(c => c.status === 'Cancelled').length;

            document.getElementById('totalComplaintsCount').innerHTML = `<span>${total}</span> <span>⚖️</span>`;
            document.getElementById('ongoingComplaintsCount').innerHTML = `<span>${ongoing}</span> <span>⏰</span>`;
            document.getElementById('resolvedComplaintsCount').innerHTML = `<span>${resolved}</span> <span>✅</span>`;
            document.getElementById('cancelledComplaintsCount').innerHTML = `<span>${cancelled}</span> <span>❌</span>`;

            updateChart();
        }

        // Chart.js functions
        function updateChart() {
            const complaintsByMonthAndType = complaints.reduce((acc, complaint) => {
                const month = complaint.dateFiled.slice(0, 7);
                if (!acc[month]) {
                    acc[month] = {};
                }
                const type = complaint.type;
                if (!acc[month][type]) {
                    acc[month][type] = 0;
                }
                acc[month][type]++;
                return acc;
            }, {});

            const months = Object.keys(complaintsByMonthAndType).sort();
            const types = [...new Set(complaints.map(c => c.type))];

            const datasets = types.map(type => {
                const data = months.map(month => complaintsByMonthAndType[month][type] || 0);
                return {
                    label: type,
                    data: data,
                    backgroundColor: `rgba(${Math.random() * 255}, ${Math.random() * 255}, ${Math.random() * 255}, 0.5)`,
                    borderColor: `rgba(${Math.random() * 255}, ${Math.random() * 255}, ${Math.random() * 255}, 1)`,
                    borderWidth: 1
                };
            });

            const chartData = {
                labels: months,
                datasets: datasets
            };

            if (complaintsChart) {
                complaintsChart.data = chartData;
                complaintsChart.update();
            } else {
                const ctx = document.getElementById('complaintsChart').getContext('2d');
                complaintsChart = new Chart(ctx, {
                    type: 'bar',
                    data: chartData,
                    options: {
                        responsive: true,
                        maintainAspectRatio: false,
                        scales: {
                            y: {
                                beginAtZero: true
                            }
                        }
                    }
                });
            }
        }

        // Firestore Real-time Listener
        function setupFirestoreListeners() {
            const complaintsCollection = collection(db, `artifacts/${appId}/public/data/complaints`);
            unsubscribeFromComplaints = onSnapshot(complaintsCollection, (snapshot) => {
                const updatedComplaints = [];
                snapshot.forEach((doc) => {
                    updatedComplaints.push({ id: doc.id, ...doc.data() });
                });
                complaints = updatedComplaints;
                renderComplaints();
                console.log("Complaints data updated from Firestore.");
            }, (error) => {
                console.error("Error listening to complaints:", error);
                showModal('Error', 'Failed to load complaints data. Please check your network connection.');
            });
        }

        function setupProfileListener(uid) {
            const profileDocRef = doc(db, `artifacts/${appId}/users/${uid}/profile/main`);
            unsubscribeFromProfile = onSnapshot(profileDocRef, (docSnap) => {
                if (docSnap.exists()) {
                    displayName = docSnap.data().displayName;
                    displayNameInput.value = displayName;
                } else {
                    displayName = null;
                    displayNameInput.value = '';
                }
                updateUserIdDisplay();
            }, (error) => {
                console.error("Error listening to profile:", error);
            });
        }

        function updateUserIdDisplay() {
            if (displayName) {
                userIdDisplay.textContent = `${displayName} (ID: ${userId})`;
            } else {
                userIdDisplay.textContent = userId;
            }
        }

        // Functions for button actions
        window.showTab = function(tabName) {
            document.querySelectorAll('.tab-content').forEach(tab => tab.classList.remove('active'));
            document.getElementById(tabName).classList.add('active');
            document.querySelectorAll('.tab-button').forEach(btn => btn.classList.remove('active'));
            document.querySelector(`.tab-button[onclick="showTab('${tabName}')"]`).classList.add('active');

            if (tabName === 'reports' && complaintsChart === null) {
                updateChart();
            }
        };

        window.showFileReference = function(ref) {
            showModal('File Reference', ref);
        };

        window.editComplaint = function(id) {
            const complaint = complaints.find(c => c.id === id);
            if (complaint) {
                showEditStatusModal(id, complaint.status, async (complaintId, newStatus) => {
                    try {
                        await updateDoc(doc(db, `artifacts/${appId}/public/data/complaints`, complaintId), {
                            status: newStatus
                        });
                        showModal('Success', 'Complaint status updated successfully.');
                    } catch (error) {
                        console.error('Error updating document:', error);
                        showModal('Error', 'An error occurred while updating the complaint status. Please try again.');
                    }
                });
            }
        };

        window.deleteComplaint = function(id) {
            showConfirmModal('Confirm Deletion', 'Are you sure you want to delete this complaint? This action cannot be undone.', async () => {
                try {
                    await deleteDoc(doc(db, `artifacts/${appId}/public/data/complaints`, id));
                    showModal('Success', 'Complaint deleted successfully.');
                } catch (error) {
                    console.error('Error deleting document:', error);
                    showModal('Error', 'An error occurred while deleting the complaint. Please try again.');
                }
            });
        };

        window.printReport = function() {
            const reportContentHtml = document.getElementById('reportContent').innerHTML;
            const printWindow = window.open('', '', 'height=600,width=800');
            printWindow.document.write('<html><head><title>Complaint Report</title>');
            printWindow.document.write('</head><body>');
            printWindow.document.write(reportContentHtml);
            printWindow.document.close();
            printWindow.print();
        };

        // Event listeners
        addComplaintForm.addEventListener('submit', async (e) => {
            e.preventDefault();
            const formData = new FormData(e.target);
            const complaint = {
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

            try {
                const complaintsCollectionRef = collection(db, `artifacts/${appId}/public/data/complaints`);
                await addDoc(complaintsCollectionRef, complaint);
                e.target.reset();
                showModal('Success', 'Complaint added successfully.');
            } catch (error) {
                console.error('Error adding document:', error);
                showModal('Error', 'An error occurred while adding the complaint. Please try again.');
            }
        });

        reportForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const reportStatus = document.getElementById('reportStatus').value;
            const startDate = document.getElementById('startDate').value;
            const endDate = document.getElementById('endDate').value;
            const reportDivision = document.getElementById('reportDivision').value;

            let filteredComplaints = [...complaints];

            if (reportStatus !== 'all') {
                filteredComplaints = filteredComplaints.filter(c => c.status === reportStatus);
            }
            if (reportDivision !== 'all') {
                filteredComplaints = filteredComplaints.filter(c => c.division === reportDivision);
            }
            if (startDate) {
                filteredComplaints = filteredComplaints.filter(c => c.dateFiled >= startDate);
            }
            if (endDate) {
                filteredComplaints = filteredComplaints.filter(c => c.dateFiled <= endDate);
            }

            const reportHtml = `
                <h2 class="text-xl font-bold mb-4">Complaint Report</h2>
                <p><strong>Status Filter:</strong> ${reportStatus}</p>
                <p><strong>Division Filter:</strong> ${reportDivision}</p>
                <p><strong>Date Range:</strong> ${startDate || 'N/A'} to ${endDate || 'N/A'}</p>
                <p><strong>Total Complaints:</strong> ${filteredComplaints.length}</p>
                <table class="w-full mt-4 border-collapse">
                    <thead>
                        <tr>
                            <th class="border px-4 py-2 text-left">Complainant</th>
                            <th class="border px-4 py-2 text-left">Respondent</th>
                            <th class="border px-4 py-2 text-left">Type</th>
                            <th class="border px-4 py-2 text-left">Division</th>
                            <th class="border px-4 py-2 text-left">Date Filed</th>
                            <th class="border px-4 py-2 text-left">Status</th>
                        </tr>
                    </thead>
                    <tbody>
                        ${filteredComplaints.map(c => `
                            <tr>
                                <td class="border px-4 py-2">${c.complainant}</td>
                                <td class="border px-4 py-2">${c.respondent}</td>
                                <td class="border px-4 py-2">${c.type}</td>
                                <td class="border px-4 py-2">${c.division}</td>
                                <td class="border px-4 py-2">${c.dateFiled}</td>
                                <td class="border px-4 py-2">${c.status}</td>
                            </tr>
                        `).join('')}
                    </tbody>
                </table>
            `;
            reportContent.innerHTML = reportHtml;
            reportOutput.classList.remove('hidden');
        });

        complaintSearch.addEventListener('input', (e) => {
            renderComplaints(e.target.value);
        });
        
        saveDisplayNameButton.addEventListener('click', async () => {
            if (!userId) {
                showModal('Error', 'User not authenticated. Please wait and try again.');
                return;
            }
            const newDisplayName = displayNameInput.value.trim();
            if (!newDisplayName) {
                showModal('Error', 'Display name cannot be empty.');
                return;
            }
            try {
                const profileDocRef = doc(db, `artifacts/${appId}/users/${userId}/profile/main`);
                await setDoc(profileDocRef, { displayName: newDisplayName }, { merge: true });
                showModal('Success', 'Display name saved successfully.');
            } catch (error) {
                console.error("Error saving display name:", error);
                showModal('Error', 'Failed to save display name. Please try again.');
            }
        });

        // Initialize App
        const app = initializeApp(firebaseConfig);
        const db = getFirestore(app);
        const auth = getAuth(app);

        window.onload = function() {
            onAuthStateChanged(auth, async (user) => {
                if (user) {
                    userId = user.uid;
                    console.log("Authenticated as:", userId);

                    // Unsubscribe from previous listeners if they exist
                    if (unsubscribeFromComplaints) {
                        unsubscribeFromComplaints();
                    }
                    if (unsubscribeFromProfile) {
                        unsubscribeFromProfile();
                    }

                    setupFirestoreListeners();
                    setupProfileListener(userId);
                } else {
                    console.log("Not authenticated, signing in anonymously...");
                    try {
                        await signInAnonymously(auth);
                    } catch (error) {
                        console.error("Anonymous sign-in failed:", error);
                        showModal('Authentication Error', 'Failed to sign in. Please try again later.');
                    }
                }
            });
            showTab('dashboard');
        };

    </script>
</body>
</html>
