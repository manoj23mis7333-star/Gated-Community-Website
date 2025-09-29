<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Gates Community Management</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f3f4f6;
        }
        .login-container {
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            padding: 20px;
        }
        .login-box {
            background: white;
            padding: 40px;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            width: 100%;
            max-width: 400px;
        }
        .login-header {
            text-align: center;
            margin-bottom: 30px;
        }
        .login-header h1 {
            color: #4f46e5;
            font-size: 32px;
            margin-bottom: 10px;
        }
        .login-header p {
            color: #6b7280;
            font-size: 14px;
        }
        .form-group {
            margin-bottom: 20px;
        }
        .form-group label {
            display: block;
            margin-bottom: 8px;
            color: #374151;
            font-weight: 600;
            font-size: 14px;
        }
        .form-group input {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid #e5e7eb;
            border-radius: 8px;
            font-size: 14px;
            outline: none;
        }
        .form-group input:focus {
            border-color: #4f46e5;
        }
        .btn-login {
            width: 100%;
            padding: 14px;
            background: #4f46e5;
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 16px;
            font-weight: 600;
            cursor: pointer;
            margin-top: 10px;
        }
        .btn-login:hover {
            background: #4338ca;
        }
        .forgot-password {
            text-align: center;
            margin-top: 15px;
        }
        .forgot-password a {
            color: #4f46e5;
            text-decoration: none;
            font-size: 14px;
        }
        .dashboard-container {
            display: none;
        }
        .dashboard-container.active {
            display: flex;
            height: 100vh;
        }
        .sidebar {
            width: 260px;
            background: #1e1b4b;
            color: white;
            padding: 30px 20px;
            overflow-y: auto;
            position: fixed;
            left: 0;
            top: 0;
            height: 100vh;
            z-index: 100;
        }
        .sidebar.mobile-hidden {
            display: none;
        }
        .sidebar-header {
            display: flex;
            align-items: center;
            gap: 12px;
            margin-bottom: 40px;
        }
        .sidebar-header h2 {
            font-size: 24px;
        }
        .nav-item {
            padding: 12px 16px;
            margin-bottom: 8px;
            border-radius: 8px;
            cursor: pointer;
            display: flex;
            align-items: center;
            gap: 12px;
            color: #e0e7ff;
        }
        .nav-item:hover {
            background: #312e81;
        }
        .nav-item.active {
            background: #4338ca;
            color: white;
        }
        .nav-item.logout {
            margin-top: 20px;
        }
        .nav-item.logout:hover {
            background: #dc2626;
        }
        .main-content {
            flex: 1;
            margin-left: 260px;
            overflow-y: auto;
            padding: 30px;
        }
        .mobile-header {
            display: none;
            background: #1e1b4b;
            color: white;
            padding: 15px;
            align-items: center;
            justify-content: space-between;
            cursor: pointer;
        }
        .mobile-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.5);
            z-index: 50;
        }
        .mobile-overlay.active {
            display: block;
        }
        .page-title {
            font-size: 32px;
            color: #1f2937;
            margin-bottom: 30px;
        }
        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 24px;
            margin-bottom: 30px;
        }
        .stat-card {
            padding: 24px;
            border-radius: 16px;
            color: white;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        .stat-card.green {
            background: linear-gradient(135deg, #34d399 0%, #10b981 100%);
        }
        .stat-card.blue {
            background: linear-gradient(135deg, #60a5fa 0%, #3b82f6 100%);
        }
        .stat-card.purple {
            background: linear-gradient(135deg, #a78bfa 0%, #8b5cf6 100%);
        }
        .stat-card.orange {
            background: linear-gradient(135deg, #fb923c 0%, #f97316 100%);
        }
        .stat-card h3 {
            font-size: 16px;
            margin-bottom: 8px;
            opacity: 0.9;
        }
        .stat-card .value {
            font-size: 36px;
            font-weight: bold;
            margin-bottom: 8px;
        }
        .stat-card .label {
            font-size: 14px;
            opacity: 0.9;
        }
        .white-card {
            background: white;
            padding: 24px;
            border-radius: 16px;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            margin-bottom: 24px;
        }
        .card-title {
            font-size: 20px;
            font-weight: bold;
            color: #1f2937;
            margin-bottom: 20px;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        thead {
            background: #4f46e5;
            color: white;
        }
        th, td {
            padding: 16px;
            text-align: left;
        }
        tbody tr {
            border-bottom: 1px solid #e5e7eb;
        }
        tbody tr:hover {
            background: #f9fafb;
        }
        .status-badge {
            display: inline-block;
            padding: 6px 12px;
            border-radius: 20px;
            font-size: 12px;
            font-weight: 600;
        }
        .status-badge.active {
            background: #d1fae5;
            color: #047857;
        }
        .status-badge.inactive {
            background: #fee2e2;
            color: #dc2626;
        }
        .status-badge.paid {
            background: #d1fae5;
            color: #047857;
        }
        .status-badge.pending {
            background: #fef3c7;
            color: #d97706;
        }
        .btn {
            padding: 12px 24px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            cursor: pointer;
            font-size: 14px;
        }
        .btn-primary {
            background: #4f46e5;
            color: white;
        }
        .btn-primary:hover {
            background: #4338ca;
        }
        .btn-secondary {
            background: #e5e7eb;
            color: #374151;
        }
        .btn-secondary:hover {
            background: #d1d5db;
        }
        .info-grid {
            display: grid;
            gap: 16px;
        }
        .info-row {
            display: flex;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #e5e7eb;
        }
        .info-label {
            color: #6b7280;
        }
        .info-value {
            font-weight: 600;
            color: #1f2937;
        }
        .parking-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
        }
        .parking-card {
            padding: 24px;
            border-radius: 12px;
            border: 3px solid;
        }
        .parking-card.occupied {
            background: #dbeafe;
            border-color: #3b82f6;
        }
        .parking-card.available {
            background: #d1fae5;
            border-color: #10b981;
        }
        .parking-card h3 {
            font-size: 24px;
            font-weight: bold;
            margin: 12px 0;
        }
        .notice-box {
            padding: 16px;
            background: #eef2ff;
            border-left: 4px solid #4f46e5;
            border-radius: 8px;
            margin-bottom: 12px;
        }
        .notice-title {
            font-weight: 600;
            color: #1f2937;
            margin-bottom: 4px;
        }
        .notice-content {
            color: #6b7280;
            font-size: 14px;
            margin-bottom: 4px;
        }
        .notice-date {
            color: #9ca3af;
            font-size: 12px;
        }
        .two-col {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 24px;
        }
        .payment-box {
            padding: 16px;
            border-radius: 8px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .payment-box.rent {
            background: #fee2e2;
            border: 1px solid #fca5a5;
        }
        .payment-box.bill {
            background: #fef3c7;
            border: 1px solid #fcd34d;
        }
        .payment-amount {
            font-size: 20px;
            font-weight: bold;
        }
        .hidden {
            display: none !important;
        }
        .page-content {
            display: none;
        }
        .page-content.active {
            display: block;
        }
        @media (max-width: 1024px) {
            .sidebar {
                display: none;
            }
            .sidebar.mobile-open {
                display: block;
            }
            .mobile-header {
                display: flex;
            }
            .dashboard-container.active {
                flex-direction: column;
            }
            .main-content {
                margin-left: 0;
            }
        }
        @media (max-width: 640px) {
            .main-content {
                padding: 15px;
            }
            .page-title {
                font-size: 24px;
            }
            .card-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="login-container" id="loginPage">
        <div class="login-box">
            <div class="login-header">
                <h1>🏠 Gates Community</h1>
                <p>Manage your gated community</p>
            </div>
            <div class="form-group">
                <label>Email</label>
                <input type="email" id="loginEmail" placeholder="your.email@example.com">
            </div>
            <div class="form-group">
                <label>Password</label>
                <input type="password" id="loginPassword" placeholder="Enter your password">
            </div>
            <button class="btn-login" onclick="login()">Sign In</button>
            <div class="forgot-password">
                <a href="#">Forgot Password?</a>
            </div>
        </div>
    </div>
    
    <div class="dashboard-container" id="dashboardPage">
        <div class="mobile-overlay" id="mobileOverlay" onclick="toggleMobileMenu()"></div>
        
        <div class="sidebar" id="sidebar">
            <div class="sidebar-header">
                <h2>🏠 Gates</h2>
            </div>
            <nav>
                <div class="nav-item active" onclick="showPage('dashboard', this)">📊 Dashboard</div>
                <div class="nav-item" onclick="showPage('rent', this)">💰 Rent Details</div>
                <div class="nav-item" onclick="showPage('maids', this)">👥 Maids & Services</div>
                <div class="nav-item" onclick="showPage('parking', this)">🚗 Parking</div>
                <div class="nav-item" onclick="showPage('bills', this)">📄 Utility Bills</div>
                <div class="nav-item" onclick="showPage('lounge', this)">🍸 Bar & Lounge</div>
                <div class="nav-item" onclick="showPage('pool', this)">🏊 Swimming Pool</div>
                <div class="nav-item" onclick="showPage('theatre', this)">🎬 Theatre</div>
                <div class="nav-item" onclick="showPage('events', this)">🎉 Events</div>
                <div class="nav-item" onclick="showPage('meetings', this)">📅 Meetings</div>
                <div class="nav-item" onclick="showPage('gym', this)">💪 Gym & Fitness</div>
                <div class="nav-item" onclick="showPage('sports', this)">🎾 Sports Complex</div>
                <div class="nav-item" onclick="showPage('library', this)">📚 Library</div>
                <div class="nav-item" onclick="showPage('salon', this)">💇 Salon & Spa</div>
                <div class="nav-item" onclick="showPage('security', this)">🛡 Security</div>
                <div class="nav-item" onclick="showPage('maintenance', this)">🔧 Maintenance</div>
                <div class="nav-item" onclick="showPage('visitors', this)">👥 Visitor Management</div>
                <div class="nav-item" onclick="showPage('marketplace', this)">🛒 Community Marketplace</div>
                <div class="nav-item" onclick="showPage('complaints', this)">📝 Complaints & Feedback</div>
                <div class="nav-item" onclick="showPage('settings', this)">⚙ Settings</div>
                <div class="nav-item logout" onclick="logout()">🚪 Logout</div>
            </nav>
        </div>
        
        <div class="main-content">
            <div class="mobile-header" onclick="toggleMobileMenu()">
                <span style="font-size: 24px;">☰</span>
                <span style="font-weight: bold; font-size: 18px;">Gates Community</span>
                <span></span>
            </div>
            
            <div id="dashboardContent" class="page-content active">
                <h1 class="page-title">Dashboard</h1>
                <div class="card-grid">
                    <div class="stat-card green">
                        <h3>Rent Status</h3>
                        <div class="value">₹15,000</div>
                        <div class="label">Paid</div>
                    </div>
                    <div class="stat-card blue">
                        <h3>Parking Slots</h3>
                        <div class="value">2/2</div>
                        <div class="label">Occupied</div>
                    </div>
                    <div class="stat-card purple">
                        <h3>Active Maids</h3>
                        <div class="value">2/3</div>
                        <div class="label">Available</div>
                    </div>
                    <div class="stat-card orange">
                        <h3>Pending Bills</h3>
                        <div class="value">₹3,680</div>
                        <div class="label">3 Bills Due</div>
                    </div>
                </div>
                <div class="two-col">
                    <div class="white-card">
                        <h3 class="card-title">🔔 Recent Notices</h3>
                        <div class="notice-box">
                            <div class="notice-title">Society Meeting</div>
                            <div class="notice-content">Monthly society meeting at 6 PM in clubhouse</div>
                            <div class="notice-date">2025-10-15</div>
                        </div>
                        <div class="notice-box">
                            <div class="notice-title">Water Supply Interruption</div>
                            <div class="notice-content">Water supply will be interrupted from 10 AM to 2 PM</div>
                            <div class="notice-date">2025-10-08</div>
                        </div>
                        <div class="notice-box">
                            <div class="notice-title">Festival Celebration</div>
                            <div class="notice-content">Dussehra celebration in community hall</div>
                            <div class="notice-date">2025-10-20</div>
                        </div>
                    </div>
                    <div class="white-card">
                        <h3 class="card-title">📅 Upcoming Payments</h3>
                        <div class="payment-box rent">
                            <div>
                                <div style="font-weight: 600; color: #1f2937;">Rent Due</div>
                                <div style="font-size: 14px; color: #6b7280;">2025-10-05</div>
                            </div>
                            <div class="payment-amount" style="color: #dc2626;">₹15,000</div>
                        </div>
                        <div class="payment-box bill">
                            <div>
                                <div style="font-weight: 600; color: #1f2937;">Electricity</div>
                                <div style="font-size: 14px; color: #6b7280;">2025-10-10</div>
                            </div>
                            <div class="payment-amount" style="color: #d97706;">₹2,340</div>
                        </div>
                        <div class="payment-box bill">
                            <div>
                                <div style="font-weight: 600; color: #1f2937;">Water</div>
                                <div style="font-size: 14px; color: #6b7280;">2025-10-15</div>
                            </div>
                            <div class="payment-amount" style="color: #d97706;">₹450</div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div id="rentContent" class="page-content">
                <h1 class="page-title">Rent Details</h1>
                <div class="white-card">
                    <div class="two-col">
                        <div>
                            <h3 style="font-size: 18px; font-weight: 600; margin-bottom: 20px;">Payment Information</h3>
                            <div class="info-grid">
                                <div class="info-row">
                                    <span class="info-label">Monthly Rent:</span>
                                    <span class="info-value">₹15,000</span>
                                </div>
                                <div class="info-row">
                                    <span class="info-label">Due Date:</span>
                                    <span class="info-value">5th of every month</span>
                                </div>
                                <div class="info-row">
                                    <span class="info-label">Last Paid:</span>
                                    <span class="info-value" style="color: #10b981;">2025-09-01</span>
                                </div>
                                <div class="info-row">
                                    <span class="info-label">Next Due:</span>
                                    <span class="info-value" style="color: #f97316;">2025-10-05</span>
                                </div>
                                <div class="info-row">
                                    <span class="info-label">Late Fee (per day):</span>
                                    <span class="info-value" style="color: #dc2626;">₹500</span>
                                </div>
                                <div class="info-row">
                                    <span class="info-label">Status:</span>
                                    <span class="status-badge paid">Paid</span>
                                </div>
                            </div>
                        </div>
                        <div>
                            <h3 style="font-size: 18px; font-weight: 600; margin-bottom: 20px;">Payment History</h3>
                            <div style="max-height: 300px; overflow-y: auto;">
                                <div style="display: flex; justify-content: space-between; padding: 12px; background: #f9fafb; border-radius: 8px; margin-bottom: 8px;">
                                    <span>September 2025</span>
                                    <span style="color: #10b981; font-weight: 600;">✓ Paid</span>
                                </div>
                                <div style="display: flex; justify-content: space-between; padding: 12px; background: #f9fafb; border-radius: 8px; margin-bottom: 8px;">
                                    <span>August 2025</span>
                                    <span style="color: #10b981; font-weight: 600;">✓ Paid</span>
                                </div>
                                <div style="display: flex; justify-content: space-between; padding: 12px; background: #f9fafb; border-radius: 8px; margin-bottom: 8px;">
                                    <span>July 2025</span>
                                    <span style="color: #10b981; font-weight: 600;">✓ Paid</span>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div style="margin-top: 24px;">
                        <button class="btn btn-primary">Pay Rent Now</button>
                    </div>
                </div>
            </div>
            
            <div id="maidsContent" class="page-content">
                <h1 class="page-title">Maids & Services</h1>
                <div class="white-card">
                    <table>
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>Service</th>
                                <th>Time</th>
                                <th>Days</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td style="font-weight: 600;">Lakshmi</td>
                                <td>Cleaning</td>
                                <td>8:00 AM - 10:00 AM</td>
                                <td>Mon, Wed, Fri</td>
                                <td><span class="status-badge active">Active</span></td>
                            </tr>
                            <tr>
                                <td style="font-weight: 600;">Ramya</td>
                                <td>Cooking</td>
                                <td>6:00 PM - 8:00 PM</td>
                                <td>Tue, Thu, Sat</td>
                                <td><span class="status-badge active">Active</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            
            <div id="parkingContent" class="page-content">
                <h1 class="page-title">Parking Management</h1>
                <div class="parking-grid">
                    <div class="parking-card occupied">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px;">
                            <span style="font-size: 32px;">🚗</span>
                            <span class="status-badge" style="background: #3b82f6; color: white;">Occupied</span>
                        </div>
                        <h3>Slot A-101</h3>
                        <p style="font-weight: 600;">Car - AP 39 XX 1234</p>
                    </div>
                    <div class="parking-card available">
                        <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px;">
                            <span style="font-size: 32px;">🅿️</span>
                            <span class="status-badge" style="background: #10b981; color: white;">Available</span>
                        </div>
                        <h3>Visitor-3</h3>
                        <p style="font-weight: 600;">Available</p>
                    </div>
                </div>
            </div>
            
            <div id="billsContent" class="page-content">
                <h1 class="page-title">Utility Bills</h1>
                <div class="white-card">
                    <table>
                        <thead>
                            <tr>
                                <th>Bill Type</th>
                                <th>Amount</th>
                                <th>Due Date</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td style="font-weight: 600;">Electricity</td>
                                <td style="font-weight: 700;">₹2,340</td>
                                <td>2025-10-10</td>
                                <td><span class="status-badge pending">Pending</span></td>
                            </tr>
                            <tr>
                                <td style="font-weight: 600;">Water</td>
                                <td style="font-weight: 700;">₹450</td>
                                <td>2025-10-15</td>
                                <td><span class="status-badge pending">Pending</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Payment Summary</h3>
                    <div style="display: flex; justify-content: space-between; margin-bottom: 16px;">
                        <span style="color: #6b7280;">Total Pending:</span>
                        <span style="font-size: 24px; font-weight: bold; color: #dc2626;">₹3,680</span>
                    </div>
                    <div style="display: flex; justify-content: space-between;">
                        <span style="color: #6b7280;">Total Paid This Month:</span>
                        <span style="font-size: 24px; font-weight: bold; color: #10b981;">₹3,500</span>
                    </div>
                </div>
            </div>
            
            <div id="loungeContent" class="page-content">
                <h1 class="page-title">🍸 Bar & Lounge</h1>
                <div class="card-grid">
                    <div class="stat-card purple">
                        <h3>Opening Hours</h3>
                        <div class="value">6 PM - 12 AM</div>
                        <div class="label">Everyday</div>
                    </div>
                    <div class="stat-card orange">
                        <h3>Current Status</h3>
                        <div class="value">Open</div>
                        <div class="label">20 Seats Available</div>
                    </div>
                </div>
            </div>
            
            <div id="poolContent" class="page-content">
                <h1 class="page-title">🏊 Swimming Pool</h1>
                <div class="card-grid">
                    <div class="stat-card blue">
                        <h3>Pool Timings</h3>
                        <div class="value">6 AM - 9 PM</div>
                        <div class="label">7 Days a Week</div>
                    </div>
                </div>
            </div>
            
            <div id="theatreContent" class="page-content">
                <h1 class="page-title">🎬 Community Theatre</h1>
                <div class="card-grid">
                    <div class="stat-card purple">
                        <h3>Seating Capacity</h3>
                        <div class="value">100</div>
                        <div class="label">Premium Seats</div>
                    </div>
                </div>
            </div>
            
            <div id="eventsContent" class="page-content">
                <h1 class="page-title">🎉 Community Events</h1>
                <div class="white-card">
                    <h3 class="card-title">Upcoming Events</h3>
                    <div class="notice-box">
                        <div class="notice-title">Dussehra Celebration</div>
                        <div class="notice-content">Grand celebration with cultural programs and food</div>
                        <div class="notice-date">October 20, 2025</div>
                    </div>
                </div>
            </div>
            
            <div id="meetingsContent" class="page-content">
                <h1 class="page-title">📅 Meeting Rooms</h1>
                <div class="card-grid">
                    <div class="stat-card blue">
                        <h3>Conference Hall</h3>
                        <div class="value">50</div>
                        <div class="label">Seating Capacity</div>
                    </div>
                    <div class="stat-card green">
                        <h3>Board Room</h3>
                        <div class="value">20</div>
                        <div class="label">Seating Capacity</div>
                    </div>
                </div>
            </div>
            
            <div id="gymContent" class="page-content">
                <h1 class="page-title">💪 Gym & Fitness</h1>
                <div class="card-grid">
                    <div class="stat-card orange">
                        <h3>Gym Timings</h3>
                        <div class="value">5 AM - 11 PM</div>
                        <div class="label">All Days</div>
                    </div>
                    <div class="stat-card purple">
                        <h3>Trainer Available</h3>
                        <div class="value">6 AM - 10 PM</div>
                        <div class="label">Personal Training</div>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Facilities</h3>
                    <div style="line-height: 1.8; color: #374151;">
                        ✓ Cardio Equipment (Treadmills, Cycles, Cross-trainers)<br>
                        ✓ Weight Training Equipment<br>
                        ✓ Free Weights & Dumbbells<br>
                        ✓ Yoga Studio<br>
                        ✓ Steam Room & Sauna<br>
                        ✓ Locker Rooms & Showers<br>
                        ✓ Personal Training Sessions<br>
                        ✓ Group Fitness Classes
                    </div>
                </div>
            </div>
            
            <div id="sportsContent" class="page-content">
                <h1 class="page-title">🎾 Sports Complex</h1>
                <div class="card-grid">
                    <div class="stat-card green">
                        <h3>Tennis Court</h3>
                        <div class="value">2</div>
                        <div class="label">Courts Available</div>
                    </div>
                    <div class="stat-card blue">
                        <h3>Badminton</h3>
                        <div class="value">4</div>
                        <div class="label">Courts Available</div>
                    </div>
                    <div class="stat-card purple">
                        <h3>Basketball</h3>
                        <div class="value">1</div>
                        <div class="label">Full Court</div>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Book a Court</h3>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px;">
                        <select style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                            <option>Tennis Court - ₹300/hour</option>
                            <option>Badminton - ₹200/hour</option>
                            <option>Basketball - ₹400/hour</option>
                        </select>
                        <input type="date" style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <input type="time" style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <button class="btn btn-primary">Book Now</button>
                    </div>
                </div>
            </div>
            
            <div id="libraryContent" class="page-content">
                <h1 class="page-title">📚 Library</h1>
                <div class="card-grid">
                    <div class="stat-card purple">
                        <h3>Total Books</h3>
                        <div class="value">5,000+</div>
                        <div class="label">Collection</div>
                    </div>
                    <div class="stat-card blue">
                        <h3>Library Hours</h3>
                        <div class="value">9 AM - 9 PM</div>
                        <div class="label">All Days</div>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Search Books</h3>
                    <input type="text" placeholder="Search by title, author, or genre..." style="width: 100%; padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px; margin-bottom: 16px;">
                    <h3 class="card-title">Popular Categories</h3>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 12px;">
                        <button class="btn btn-secondary">Fiction</button>
                        <button class="btn btn-secondary">Non-Fiction</button>
                        <button class="btn btn-secondary">Biography</button>
                        <button class="btn btn-secondary">Self-Help</button>
                        <button class="btn btn-secondary">Children's Books</button>
                        <button class="btn btn-secondary">Technology</button>
                    </div>
                </div>
            </div>
            
            <div id="salonContent" class="page-content">
                <h1 class="page-title">💇 Salon & Spa</h1>
                <div class="card-grid">
                    <div class="stat-card orange">
                        <h3>Salon Hours</h3>
                        <div class="value">10 AM - 8 PM</div>
                        <div class="label">Tue - Sun</div>
                    </div>
                    <div class="stat-card purple">
                        <h3>Spa Services</h3>
                        <div class="value">Available</div>
                        <div class="label">Appointment Required</div>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Services & Pricing</h3>
                    <table>
                        <thead>
                            <tr>
                                <th>Service</th>
                                <th>Duration</th>
                                <th>Price</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Haircut (Men)</td>
                                <td>30 min</td>
                                <td>₹300</td>
                            </tr>
                            <tr>
                                <td>Haircut (Women)</td>
                                <td>45 min</td>
                                <td>₹500</td>
                            </tr>
                            <tr>
                                <td>Spa Massage</td>
                                <td>60 min</td>
                                <td>₹1,500</td>
                            </tr>
                            <tr>
                                <td>Facial</td>
                                <td>45 min</td>
                                <td>₹800</td>
                            </tr>
                        </tbody>
                    </table>
                    <button class="btn btn-primary" style="margin-top: 16px;">Book Appointment</button>
                </div>
            </div>
            
            <div id="securityContent" class="page-content">
                <h1 class="page-title">🛡 Security</h1>
                <div class="card-grid">
                    <div class="stat-card green">
                        <h3>24/7 Security</h3>
                        <div class="value">Active</div>
                        <div class="label">Always On Duty</div>
                    </div>
                    <div class="stat-card blue">
                        <h3>CCTV Cameras</h3>
                        <div class="value">120+</div>
                        <div class="label">Full Coverage</div>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Emergency Contacts</h3>
                    <div class="info-grid">
                        <div class="info-row">
                            <span class="info-label">Security Control Room:</span>
                            <span class="info-value">+91 98765 00001</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">Fire Department:</span>
                            <span class="info-value">101</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">Police:</span>
                            <span class="info-value">100</span>
                        </div>
                        <div class="info-row">
                            <span class="info-label">Ambulance:</span>
                            <span class="info-value">108</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div id="maintenanceContent" class="page-content">
                <h1 class="page-title">🔧 Maintenance</h1>
                <div class="white-card">
                    <h3 class="card-title">Request Maintenance</h3>
                    <div style="display: grid; gap: 16px;">
                        <select style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                            <option>Select Issue Type</option>
                            <option>Plumbing</option>
                            <option>Electrical</option>
                            <option>Carpentry</option>
                            <option>Painting</option>
                            <option>AC/Appliance</option>
                            <option>Other</option>
                        </select>
                        <textarea rows="4" placeholder="Describe the issue..." style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;"></textarea>
                        <button class="btn btn-primary">Submit Request</button>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Active Requests</h3>
                    <div class="notice-box">
                        <div class="notice-title">Plumbing - Kitchen Tap Leak</div>
                        <div class="notice-content">Status: In Progress</div>
                        <div class="notice-date">Submitted: Oct 1, 2025</div>
                    </div>
                </div>
            </div>
            
            <div id="visitorsContent" class="page-content">
                <h1 class="page-title">👥 Visitor Management</h1>
                <div class="white-card">
                    <h3 class="card-title">Pre-Approve Visitor</h3>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 16px;">
                        <input type="text" placeholder="Visitor Name" style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <input type="tel" placeholder="Phone Number" style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <input type="datetime-local" style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <button class="btn btn-primary">Add Visitor</button>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Recent Visitors</h3>
                    <table>
                        <thead>
                            <tr>
                                <th>Name</th>
                                <th>Phone</th>
                                <th>Date & Time</th>
                                <th>Status</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr>
                                <td>Rajesh Kumar</td>
                                <td>+91 98765 43210</td>
                                <td>Oct 1, 2025 - 4:30 PM</td>
                                <td><span class="status-badge active">Checked Out</span></td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            
            <div id="marketplaceContent" class="page-content">
                <h1 class="page-title">🛒 Community Marketplace</h1>
                <div class="white-card">
                    <h3 class="card-title">Buy & Sell Items</h3>
                    <button class="btn btn-primary" style="margin-bottom: 20px;">Post New Item</button>
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px;">
                        <div style="border: 2px solid #e5e7eb; border-radius: 12px; padding: 20px;">
                            <div style="background: #f3f4f6; height: 150px; border-radius: 8px; margin-bottom: 12px;"></div>
                            <h4 style="font-weight: bold; margin-bottom: 8px;">Study Table</h4>
                            <p style="color: #6b7280; font-size: 14px; margin-bottom: 8px;">Good condition, 2 years old</p>
                            <div style="display: flex; justify-content: space-between; align-items: center;">
                                <span style="font-size: 20px; font-weight: bold; color: #4f46e5;">₹2,500</span>
                                <button class="btn btn-secondary" style="padding: 8px 16px; font-size: 12px;">Contact</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            
            <div id="complaintsContent" class="page-content">
                <h1 class="page-title">📝 Complaints & Feedback</h1>
                <div class="white-card">
                    <h3 class="card-title">Submit Complaint/Feedback</h3>
                    <div style="display: grid; gap: 16px;">
                        <select style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                            <option>Select Category</option>
                            <option>Noise Complaint</option>
                            <option>Parking Issue</option>
                            <option>Maintenance</option>
                            <option>Security</option>
                            <option>Cleanliness</option>
                            <option>Other</option>
                        </select>
                        <input type="text" placeholder="Subject" style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <textarea rows="5" placeholder="Describe your complaint or feedback..." style="padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;"></textarea>
                        <button class="btn btn-primary">Submit</button>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Your Submissions</h3>
                    <div class="notice-box">
                        <div class="notice-title">Parking Issue - Resolved</div>
                        <div class="notice-content">Visitor vehicle blocking driveway</div>
                        <div class="notice-date">Submitted: Sep 28, 2025 | Resolved: Sep 29, 2025</div>
                    </div>
                </div>
            </div>
            
            <div id="settingsContent" class="page-content">
                <h1 class="page-title">⚙ Settings</h1>
                <div class="white-card">
                    <h3 class="card-title">Profile Settings</h3>
                    <div style="display: grid; gap: 16px;">
                        <div>
                            <label style="display: block; margin-bottom: 8px; font-weight: 600;">Name</label>
                            <input type="text" value="John Doe" style="width: 100%; padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        </div>
                        <div>
                            <label style="display: block; margin-bottom: 8px; font-weight: 600;">Email</label>
                            <input type="email" value="john.doe@example.com" style="width: 100%; padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        </div>
                        <div>
                            <label style="display: block; margin-bottom: 8px; font-weight: 600;">Phone</label>
                            <input type="tel" value="+91 98765 43210" style="width: 100%; padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        </div>
                        <button class="btn btn-primary">Update Profile</button>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Change Password</h3>
                    <div style="display: grid; gap: 16px;">
                        <input type="password" placeholder="Current Password" style="width: 100%; padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <input type="password" placeholder="New Password" style="width: 100%; padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <input type="password" placeholder="Confirm New Password" style="width: 100%; padding: 12px; border: 1px solid #e5e7eb; border-radius: 8px;">
                        <button class="btn btn-primary">Change Password</button>
                    </div>
                </div>
                <div class="white-card">
                    <h3 class="card-title">Notifications</h3>
                    <div style="display: grid; gap: 12px;">
                        <label style="display: flex; align-items: center; gap: 12px; cursor: pointer;">
                            <input type="checkbox" checked>
                            <span>Email notifications for payments</span>
                        </label>
                        <label style="display: flex; align-items: center; gap: 12px; cursor: pointer;">
                            <input type="checkbox" checked>
                            <span>SMS notifications for security alerts</span>
                        </label>
                        <label style="display: flex; align-items: center; gap: 12px; cursor: pointer;">
                            <input type="checkbox">
                            <span>Community event updates</span>
                        </label>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        function login() {
            var email = document.getElementById('loginEmail').value;
            var password = document.getElementById('loginPassword').value;
            
            if (email && password) {
                document.getElementById('loginPage').style.display = 'none';
                document.getElementById('dashboardPage').classList.add('active');
            } else {
                alert('Please enter email and password');
            }
        }
        
        function logout() {
            document.getElementById('dashboardPage').classList.remove('active');
            document.getElementById('loginPage').style.display = 'flex';
            document.getElementById('loginEmail').value = '';
            document.getElementById('loginPassword').value = '';
        }
        
        function showPage(pageName, element) {
            var pages = document.querySelectorAll('.page-content');
            for (var i = 0; i < pages.length; i++) {
                pages[i].classList.remove('active');
            }
            
            var navItems = document.querySelectorAll('.nav-item');
            for (var i = 0; i < navItems.length; i++) {
                navItems[i].classList.remove('active');
            }
            
            document.getElementById(pageName + 'Content').classList.add('active');
            
            if (element) {
                element.classList.add('active');
            }
            
            if (window.innerWidth <= 1024) {
                toggleMobileMenu();
            }
        }
        
        function toggleMobileMenu() {
            var sidebar = document.getElementById('sidebar');
            var overlay = document.getElementById('mobileOverlay');
            
            sidebar.classList.toggle('mobile-open');
            overlay.classList.toggle('active');
        }
    </script>
</body>
</html>
