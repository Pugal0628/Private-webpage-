<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>College Student Information</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #e2f7e9;
            color: #2c3e50;
        }

        header {
               background-color: #1abc9c;
            color: white;
            padding: 20px 0;
            text-align: center;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }

        h1, h2 {
            margin: 0;
            padding: 10px;
        }

        .search-container {
            text-align: center;
            margin: 40px 0;
        }

        .search-container input {
            width: 60%;
            padding: 12px;
            font-size: 16px;
            border: 1px solid #7f8c8d;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .search-container button {
            padding: 12px 20px;
            font-size: 16px;
            background-color: #9b59b6;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            margin-left: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .search-container button:hover {
            background-color: #8e44ad;
        }

        .departments, .years {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            margin-top: 40px;
        }

        .department, .year {
            background-color: #f39c12;
            color: white;
            padding: 25px;
            margin: 12px;
            border-radius: 10px;
            cursor: pointer;
            text-align: center;
            width: 220px;
            transition: background-color 0.3s ease;
        }

        .department:hover, .year:hover {
            background-color: #f1c40f;
        }

        .student-details {
            margin: 20px auto;
            max-width: 800px;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
            display: none;
        }

        .student-details table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        th, td {
            border: 1px solid #bdc3c7;
            padding: 12px;
            text-align: center;
        }

        th {
            background-color: #9b59b6;
            color: white;
        }

        .back-button {
            display: block;
            text-align: center;
            margin: 30px auto;
            padding: 12px 25px;
            background-color: #9b59b6;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }

        .back-button:hover {
            background-color: #8e44ad;
        }

        footer {
            background-color: #34495e;
            color: white;
            padding: 15px 0;
            text-align: center;
            position: fixed;
            width: 100%;
            bottom: 0;
        }
    </style>
</head>
<body>
    <header>
        <h1>College Student Information</h1>
    </header>

    <!-- Main Search Section -->
    <div class="search-container" id="searchContainer">
        <input type="text" id="searchBox" placeholder="Search for a student..." />
        <button onclick="searchStudent()">Search</button>
    </div>

    <!-- Department Section -->
    <div class="departments" id="departmentSection">
        <div class="department" onclick="showYears()">B.Com CA</div>
    </div>

    <!-- Year Selection Section -->
    <div class="years" id="yearSection" style="display: none;">
        <button class="back-button" onclick="goBackToDepartments()">Back to Departments</button>
        <div class="year" onclick="showStudents('1st Year')">1st Year</div>
        <div class="year" onclick="showStudents('2nd Year')">2nd Year</div>
        <div class="year" onclick="showStudents('3rd Year')">3rd Year</div>
    </div>

    <!-- Student Details Section -->
    <div class="student-details" id="studentDetails">
        <h2 id="studentTitle"></h2>
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Register Number</th>
                    <th>University Number</th>
                    <th>Date of Birth</th>
                    <th>Which Year</th>
                </tr>
            </thead>
            <tbody id="studentTableBody"></tbody>
        </table>
        <button class="back-button" onclick="goBackToYears()">Back to Years</button>
    </div>

    <footer>
        <p>THIS PAGE IS CREATED BY PUGAL</p>
    </footer>

    <script>
        // Sample data for students
        const studentsData = {
            '1st Year': [
                { name: 'John Doe', regNo: 'BC101', uniNo: 'U101', dob: '2005-01-15', year: '1st Year' },
                { name: 'Jane Smith', regNo: 'BC102', uniNo: 'U102', dob: '2005-05-22', year: '1st Year' }
            ],
            '2nd Year': [
                { name: 'Alice Brown', regNo: 'BC201', uniNo: 'U201', dob: '2004-03-11', year: '2nd Year' },
                { name: 'Bob White', regNo: 'BC202', uniNo: 'U202', dob: '2004-07-09', year: '2nd Year' }
            ],
            '3rd Year': [
                { name: 'Charlie Green', regNo: 'BC301', uniNo: 'U301', dob: '2003-02-19', year: '3rd Year' },
                { name: 'Diana Black', regNo: 'BC302', uniNo: 'U302', dob: '2003-11-29', year: '3rd Year' }
            ]
        };

        // Show Year Section
        function showYears() {
            document.getElementById('departmentSection').style.display = 'none';
            document.getElementById('yearSection').style.display = 'flex';
        }

        // Show Students of a Selected Year
        function showStudents(year) {
            const studentDetails = document.getElementById('studentDetails');
            const studentTitle = document.getElementById('studentTitle');
            const studentTableBody = document.getElementById('studentTableBody');

            studentTitle.innerText = `B.Com CA - ${year}`;
            studentTableBody.innerHTML = '';

            studentsData[year].forEach(student => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td>${student.name}</td>
                    <td>${student.regNo}</td>
                    <td>${student.uniNo}</td>
                    <td>${student.dob}</td>
                    <td>${student.year}</td>
                `;
                studentTableBody.appendChild(row);
            });

            document.getElementById('yearSection').style.display = 'none';
            studentDetails.style.display = 'block';
        }

        // Go Back to Years Section
        function goBackToYears() {
            document.getElementById('studentDetails').style.display = 'none';
            document.getElementById('yearSection').style.display = 'flex';
        }

        // Go Back to Departments Section
        function goBackToDepartments() {
            document.getElementById('yearSection').style.display = 'none';
            document.getElementById('departmentSection').style.display = 'flex';
        }

        // Search Student
        function searchStudent() {
            const searchValue = document.getElementById('searchBox').value.trim().toLowerCase();
            const studentDetails = document.getElementById('studentDetails');
            const studentTitle = document.getElementById('studentTitle');
            const studentTableBody = document.getElementById('studentTableBody');

            let found = false;
            studentTableBody.innerHTML = '';

            Object.keys(studentsData).forEach(year => {
                studentsData[year].forEach(student => {
                    if (
                        student.name.toLowerCase().includes(searchValue) ||
                        student.regNo.toLowerCase().includes(searchValue) ||
                        student.uniNo.toLowerCase().includes(searchValue) // Added university number check
                    ) {
                        found = true;
                        const row = document.createElement('tr');
                        row.innerHTML = `
                            <td>${student.name}</td>
                            <td>${student.regNo}</td>
                            <td>${student.uniNo}</td>
                            <td>${student.dob}</td>
                            <td>${student.year}</td>
                        `;
                        studentTableBody.appendChild(row);
                    }
                });
            });

            studentTitle.innerText = found ? 'Search Results' : 'No Results Found';
            document.getElementById('departmentSection').style.display = 'none';
            document.getElementById('yearSection').style.display = 'none';
            studentDetails.style.display = 'block';
        }
    </script>
</body>
</html>
