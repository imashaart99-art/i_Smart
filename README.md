<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Job & Task Manager Pro</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
    <style>
        /* All existing CSS styles remain the same */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #f8f9fa;
            color: #333;
            line-height: 1.6;
        }

        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding: 20px 0;
            background: linear-gradient(135deg, #2c3e50, #3498db);
            color: white;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            position: relative;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
        }

        .header-buttons {
            position: absolute;
            top: 20px;
            right: 20px;
            display: flex;
            gap: 10px;
        }

        .header-btn {
            background-color: #e74c3c;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .header-btn:hover {
            background-color: #c0392b;
        }

        .finance-btn {
            background-color: #27ae60;
        }

        .finance-btn:hover {
            background-color: #229954;
        }

        .tabs {
            display: flex;
            margin-bottom: 20px;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .tab {
            flex: 1;
            padding: 15px;
            text-align: center;
            cursor: pointer;
            transition: background-color 0.3s;
            border-bottom: 3px solid transparent;
        }

        .tab:hover {
            background-color: #f0f2f5;
        }

        .tab.active {
            border-bottom: 3px solid #3498db;
            background-color: #f0f2f5;
        }

        .tab-content {
            display: none;
            background-color: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
        }

        .tab-content.active {
            display: block;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
        }

        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1rem;
        }

        textarea {
            resize: vertical;
            min-height: 100px;
        }

        button {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 12px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
            margin-right: 10px;
            margin-bottom: 10px;
        }

        button:hover {
            background-color: #2980b9;
        }

        .btn-secondary {
            background-color: #95a5a6;
        }

        .btn-secondary:hover {
            background-color: #7f8c8d;
        }

        .btn-danger {
            background-color: #e74c3c;
        }

        .btn-danger:hover {
            background-color: #c0392b;
        }

        .btn-success {
            background-color: #2ecc71;
        }

        .btn-success:hover {
            background-color: #27ae60;
        }

        .btn-payroll {
            background-color: #9b59b6;
        }

        .btn-payroll:hover {
            background-color: #8e44ad;
        }

        .btn-finance {
            background-color: #27ae60;
        }

        .btn-finance:hover {
            background-color: #229954;
        }

        /* Dashboard Styles */
        .dashboard-controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            flex-wrap: wrap;
            gap: 15px;
        }

        .dashboard-title {
            font-size: 1.8rem;
            color: #2c3e50;
            margin: 0;
        }

        .dashboard-filters {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .search-box {
            position: relative;
            min-width: 250px;
        }

        .search-box input {
            padding-left: 40px;
        }

        .search-box i {
            position: absolute;
            left: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #7f8c8d;
        }

        .filter-select {
            min-width: 150px;
        }

        .dashboard-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
        }

        .dashboard-section {
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.05);
            overflow: hidden;
        }

        .section-header {
            padding: 18px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #eee;
        }

        .section-title {
            font-size: 1.3rem;
            font-weight: 600;
            color: #2c3e50;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section-count {
            background-color: #3498db;
            color: white;
            border-radius: 20px;
            padding: 4px 12px;
            font-size: 0.85rem;
            font-weight: 600;
        }

        .pending-header {
            background-color: #fff8e1;
        }

        .pending-header .section-title {
            color: #f39c12;
        }

        .pending-header .section-count {
            background-color: #f39c12;
        }

        .completed-header {
            background-color: #e8f5e9;
        }

        .completed-header .section-title {
            color: #2ecc71;
        }

        .completed-header .section-count {
            background-color: #2ecc71;
        }

        .task-list {
            max-height: 600px;
            overflow-y: auto;
            padding: 15px;
        }

        .task-item {
            padding: 15px;
            border: 1px solid #eee;
            border-radius: 8px;
            margin-bottom: 12px;
            transition: all 0.2s ease;
            position: relative;
            background-color: #fff;
        }

        .task-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.08);
        }

        .priority-badge {
            position: absolute;
            top: 12px;
            right: 12px;
            padding: 3px 8px;
            border-radius: 12px;
            font-size: 0.75rem;
            font-weight: bold;
        }

        .priority-normal {
            background-color: #3498db;
            color: white;
        }

        .priority-important {
            background-color: #f39c12;
            color: white;
        }

        .priority-very-important {
            background-color: #e74c3c;
            color: white;
        }

        .priority-errors {
            background-color: #9b59b6;
            color: white;
        }

        .priority-fixes {
            background-color: #1abc9c;
            color: white;
        }

        .priority-bugs {
            background-color: #e67e22;
            color: white;
        }

        .priority-repairs {
            background-color: #34495e;
            color: white;
        }

        .priority-not-working {
            background-color: #c0392b;
            color: white;
        }

        .task-title {
            font-weight: 600;
            font-size: 1.1rem;
            margin-bottom: 8px;
            padding-right: 80px;
            color: #2c3e50;
        }

        .task-meta {
            display: flex;
            justify-content: space-between;
            margin-bottom: 10px;
            font-size: 0.9rem;
            color: #7f8c8d;
        }

        .task-deadline {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .task-cost {
            font-weight: 600;
            color: #2ecc71;
        }

        .task-actions {
            display: flex;
            justify-content: flex-end;
            gap: 8px;
            margin-top: 12px;
        }

        .task-actions button {
            padding: 6px 12px;
            font-size: 0.85rem;
            margin: 0;
        }

        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: #95a5a6;
        }

        .empty-state i {
            font-size: 3rem;
            margin-bottom: 15px;
            opacity: 0.5;
        }

        .empty-state h3 {
            font-weight: 500;
            margin-bottom: 5px;
        }

        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 20px;
            background-color: #2ecc71;
            color: white;
            border-radius: 5px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            transform: translateX(150%);
            transition: transform 0.3s ease-out;
            z-index: 1000;
        }

        .notification.show {
            transform: translateX(0);
        }

        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            overflow: auto;
        }

        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 20px;
            border-radius: 10px;
            width: 90%;
            max-width: 900px;
            position: relative;
        }

        .close-modal {
            position: absolute;
            top: 10px;
            right: 15px;
            font-size: 24px;
            cursor: pointer;
        }

        .comments-section {
            margin-top: 20px;
            border-top: 1px solid #eee;
            padding-top: 15px;
        }

        .comment {
            background-color: #f9f9f9;
            padding: 10px;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        .comment-date {
            font-size: 0.8rem;
            color: #777;
            margin-bottom: 5px;
        }

        .file-upload {
            margin-bottom: 15px;
        }

        .file-preview {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }

        .file-item {
            position: relative;
            width: 100px;
            height: 100px;
            border: 1px solid #ddd;
            border-radius: 5px;
            overflow: hidden;
        }

        .file-item img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .file-item .remove-file {
            position: absolute;
            top: 5px;
            right: 5px;
            background-color: rgba(255, 255, 255, 0.7);
            border-radius: 50%;
            width: 20px;
            height: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }

        .chart-container {
            height: 300px;
            margin-top: 20px;
            margin-bottom: 30px;
        }

        .invoice-container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }

        .invoice-header {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }

        .invoice-details {
            margin-bottom: 20px;
        }

        .invoice-table {
            width: 100%;
            border-collapse: collapse;
            margin-bottom: 20px;
        }

        .invoice-table th, .invoice-table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }

        .invoice-table th {
            background-color: #f2f2f2;
        }

        .invoice-total {
            text-align: right;
            font-size: 1.2rem;
            font-weight: bold;
        }

        .remaining-time {
            font-size: 0.9rem;
            font-weight: bold;
            margin-bottom: 10px;
        }

        .time-overdue {
            color: #e74c3c;
        }

        .time-warning {
            color: #f39c12;
        }

        .time-normal {
            color: #2ecc71;
        }

        .filter-section {
            background-color: #f8f9fa;
            padding: 15px;
            border-radius: 5px;
            margin-bottom: 20px;
        }

        .filter-row {
            display: flex;
            gap: 15px;
            margin-bottom: 10px;
            flex-wrap: wrap;
        }

        .filter-group {
            flex: 1;
            min-width: 200px;
        }

        .report-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }

        .report-table th, .report-table td {
            border: 1px solid #ddd;
            padding: 8px;
            text-align: left;
        }

        .report-table th {
            background-color: #f2f2f2;
        }

        .report-table tr:nth-child(even) {
            background-color: #f8f9fa;
        }

        .invoice-archive {
            margin-top: 20px;
        }

        .invoice-archive-item {
            padding: 15px;
            border: 1px solid #eee;
            border-radius: 5px;
            margin-bottom: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .invoice-archive-item:hover {
            background-color: #f8f9fa;
        }

        .invoice-details-summary {
            flex: 1;
        }

        .invoice-actions {
            display: flex;
            gap: 10px;
        }

        /* Payroll Module Styles */
        .payroll-module {
            display: none;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 25px;
            margin-bottom: 20px;
        }

        .payroll-module.active {
            display: block;
        }

        .payroll-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 1px solid #eee;
            padding-bottom: 15px;
        }

        .payroll-title {
            font-size: 1.8rem;
            color: #2c3e50;
            margin: 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .payroll-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #eee;
        }

        .payroll-tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 2px solid transparent;
            font-weight: 500;
            transition: all 0.3s;
        }

        .payroll-tab:hover {
            background-color: #f8f9fa;
        }

        .payroll-tab.active {
            border-bottom: 2px solid #9b59b6;
            color: #9b59b6;
        }

        .payroll-tab-content {
            display: none;
        }

        .payroll-tab-content.active {
            display: block;
        }

        .employee-form {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .employee-list {
            margin-top: 20px;
        }

        .employee-card {
            background-color: #f8f9fa;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            border-left: 4px solid #9b59b6;
            transition: transform 0.2s;
        }

        .employee-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }

        .employee-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .employee-name {
            font-size: 1.2rem;
            font-weight: 600;
            color: #2c3e50;
        }

        .employee-number {
            background-color: #9b59b6;
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 0.85rem;
        }

        .employee-details {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-bottom: 15px;
        }

        .employee-detail {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #555;
        }

        .employee-detail i {
            color: #9b59b6;
            width: 20px;
            text-align: center;
        }

        .employee-actions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }

        .salary-form {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .salary-calculations {
            background-color: #f8f9fa;
            border-radius: 8px;
            padding: 15px;
            margin-top: 20px;
        }

        .calculation-row {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }

        .calculation-row:last-child {
            border-bottom: none;
            font-weight: 600;
            font-size: 1.1rem;
            color: #2c3e50;
            margin-top: 10px;
            padding-top: 10px;
        }

        .calculation-label {
            color: #555;
        }

        .calculation-value {
            font-weight: 500;
        }

        .monthly-records {
            margin-top: 20px;
        }

        .record-card {
            background-color: #f8f9fa;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            border-left: 4px solid #2ecc71;
        }

        .record-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .record-month {
            font-size: 1.1rem;
            font-weight: 600;
            color: #2c3e50;
        }

        .record-year {
            background-color: #2ecc71;
            color: white;
            padding: 4px 10px;
            border-radius: 20px;
            font-size: 0.85rem;
        }

        .record-details {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-bottom: 15px;
        }

        .record-detail {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #555;
        }

        .record-detail i {
            color: #2ecc71;
            width: 20px;
            text-align: center;
        }

        .record-actions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }

        .back-btn {
            background-color: #95a5a6;
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1rem;
            transition: background-color 0.3s;
            display: flex;
            align-items: center;
            gap: 8px;
            margin-bottom: 20px;
        }

        .back-btn:hover {
            background-color: #7f8c8d;
        }

        /* Business Finance Module Styles */
        .finance-module {
            display: none;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            padding: 25px;
            margin-bottom: 20px;
        }

        .finance-module.active {
            display: block;
        }

        .finance-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 1px solid #eee;
            padding-bottom: 15px;
        }

        .finance-title {
            font-size: 1.8rem;
            color: #2c3e50;
            margin: 0;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .finance-tabs {
            display: flex;
            margin-bottom: 20px;
            border-bottom: 1px solid #eee;
        }

        .finance-tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 2px solid transparent;
            font-weight: 500;
            transition: all 0.3s;
        }

        .finance-tab:hover {
            background-color: #f8f9fa;
        }

        .finance-tab.active {
            border-bottom: 2px solid #27ae60;
            color: #27ae60;
        }

        .finance-tab-content {
            display: none;
        }

        .finance-tab-content.active {
            display: block;
        }

        .finance-form {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        .finance-list {
            margin-top: 20px;
        }

        .finance-card {
            background-color: #f8f9fa;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            transition: transform 0.2s;
        }

        .finance-card.income {
            border-left: 4px solid #2ecc71;
        }

        .finance-card.expense {
            border-left: 4px solid #e74c3c;
        }

        .finance-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.05);
        }

        .finance-header-card {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }

        .finance-title-card {
            font-size: 1.1rem;
            font-weight: 600;
            color: #2c3e50;
        }

        .finance-amount {
            font-size: 1.1rem;
            font-weight: 600;
        }

        .finance-amount.income {
            color: #2ecc71;
        }

        .finance-amount.expense {
            color: #e74c3c;
        }

        .finance-details {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 10px;
            margin-bottom: 15px;
        }

        .finance-detail {
            display: flex;
            align-items: center;
            gap: 8px;
            color: #555;
        }

        .finance-detail i {
            width: 20px;
            text-align: center;
        }

        .finance-detail.income i {
            color: #2ecc71;
        }

        .finance-detail.expense i {
            color: #e74c3c;
        }

        .finance-actions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }

        .finance-summary {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }

        .summary-card {
            background-color: #f8f9fa;
            border-radius: 8px;
            padding: 20px;
            text-align: center;
        }

        .summary-card.income {
            border-top: 4px solid #2ecc71;
        }

        .summary-card.expense {
            border-top: 4px solid #e74c3c;
        }

        .summary-card.profit {
            border-top: 4px solid #2ecc71;
        }

        .summary-card.loss {
            border-top: 4px solid #e74c3c;
        }

        .summary-title {
            font-size: 1rem;
            color: #555;
            margin-bottom: 10px;
        }

        .summary-amount {
            font-size: 1.8rem;
            font-weight: 600;
        }

        .summary-amount.income {
            color: #2ecc71;
        }

        .summary-amount.expense {
            color: #e74c3c;
        }

        .summary-amount.profit {
            color: #2ecc71;
        }

        .summary-amount.loss {
            color: #e74c3c;
        }

        .finance-report {
            background-color: #f8f9fa;
            border-radius: 8px;
            padding: 20px;
            margin-bottom: 20px;
        }

        .report-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 1px solid #ddd;
        }

        .report-title {
            font-size: 1.2rem;
            font-weight: 600;
            color: #2c3e50;
        }

        .report-period {
            font-size: 1rem;
            color: #555;
        }

        .report-summary {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
        }

        .report-summary-item {
            text-align: center;
            flex: 1;
        }

        .report-summary-label {
            font-size: 0.9rem;
            color: #555;
            margin-bottom: 5px;
        }

        .report-summary-value {
            font-size: 1.2rem;
            font-weight: 600;
        }

        .report-summary-value.income {
            color: #2ecc71;
        }

        .report-summary-value.expense {
            color: #e74c3c;
        }

        .report-summary-value.profit {
            color: #2ecc71;
        }

        .report-summary-value.loss {
            color: #e74c3c;
        }

        .report-details {
            margin-top: 20px;
        }

        .report-section {
            margin-bottom: 20px;
        }

        .report-section-title {
            font-size: 1.1rem;
            font-weight: 600;
            color: #2c3e50;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .report-section-title.income {
            color: #2ecc71;
        }

        .report-section-title.expense {
            color: #e74c3c;
        }

        .report-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }

        .report-item:last-child {
            border-bottom: none;
        }

        .report-item-description {
            color: #555;
        }

        .report-item-amount {
            font-weight: 500;
        }

        .report-item-amount.income {
            color: #2ecc71;
        }

        .report-item-amount.expense {
            color: #e74c3c;
        }

        @media (max-width: 768px) {
            .dashboard-grid, .employee-form, .salary-form, .finance-form, .finance-summary {
                grid-template-columns: 1fr;
            }
            
            .dashboard-controls {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .dashboard-filters {
                width: 100%;
            }
            
            .search-box {
                min-width: 100%;
            }
            
            .filter-select {
                min-width: 100%;
            }
            
            h1 {
                font-size: 2rem;
            }
            
            .container {
                padding: 10px;
            }
            
            .tabs {
                flex-direction: column;
            }
            
            .modal-content {
                width: 95%;
                margin: 5% auto;
            }
            
            .filter-row {
                flex-direction: column;
            }
            
            .invoice-archive-item {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .invoice-actions {
                margin-top: 10px;
            }
            
            .header-buttons {
                flex-direction: column;
                gap: 5px;
            }
            
            .payroll-btn, .finance-btn {
                position: static;
                margin-top: 15px;
                align-self: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-tasks"></i> Job & Task Manager Pro</h1>
            <p>Advanced job and task management system with invoicing</p>
            <div class="header-buttons">
                <button class="header-btn payroll-btn" id="payroll-btn">
                    <i class="fas fa-money-check-alt"></i> Payroll
                </button>
                <button class="header-btn finance-btn" id="finance-btn">
                    <i class="fas fa-chart-line"></i> Business Finance
                </button>
            </div>
        </header>

        <div id="main-app">
            <div class="tabs">
                <div class="tab active" data-tab="dashboard">
                    <i class="fas fa-tachometer-alt"></i> Dashboard
                </div>
                <div class="tab" data-tab="add-job">
                    <i class="fas fa-plus-circle"></i> Add Job
                </div>
                <div class="tab" data-tab="reports">
                    <i class="fas fa-chart-bar"></i> Reports
                </div>
                <div class="tab" data-tab="invoices">
                    <i class="fas fa-file-invoice-dollar"></i> Invoices
                </div>
            </div>

            <div id="dashboard" class="tab-content active">
                <div class="dashboard-controls">
                    <h2 class="dashboard-title">Job Dashboard</h2>
                    <div class="dashboard-filters">
                        <div class="search-box">
                            <i class="fas fa-search"></i>
                            <input type="text" id="search-input" placeholder="Search jobs...">
                        </div>
                        <div class="filter-select">
                            <select id="category-filter">
                                <option value="">All Categories</option>
                                <option value="normal">Normal</option>
                                <option value="important">Important</option>
                                <option value="very-important">Very Important</option>
                                <option value="errors">Errors</option>
                                <option value="fixes">Fixes</option>
                                <option value="bugs">Bugs</option>
                                <option value="repairs">Repairs</option>
                                <option value="not-working">Not Working</option>
                            </select>
                        </div>
                        <div class="filter-group">
                            <label for="deadline-from">Deadline From</label>
                            <input type="date" id="deadline-from">
                        </div>
                        <div class="filter-group">
                            <label for="deadline-to">Deadline To</label>
                            <input type="date" id="deadline-to">
                        </div>
                        <div class="filter-group">
                            <label for="min-cost">Min Cost (LKR)</label>
                            <input type="number" id="min-cost" min="0" step="0.01">
                        </div>
                        <div class="filter-group">
                            <label for="max-cost">Max Cost (LKR)</label>
                            <input type="number" id="max-cost" min="0" step="0.01">
                        </div>
                        <div class="filter-group">
                            <button id="reset-dashboard-filters" class="btn-secondary"><i class="fas fa-redo"></i> Reset</button>
                        </div>
                    </div>
                </div>

                <div class="dashboard-grid">
                    <div class="dashboard-section">
                        <div class="section-header pending-header">
                            <div class="section-title">
                                <i class="fas fa-clock"></i> Pending Jobs
                            </div>
                            <div class="section-count" id="pending-count">0</div>
                        </div>
                        <div class="task-list" id="pending-jobs">
                            <div class="empty-state">
                                <i class="fas fa-clipboard-list"></i>
                                <h3>No pending jobs</h3>
                                <p>Add a new job to get started</p>
                            </div>
                        </div>
                    </div>

                    <div class="dashboard-section">
                        <div class="section-header completed-header">
                            <div class="section-title">
                                <i class="fas fa-check-circle"></i> Completed Jobs
                            </div>
                            <div class="section-count" id="completed-count">0</div>
                        </div>
                        <div class="task-list" id="completed-jobs">
                            <div class="empty-state">
                                <i class="fas fa-clipboard-check"></i>
                                <h3>No completed jobs</h3>
                                <p>Complete a job to see it here</p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div id="add-job" class="tab-content">
                <h2 class="section-title"><i class="fas fa-plus-circle"></i> Add New Job</h2>
                <form id="job-form">
                    <div class="form-group">
                        <label for="job-title">Job Title</label>
                        <input type="text" id="job-title" required placeholder="Enter job title">
                    </div>
                    <div class="form-group">
                        <label for="job-description">Description</label>
                        <textarea id="job-description" required placeholder="Enter job description"></textarea>
                    </div>
                    <div class="form-group">
                        <label for="job-category">Category</label>
                        <select id="job-category" required>
                            <option value="">Select a category</option>
                            <option value="normal">Normal</option>
                            <option value="important">Important</option>
                            <option value="very-important">Very Important</option>
                            <option value="errors">Errors</option>
                            <option value="fixes">Fixes</option>
                            <option value="bugs">Bugs</option>
                            <option value="repairs">Repairs</option>
                            <option value="not-working">Not Working</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label for="job-deadline">Deadline</label>
                        <input type="date" id="job-deadline" required>
                    </div>
                    <div class="form-group">
                        <label for="job-cost">Cost (LKR)</label>
                        <input type="number" id="job-cost" min="0" step="0.01" required placeholder="0.00">
                    </div>
                    <div class="form-group file-upload">
                        <label for="job-files">Attachments</label>
                        <input type="file" id="job-files" multiple accept="image/*,.pdf,.doc,.docx">
                        <div id="file-preview" class="file-preview"></div>
                    </div>
                    <button type="submit"><i class="fas fa-save"></i> Save Job</button>
                    <button type="reset" class="btn-secondary"><i class="fas fa-redo"></i> Reset</button>
                </form>
            </div>

            <div id="reports" class="tab-content">
                <h2 class="section-title"><i class="fas fa-chart-bar"></i> Reports & Records</h2>
                
                <div class="filter-section">
                    <h3>Filter Jobs</h3>
                    <div class="filter-row">
                        <div class="filter-group">
                            <label for="filter-category">Category</label>
                            <select id="filter-category">
                                <option value="">All Categories</option>
                                <option value="normal">Normal</option>
                                <option value="important">Important</option>
                                <option value="very-important">Very Important</option>
                                <option value="errors">Errors</option>
                                <option value="fixes">Fixes</option>
                                <option value="bugs">Bugs</option>
                                <option value="repairs">Repairs</option>
                                <option value="not-working">Not Working</option>
                            </select>
                        </div>
                        <div class="filter-group">
                            <label for="filter-status">Status</label>
                            <select id="filter-status">
                                <option value="">All Statuses</option>
                                <option value="pending">Pending</option>
                                <option value="completed">Completed</option>
                            </select>
                        </div>
                        <div class="filter-group">
                            <label for="filter-date-from">From Date</label>
                            <input type="date" id="filter-date-from">
                        </div>
                        <div class="filter-group">
                            <label for="filter-date-to">To Date</label>
                            <input type="date" id="filter-date-to">
                        </div>
                    </div>
                    <div class="filter-row">
                        <button id="apply-filter"><i class="fas fa-filter"></i> Apply Filter</button>
                        <button id="reset-filter" class="btn-secondary"><i class="fas fa-redo"></i> Reset Filter</button>
                    </div>
                </div>
                
                <div class="chart-container">
                    <canvas id="completion-chart"></canvas>
                </div>
                
                <div id="report-results">
                    <h3>Job Report</h3>
                    <table class="report-table">
                        <thead>
                            <tr>
                                <th>ID</th>
                                <th>Title</th>
                                <th>Category</th>
                                <th>Status</th>
                                <th>Start Time</th>
                                <th>End Time</th>
                                <th>Cost (LKR)</th>
                            </tr>
                        </thead>
                        <tbody id="report-table-body">
                            <tr>
                                <td colspan="7" class="empty-state">Apply filters to see report results</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <div id="invoices" class="tab-content">
                <h2 class="section-title"><i class="fas fa-file-invoice-dollar"></i> Invoice Management</h2>
                
                <div id="generate-invoice-section">
                    <h3>Generate New Invoice</h3>
                    <div class="form-group">
                        <label for="invoice-job">Select Completed Job</label>
                        <select id="invoice-job">
                            <option value="">Select a job</option>
                        </select>
                    </div>
                    <button id="generate-invoice-btn"><i class="fas fa-file-invoice"></i> Generate Invoice</button>
                </div>
                
                <div class="invoice-archive">
                    <h3>Invoice Archive</h3>
                    <div id="invoices-list">
                        <div class="empty-state">No invoices generated yet</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Payroll Module -->
        <div id="payroll-module" class="payroll-module">
            <div class="payroll-header">
                <h2 class="payroll-title"><i class="fas fa-money-check-alt"></i> Payroll Management System</h2>
                <button class="back-btn" id="back-to-main">
                    <i class="fas fa-arrow-left"></i> Back to Main
                </button>
            </div>

            <div class="payroll-tabs">
                <div class="payroll-tab active" data-payroll-tab="employees">
                    <i class="fas fa-users"></i> Employees
                </div>
                <div class="payroll-tab" data-payroll-tab="salary">
                    <i class="fas fa-calculator"></i> Salary Calculation
                </div>
                <div class="payroll-tab" data-payroll-tab="reports">
                    <i class="fas fa-file-invoice-dollar"></i> Payroll Reports
                </div>
            </div>

            <div id="employees" class="payroll-tab-content active">
                <h3>Employee Management</h3>
                <button id="add-employee-btn" class="btn-payroll">
                    <i class="fas fa-user-plus"></i> Add Employee
                </button>

                <div id="employee-form-container" style="display: none;">
                    <h4>Add New Employee</h4>
                    <form id="employee-form" class="employee-form">
                        <div class="form-group">
                            <label for="employee-number">Employee Number</label>
                            <input type="text" id="employee-number" required placeholder="Enter employee number">
                        </div>
                        <div class="form-group">
                            <label for="employee-name">Full Name</label>
                            <input type="text" id="employee-name" required placeholder="Enter full name">
                        </div>
                        <div class="form-group">
                            <label for="employee-address">Address</label>
                            <textarea id="employee-address" required placeholder="Enter address"></textarea>
                        </div>
                        <div class="form-group">
                            <label for="employee-age">Age</label>
                            <input type="number" id="employee-age" required min="18" max="65" placeholder="Enter age">
                        </div>
                        <div class="form-group">
                            <label for="employee-dob">Date of Birth</label>
                            <input type="date" id="employee-dob" required>
                        </div>
                        <div class="form-group">
                            <label for="employee-mobile">Mobile Number</label>
                            <input type="tel" id="employee-mobile" required placeholder="Enter mobile number">
                        </div>
                        <div class="form-group">
                            <label for="employee-basic-salary">Basic Salary (LKR)</label>
                            <input type="number" id="employee-basic-salary" required min="0" step="0.01" placeholder="Enter basic salary">
                        </div>
                        <div class="form-group">
                            <label for="employee-etf">ETF %</label>
                            <input type="number" id="employee-etf" required min="0" max="100" step="0.01" value="3" placeholder="Enter ETF percentage">
                        </div>
                        <div class="form-group">
                            <label for="employee-epf">EPF %</label>
                            <input type="number" id="employee-epf" required min="0" max="100" step="0.01" value="8" placeholder="Enter EPF percentage">
                        </div>
                        <button type="submit"><i class="fas fa-save"></i> Save Employee</button>
                        <button type="reset" class="btn-secondary"><i class="fas fa-redo"></i> Reset</button>
                    </form>
                </div>

                <div class="employee-list" id="employee-list">
                    <div class="empty-state">
                        <i class="fas fa-users"></i>
                        <h3>No employees found</h3>
                        <p>Add a new employee to get started</p>
                    </div>
                </div>
            </div>

            <div id="salary" class="payroll-tab-content">
                <h3>Salary Calculation</h3>
                <div class="form-group">
                    <label for="salary-employee">Select Employee</label>
                    <select id="salary-employee" required>
                        <option value="">Select an employee</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="salary-month">Month</label>
                    <select id="salary-month" required>
                        <option value="">Select month</option>
                        <option value="0">January</option>
                        <option value="1">February</option>
                        <option value="2">March</option>
                        <option value="3">April</option>
                        <option value="4">May</option>
                        <option value="5">June</option>
                        <option value="6">July</option>
                        <option value="7">August</option>
                        <option value="8">September</option>
                        <option value="9">October</option>
                        <option value="10">November</option>
                        <option value="11">December</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="salary-year">Year</label>
                    <input type="number" id="salary-year" required min="2000" max="2100" value="2023">
                </div>

                <div id="salary-form-container" style="display: none;">
                    <h4>Monthly Details</h4>
                    <form id="salary-form" class="salary-form">
                        <div class="form-group">
                            <label for="days-worked">Days Worked</label>
                            <input type="number" id="days-worked" required min="0" max="31" placeholder="Enter days worked">
                        </div>
                        <div class="form-group">
                            <label for="leave-days">Leave Days</label>
                            <input type="number" id="leave-days" required min="0" max="31" placeholder="Enter leave days">
                        </div>
                        <div class="form-group">
                            <label for="ot-hours">OT Hours</label>
                            <input type="number" id="ot-hours" required min="0" step="0.5" placeholder="Enter OT hours">
                        </div>
                        <div class="form-group">
                            <label for="ot-rate">OT Rate (per hour)</label>
                            <input type="number" id="ot-rate" required min="0" step="0.01" placeholder="Enter OT rate per hour">
                        </div>
                        <div class="form-group">
                            <label for="bonus-percent">Bonus (%)</label>
                            <input type="number" id="bonus-percent" required min="0" max="100" step="0.01" value="0" placeholder="Enter bonus percentage">
                        </div>
                        <div class="form-group">
                            <label for="bonus-amount">Bonus Amount (LKR)</label>
                            <input type="number" id="bonus-amount" required min="0" step="0.01" value="0" placeholder="Enter bonus amount">
                        </div>
                        <div class="form-group">
                            <label for="deduction-percent">Deductions (%)</label>
                            <input type="number" id="deduction-percent" required min="0" max="100" step="0.01" value="0" placeholder="Enter deduction percentage">
                        </div>
                        <div class="form-group">
                            <label for="deduction-amount">Deduction Amount (LKR)</label>
                            <input type="number" id="deduction-amount" required min="0" step="0.01" value="0" placeholder="Enter deduction amount">
                        </div>
                        <button type="submit"><i class="fas fa-calculator"></i> Calculate Salary</button>
                        <button type="reset" class="btn-secondary"><i class="fas fa-redo"></i> Reset</button>
                    </form>

                    <div id="salary-calculations" class="salary-calculations" style="display: none;">
                        <h4>Salary Breakdown</h4>
                        <div class="calculation-row">
                            <span class="calculation-label">Basic Salary:</span>
                            <span class="calculation-value" id="calc-basic">LKR 0.00</span>
                        </div>
                        <div class="calculation-row">
                            <span class="calculation-label">OT Payment:</span>
                            <span class="calculation-value" id="calc-ot">LKR 0.00</span>
                        </div>
                        <div class="calculation-row">
                            <span class="calculation-label">Bonus:</span>
                            <span class="calculation-value" id="calc-bonus">LKR 0.00</span>
                        </div>
                        <div class="calculation-row">
                            <span class="calculation-label">ETF Deduction:</span>
                            <span class="calculation-value" id="calc-etf">LKR 0.00</span>
                        </div>
                        <div class="calculation-row">
                            <span class="calculation-label">EPF Deduction:</span>
                            <span class="calculation-value" id="calc-epf">LKR 0.00</span>
                        </div>
                        <div class="calculation-row">
                            <span class="calculation-label">Other Deductions:</span>
                            <span class="calculation-value" id="calc-deductions">LKR 0.00</span>
                        </div>
                        <div class="calculation-row">
                            <span class="calculation-label">Net Salary:</span>
                            <span class="calculation-value" id="calc-net">LKR 0.00</span>
                        </div>
                        <button id="save-salary-btn" class="btn-success"><i class="fas fa-save"></i> Save Salary Record</button>
                    </div>
                </div>
            </div>

            <div id="reports" class="payroll-tab-content">
                <h3>Payroll Reports</h3>
                <div class="form-group">
                    <label for="report-employee">Select Employee</label>
                    <select id="report-employee">
                        <option value="">Select an employee</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="report-year">Year</label>
                    <input type="number" id="report-year" min="2000" max="2100" value="2023">
                </div>
                <button id="generate-report-btn" class="btn-payroll"><i class="fas fa-file-alt"></i> Generate Report</button>

                <div id="payroll-reports" class="monthly-records">
                    <div class="empty-state">
                        <i class="fas fa-file-invoice-dollar"></i>
                        <h3>No reports found</h3>
                        <p>Select an employee and generate a report</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Business Finance Module -->
        <div id="finance-module" class="finance-module">
            <div class="finance-header">
                <h2 class="finance-title"><i class="fas fa-chart-line"></i> Business Finance Management</h2>
                <button class="back-btn" id="back-to-main-finance">
                    <i class="fas fa-arrow-left"></i> Back to Main
                </button>
            </div>

            <div class="finance-tabs">
                <div class="finance-tab active" data-finance-tab="income">
                    <i class="fas fa-plus-circle"></i> Income
                </div>
                <div class="finance-tab" data-finance-tab="expenses">
                    <i class="fas fa-minus-circle"></i> Expenses
                </div>
                <div class="finance-tab" data-finance-tab="reports">
                    <i class="fas fa-file-invoice-dollar"></i> Reports
                </div>
            </div>

            <div id="income" class="finance-tab-content active">
                <h3>Income Management</h3>
                <button id="add-income-btn" class="btn-finance">
                    <i class="fas fa-plus"></i> Add Income
                </button>

                <div id="income-form-container" style="display: none;">
                    <h4>Add New Income</h4>
                    <form id="income-form" class="finance-form">
                        <div class="form-group">
                            <label for="income-source">Source</label>
                            <select id="income-source" required>
                                <option value="">Select source</option>
                                <option value="job-completion">Job Completion</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="income-description">Description</label>
                            <input type="text" id="income-description" required placeholder="Enter description">
                        </div>
                        <div class="form-group">
                            <label for="income-amount">Amount (LKR)</label>
                            <input type="number" id="income-amount" required min="0" step="0.01" placeholder="Enter amount">
                        </div>
                        <div class="form-group">
                            <label for="income-date">Date</label>
                            <input type="date" id="income-date" required>
                        </div>
                        <div class="form-group">
                            <label for="income-month">Month</label>
                            <select id="income-month" required>
                                <option value="">Select month</option>
                                <option value="0">January</option>
                                <option value="1">February</option>
                                <option value="2">March</option>
                                <option value="3">April</option>
                                <option value="4">May</option>
                                <option value="5">June</option>
                                <option value="6">July</option>
                                <option value="7">August</option>
                                <option value="8">September</option>
                                <option value="9">October</option>
                                <option value="10">November</option>
                                <option value="11">December</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="income-year">Year</label>
                            <input type="number" id="income-year" required min="2000" max="2100" value="2023">
                        </div>
                        <button type="submit"><i class="fas fa-save"></i> Save Income</button>
                        <button type="reset" class="btn-secondary"><i class="fas fa-redo"></i> Reset</button>
                    </form>
                </div>

                <div class="finance-list" id="income-list">
                    <div class="empty-state">
                        <i class="fas fa-plus-circle"></i>
                        <h3>No income records found</h3>
                        <p>Add income records to get started</p>
                    </div>
                </div>
            </div>

            <div id="expenses" class="finance-tab-content">
                <h3>Expense Management</h3>
                <button id="add-expense-btn" class="btn-finance">
                    <i class="fas fa-plus"></i> Add Expense
                </button>

                <div id="expense-form-container" style="display: none;">
                    <h4>Add New Expense</h4>
                    <form id="expense-form" class="finance-form">
                        <div class="form-group">
                            <label for="expense-source">Source</label>
                            <select id="expense-source" required>
                                <option value="">Select source</option>
                                <option value="payroll">Payroll</option>
                                <option value="other">Other</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="expense-description">Description</label>
                            <input type="text" id="expense-description" required placeholder="Enter description">
                        </div>
                        <div class="form-group">
                            <label for="expense-amount">Amount (LKR)</label>
                            <input type="number" id="expense-amount" required min="0" step="0.01" placeholder="Enter amount">
                        </div>
                        <div class="form-group">
                            <label for="expense-date">Date</label>
                            <input type="date" id="expense-date" required>
                        </div>
                        <div class="form-group">
                            <label for="expense-month">Month</label>
                            <select id="expense-month" required>
                                <option value="">Select month</option>
                                <option value="0">January</option>
                                <option value="1">February</option>
                                <option value="2">March</option>
                                <option value="3">April</option>
                                <option value="4">May</option>
                                <option value="5">June</option>
                                <option value="6">July</option>
                                <option value="7">August</option>
                                <option value="8">September</option>
                                <option value="9">October</option>
                                <option value="10">November</option>
                                <option value="11">December</option>
                            </select>
                        </div>
                        <div class="form-group">
                            <label for="expense-year">Year</label>
                            <input type="number" id="expense-year" required min="2000" max="2100" value="2023">
                        </div>
                        <button type="submit"><i class="fas fa-save"></i> Save Expense</button>
                        <button type="reset" class="btn-secondary"><i class="fas fa-redo"></i> Reset</button>
                    </form>
                </div>

                <div class="finance-list" id="expense-list">
                    <div class="empty-state">
                        <i class="fas fa-minus-circle"></i>
                        <h3>No expense records found</h3>
                        <p>Add expense records to get started</p>
                    </div>
                </div>
            </div>

            <div id="reports" class="finance-tab-content">
                <h3>Financial Reports</h3>
                <div class="form-group">
                    <label for="report-month">Month</label>
                    <select id="report-month" required>
                        <option value="">Select month</option>
                        <option value="0">January</option>
                        <option value="1">February</option>
                        <option value="2">March</option>
                        <option value="3">April</option>
                        <option value="4">May</option>
                        <option value="5">June</option>
                        <option value="6">July</option>
                        <option value="7">August</option>
                        <option value="8">September</option>
                        <option value="9">October</option>
                        <option value="10">November</option>
                        <option value="11">December</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="report-year">Year</label>
                    <input type="number" id="report-year" required min="2000" max="2100" value="2023">
                </div>
                <button id="generate-finance-report-btn" class="btn-finance"><i class="fas fa-file-alt"></i> Generate Report</button>

                <div id="finance-reports" class="monthly-records">
                    <div class="empty-state">
                        <i class="fas fa-file-invoice-dollar"></i>
                        <h3>No reports found</h3>
                        <p>Select a month and year to generate a report</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Job Details Modal -->
        <div id="job-modal" class="modal">
            <div class="modal-content">
                <span class="close-modal">&times;</span>
                <div id="job-details">
                    <!-- Job details will be loaded here -->
                </div>
            </div>
        </div>

        <!-- Invoice Modal -->
        <div id="invoice-modal" class="modal">
            <div class="modal-content">
                <span class="close-modal">&times;</span>
                <div id="invoice-content">
                    <!-- Invoice content will be loaded here -->
                </div>
            </div>
        </div>

        <!-- Employee Details Modal -->
        <div id="employee-modal" class="modal">
            <div class="modal-content">
                <span class="close-modal">&times;</span>
                <div id="employee-details">
                    <!-- Employee details will be loaded here -->
                </div>
            </div>
        </div>

        <!-- Finance Details Modal -->
        <div id="finance-modal" class="modal">
            <div class="modal-content">
                <span class="close-modal">&times;</span>
                <div id="finance-details">
                    <!-- Finance details will be loaded here -->
                </div>
            </div>
        </div>

        <div id="notification" class="notification"></div>

        <script>
            document.addEventListener('DOMContentLoaded', function() {
                // Initialize the app
                const tabs = document.querySelectorAll('.tab');
                const tabContents = document.querySelectorAll('.tab-content');
                const jobForm = document.getElementById('job-form');
                const pendingJobsContainer = document.getElementById('pending-jobs');
                const completedJobsContainer = document.getElementById('completed-jobs');
                const pendingCount = document.getElementById('pending-count');
                const completedCount = document.getElementById('completed-count');
                const invoicesList = document.getElementById('invoices-list');
                const notification = document.getElementById('notification');
                const jobModal = document.getElementById('job-modal');
                const invoiceModal = document.getElementById('invoice-modal');
                const closeModalButtons = document.querySelectorAll('.close-modal');
                const fileInput = document.getElementById('job-files');
                const filePreview = document.getElementById('file-preview');
                const invoiceJobSelect = document.getElementById('invoice-job');
                const generateInvoiceBtn = document.getElementById('generate-invoice-btn');
                
                // Dashboard filters
                const searchInput = document.getElementById('search-input');
                const categoryFilter = document.getElementById('category-filter');
                const deadlineFrom = document.getElementById('deadline-from');
                const deadlineTo = document.getElementById('deadline-to');
                const minCost = document.getElementById('min-cost');
                const maxCost = document.getElementById('max-cost');
                const resetDashboardFiltersBtn = document.getElementById('reset-dashboard-filters');
                
                // Filter elements
                const filterCategory = document.getElementById('filter-category');
                const filterStatus = document.getElementById('filter-status');
                const filterDateFrom = document.getElementById('filter-date-from');
                const filterDateTo = document.getElementById('filter-date-to');
                const applyFilterBtn = document.getElementById('apply-filter');
                const resetFilterBtn = document.getElementById('reset-filter');
                const reportTableBody = document.getElementById('report-table-body');
                
                // Chart variables
                let completionChart = null;
                
                // File storage
                let uploadedFiles = [];
                
                // Load data from local storage
                let jobs = JSON.parse(localStorage.getItem('jobs')) || [];
                let invoices = JSON.parse(localStorage.getItem('invoices')) || [];
                let comments = JSON.parse(localStorage.getItem('comments')) || {};
                let nextInvoiceNumber = parseInt(localStorage.getItem('nextInvoiceNumber')) || 1;
                
                // Payroll data
                let employees = JSON.parse(localStorage.getItem('employees')) || [];
                let salaryRecords = JSON.parse(localStorage.getItem('salaryRecords')) || [];
                
                // Business Finance data
                let incomeRecords = JSON.parse(localStorage.getItem('incomeRecords')) || [];
                let expenseRecords = JSON.parse(localStorage.getItem('expenseRecords')) || [];
                
                // Payroll elements
                const payrollBtn = document.getElementById('payroll-btn');
                const financeBtn = document.getElementById('finance-btn');
                const backToMainBtn = document.getElementById('back-to-main');
                const backToMainFinanceBtn = document.getElementById('back-to-main-finance');
                const mainApp = document.getElementById('main-app');
                const payrollModule = document.getElementById('payroll-module');
                const financeModule = document.getElementById('finance-module');
                const payrollTabs = document.querySelectorAll('.payroll-tab');
                const payrollTabContents = document.querySelectorAll('.payroll-tab-content');
                const addEmployeeBtn = document.getElementById('add-employee-btn');
                const employeeFormContainer = document.getElementById('employee-form-container');
                const employeeForm = document.getElementById('employee-form');
                const employeeList = document.getElementById('employee-list');
                const salaryEmployee = document.getElementById('salary-employee');
                const salaryMonth = document.getElementById('salary-month');
                const salaryYear = document.getElementById('salary-year');
                const salaryFormContainer = document.getElementById('salary-form-container');
                const salaryForm = document.getElementById('salary-form');
                const salaryCalculations = document.getElementById('salary-calculations');
                const saveSalaryBtn = document.getElementById('save-salary-btn');
                const reportEmployee = document.getElementById('report-employee');
                const reportYear = document.getElementById('report-year');
                const generateReportBtn = document.getElementById('generate-report-btn');
                const payrollReports = document.getElementById('payroll-reports');
                const employeeModal = document.getElementById('employee-modal');
                
                // Business Finance elements
                const financeTabs = document.querySelectorAll('.finance-tab');
                const financeTabContents = document.querySelectorAll('.finance-tab-content');
                const addIncomeBtn = document.getElementById('add-income-btn');
                const incomeFormContainer = document.getElementById('income-form-container');
                const incomeForm = document.getElementById('income-form');
                const incomeList = document.getElementById('income-list');
                const addExpenseBtn = document.getElementById('add-expense-btn');
                const expenseFormContainer = document.getElementById('expense-form-container');
                const expenseForm = document.getElementById('expense-form');
                const expenseList = document.getElementById('expense-list');
                const financeReportMonth = document.getElementById('report-month');
                const financeReportYear = document.getElementById('report-year');
                const generateFinanceReportBtn = document.getElementById('generate-finance-report-btn');
                const financeReports = document.getElementById('finance-reports');
                const financeModal = document.getElementById('finance-modal');
                
                // Display jobs on page load
                displayJobs();
                displayInvoices();
                updateInvoiceJobSelect();
                
                // Initialize payroll
                updateEmployeeSelects();
                displayEmployees();
                
                // Initialize business finance
                displayIncome();
                displayExpenses();
                
                // Tab switching
                tabs.forEach(tab => {
                    tab.addEventListener('click', () => {
                        const tabId = tab.getAttribute('data-tab');
                        
                        // Remove active class from all tabs and contents
                        tabs.forEach(t => t.classList.remove('active'));
                        tabContents.forEach(c => c.classList.remove('active'));
                        
                        // Add active class to clicked tab and corresponding content
                        tab.classList.add('active');
                        document.getElementById(tabId).classList.add('active');
                        
                        // Initialize chart if reports tab is selected
                        if (tabId === 'reports') {
                            initializeChart();
                        }
                    });
                });
                
                // Payroll tab switching
                payrollTabs.forEach(tab => {
                    tab.addEventListener('click', () => {
                        const tabId = tab.getAttribute('data-payroll-tab');
                        
                        // Remove active class from all tabs and contents
                        payrollTabs.forEach(t => t.classList.remove('active'));
                        payrollTabContents.forEach(c => c.classList.remove('active'));
                        
                        // Add active class to clicked tab and corresponding content
                        tab.classList.add('active');
                        document.getElementById(tabId).classList.add('active');
                    });
                });
                
                // Business Finance tab switching
                financeTabs.forEach(tab => {
                    tab.addEventListener('click', () => {
                        const tabId = tab.getAttribute('data-finance-tab');
                        
                        // Remove active class from all tabs and contents
                        financeTabs.forEach(t => t.classList.remove('active'));
                        financeTabContents.forEach(c => c.classList.remove('active'));
                        
                        // Add active class to clicked tab and corresponding content
                        tab.classList.add('active');
                        document.getElementById(tabId).classList.add('active');
                    });
                });
                
                // Payroll button
                payrollBtn.addEventListener('click', () => {
                    mainApp.style.display = 'none';
                    financeModule.classList.remove('active');
                    payrollModule.classList.add('active');
                });
                
                // Business Finance button
                financeBtn.addEventListener('click', () => {
                    mainApp.style.display = 'none';
                    payrollModule.classList.remove('active');
                    financeModule.classList.add('active');
                });
                
                // Back to main buttons
                backToMainBtn.addEventListener('click', () => {
                    payrollModule.classList.remove('active');
                    financeModule.classList.remove('active');
                    mainApp.style.display = 'block';
                });
                
                backToMainFinanceBtn.addEventListener('click', () => {
                    financeModule.classList.remove('active');
                    payrollModule.classList.remove('active');
                    mainApp.style.display = 'block';
                });
                
                // Close modal buttons
                closeModalButtons.forEach(button => {
                    button.addEventListener('click', () => {
                        jobModal.style.display = 'none';
                        invoiceModal.style.display = 'none';
                        employeeModal.style.display = 'none';
                        financeModal.style.display = 'none';
                    });
                });
                
                // Close modal when clicking outside
                window.addEventListener('click', (e) => {
                    if (e.target === jobModal) {
                        jobModal.style.display = 'none';
                    }
                    if (e.target === invoiceModal) {
                        invoiceModal.style.display = 'none';
                    }
                    if (e.target === employeeModal) {
                        employeeModal.style.display = 'none';
                    }
                    if (e.target === financeModal) {
                        financeModal.style.display = 'none';
                    }
                });
                
                // Dashboard filters
                searchInput.addEventListener('input', filterDashboardJobs);
                categoryFilter.addEventListener('change', filterDashboardJobs);
                deadlineFrom.addEventListener('change', filterDashboardJobs);
                deadlineTo.addEventListener('change', filterDashboardJobs);
                minCost.addEventListener('change', filterDashboardJobs);
                maxCost.addEventListener('change', filterDashboardJobs);
                
                // Reset dashboard filters
                resetDashboardFiltersBtn.addEventListener('click', () => {
                    searchInput.value = '';
                    categoryFilter.value = '';
                    deadlineFrom.value = '';
                    deadlineTo.value = '';
                    minCost.value = '';
                    maxCost.value = '';
                    filterDashboardJobs();
                });
                
                // File upload preview
                fileInput.addEventListener('change', function(e) {
                    const files = e.target.files;
                    filePreview.innerHTML = '';
                    uploadedFiles = [];
                    
                    for (let i = 0; i < files.length; i++) {
                        const file = files[i];
                        const reader = new FileReader();
                        
                        reader.onload = function(event) {
                            const fileData = {
                                name: file.name,
                                type: file.type,
                                size: file.size,
                                data: event.target.result
                            };
                            
                            uploadedFiles.push(fileData);
                            
                            const fileItem = document.createElement('div');
                            fileItem.className = 'file-item';
                            
                            if (file.type.startsWith('image/')) {
                                fileItem.innerHTML = `
                                    <img src="${event.target.result}" alt="${file.name}">
                                    <div class="remove-file" data-index="${uploadedFiles.length - 1}"><i class="fas fa-times"></i></div>
                                `;
                            } else {
                                fileItem.innerHTML = `
                                    <div style="display: flex; align-items: center; justify-content: center; height: 100%; background-color: #f2f2f2;">
                                        <i class="fas fa-file" style="font-size: 2rem; color: #777;"></i>
                                    </div>
                                    <div class="remove-file" data-index="${uploadedFiles.length - 1}"><i class="fas fa-times"></i></div>
                                `;
                            }
                            
                            filePreview.appendChild(fileItem);
                            
                            // Add event listener to remove file
                            const removeBtn = fileItem.querySelector('.remove-file');
                            removeBtn.addEventListener('click', function() {
                                const index = parseInt(this.getAttribute('data-index'));
                                uploadedFiles.splice(index, 1);
                                fileItem.remove();
                            });
                        };
                        
                        reader.readAsDataURL(file);
                    }
                });
                
                // Add new job
                jobForm.addEventListener('submit', function(e) {
                    e.preventDefault();
                    
                    const title = document.getElementById('job-title').value;
                    const description = document.getElementById('job-description').value;
                    const category = document.getElementById('job-category').value;
                    const deadline = document.getElementById('job-deadline').value;
                    const cost = parseFloat(document.getElementById('job-cost').value);
                    
                    const now = new Date();
                    const startTime = now.toISOString();
                    
                    const newJob = {
                        id: Date.now(),
                        title,
                        description,
                        category,
                        deadline,
                        cost,
                        completed: false,
                        startTime,
                        endTime: null,
                        createdAt: now.toISOString(),
                        files: uploadedFiles
                    };
                    
                    jobs.push(newJob);
                    saveJobs();
                    displayJobs();
                    updateInvoiceJobSelect();
                    
                    // Reset form
                    jobForm.reset();
                    filePreview.innerHTML = '';
                    uploadedFiles = [];
                    
                    // Show notification
                    showNotification('Job added successfully!');
                    
                    // Switch to dashboard tab
                    document.querySelector('[data-tab="dashboard"]').click();
                });
                
                // Generate invoice button
                generateInvoiceBtn.addEventListener('click', function() {
                    const jobId = parseInt(invoiceJobSelect.value);
                    if (jobId) {
                        generateInvoice(jobId);
                    } else {
                        showNotification('Please select a job to generate an invoice', 'error');
                    }
                });
                
                // Apply filter button
                applyFilterBtn.addEventListener('click', function() {
                    applyFilters();
                });
                
                // Reset filter button
                resetFilterBtn.addEventListener('click', function() {
                    filterCategory.value = '';
                    filterStatus.value = '';
                    filterDateFrom.value = '';
                    filterDateTo.value = '';
                    applyFilters();
                });
                
                // Payroll functions
                // Add employee button
                addEmployeeBtn.addEventListener('click', () => {
                    employeeFormContainer.style.display = employeeFormContainer.style.display === 'none' ? 'block' : 'none';
                });
                
                // Add employee form
                employeeForm.addEventListener('submit', (e) => {
                    e.preventDefault();
                    
                    const employeeNumber = document.getElementById('employee-number').value;
                    const name = document.getElementById('employee-name').value;
                    const address = document.getElementById('employee-address').value;
                    const age = parseInt(document.getElementById('employee-age').value);
                    const dob = document.getElementById('employee-dob').value;
                    const mobile = document.getElementById('employee-mobile').value;
                    const basicSalary = parseFloat(document.getElementById('employee-basic-salary').value);
                    const etf = parseFloat(document.getElementById('employee-etf').value);
                    const epf = parseFloat(document.getElementById('employee-epf').value);
                    
                    const newEmployee = {
                        id: Date.now(),
                        employeeNumber,
                        name,
                        address,
                        age,
                        dob,
                        mobile,
                        basicSalary,
                        etf,
                        epf
                    };
                    
                    employees.push(newEmployee);
                    saveEmployees();
                    displayEmployees();
                    updateEmployeeSelects();
                    
                    // Reset form
                    employeeForm.reset();
                    employeeFormContainer.style.display = 'none';
                    
                    showNotification('Employee added successfully!');
                });
                
                // Salary employee select
                salaryEmployee.addEventListener('change', () => {
                    if (salaryEmployee.value && salaryMonth.value && salaryYear.value) {
                        salaryFormContainer.style.display = 'block';
                    } else {
                        salaryFormContainer.style.display = 'none';
                    }
                });
                
                // Salary month select
                salaryMonth.addEventListener('change', () => {
                    if (salaryEmployee.value && salaryMonth.value && salaryYear.value) {
                        salaryFormContainer.style.display = 'block';
                    } else {
                        salaryFormContainer.style.display = 'none';
                    }
                });
                
                // Salary year input
                salaryYear.addEventListener('change', () => {
                    if (salaryEmployee.value && salaryMonth.value && salaryYear.value) {
                        salaryFormContainer.style.display = 'block';
                    } else {
                        salaryFormContainer.style.display = 'none';
                    }
                });
                
                // Salary form
                salaryForm.addEventListener('submit', (e) => {
                    e.preventDefault();
                    
                    const employeeId = parseInt(salaryEmployee.value);
                    const employee = employees.find(emp => emp.id === employeeId);
                    
                    if (!employee) {
                        showNotification('Employee not found', 'error');
                        return;
                    }
                    
                    const month = parseInt(salaryMonth.value);
                    const year = parseInt(salaryYear.value);
                    const daysWorked = parseInt(document.getElementById('days-worked').value);
                    const leaveDays = parseInt(document.getElementById('leave-days').value);
                    const otHours = parseFloat(document.getElementById('ot-hours').value);
                    const otRate = parseFloat(document.getElementById('ot-rate').value);
                    const bonusPercent = parseFloat(document.getElementById('bonus-percent').value);
                    const bonusAmount = parseFloat(document.getElementById('bonus-amount').value);
                    const deductionPercent = parseFloat(document.getElementById('deduction-percent').value);
                    const deductionAmount = parseFloat(document.getElementById('deduction-amount').value);
                    
                    // Calculate salary
                    const workingDays = 26; // Standard working days per month
                    const dailyRate = employee.basicSalary / workingDays;
                    const basicSalary = dailyRate * daysWorked;
                    
                    const otPayment = otHours * otRate;
                    const bonus = (basicSalary * bonusPercent / 100) + bonusAmount;
                    const deductions = (basicSalary * deductionPercent / 100) + deductionAmount;
                    const etfDeduction = basicSalary * employee.etf / 100;
                    const epfDeduction = basicSalary * employee.epf / 100;
                    const netSalary = basicSalary + otPayment + bonus - deductions - etfDeduction - epfDeduction;
                    
                    // Display calculations
                    document.getElementById('calc-basic').textContent = `LKR ${basicSalary.toFixed(2)}`;
                    document.getElementById('calc-ot').textContent = `LKR ${otPayment.toFixed(2)}`;
                    document.getElementById('calc-bonus').textContent = `LKR ${bonus.toFixed(2)}`;
                    document.getElementById('calc-etf').textContent = `LKR ${etfDeduction.toFixed(2)}`;
                    document.getElementById('calc-epf').textContent = `LKR ${epfDeduction.toFixed(2)}`;
                    document.getElementById('calc-deductions').textContent = `LKR ${deductions.toFixed(2)}`;
                    document.getElementById('calc-net').textContent = `LKR ${netSalary.toFixed(2)}`;
                    
                    salaryCalculations.style.display = 'block';
                    
                    // Store calculation data for saving
                    window.currentSalaryCalculation = {
                        employeeId,
                        employee,
                        month,
                        year,
                        daysWorked,
                        leaveDays,
                        otHours,
                        otRate,
                        bonusPercent,
                        bonusAmount,
                        deductionPercent,
                        deductionAmount,
                        basicSalary,
                        otPayment,
                        bonus,
                        deductions,
                        etfDeduction,
                        epfDeduction,
                        netSalary
                    };
                });
                
                // Save salary button
                saveSalaryBtn.addEventListener('click', () => {
                    if (!window.currentSalaryCalculation) {
                        showNotification('No salary calculation to save', 'error');
                        return;
                    }
                    
                    const calculation = window.currentSalaryCalculation;
                    
                    // Check if record already exists
                    const existingRecordIndex = salaryRecords.findIndex(record => 
                        record.employeeId === calculation.employeeId && 
                        record.month === calculation.month && 
                        record.year === calculation.year
                    );
                    
                    const salaryRecord = {
                        id: existingRecordIndex >= 0 ? salaryRecords[existingRecordIndex].id : Date.now(),
                        employeeId: calculation.employeeId,
                        employeeName: calculation.employee.name,
                        employeeNumber: calculation.employee.employeeNumber,
                        month: calculation.month,
                        year: calculation.year,
                        daysWorked: calculation.daysWorked,
                        leaveDays: calculation.leaveDays,
                        otHours: calculation.otHours,
                        otRate: calculation.otRate,
                        otPayment: calculation.otPayment,
                        bonusPercent: calculation.bonusPercent,
                        bonusAmount: calculation.bonusAmount,
                        bonus: calculation.bonus,
                        deductionPercent: calculation.deductionPercent,
                        deductionAmount: calculation.deductionAmount,
                        deductions: calculation.deductions,
                        etfPercent: calculation.employee.etf,
                        etfDeduction: calculation.etfDeduction,
                        epfPercent: calculation.employee.epf,
                        epfDeduction: calculation.epfDeduction,
                        basicSalary: calculation.basicSalary,
                        netSalary: calculation.netSalary,
                        createdAt: new Date().toISOString()
                    };
                    
                    if (existingRecordIndex >= 0) {
                        // Update existing record
                        salaryRecords[existingRecordIndex] = salaryRecord;
                        showNotification('Salary record updated successfully!');
                    } else {
                        // Add new record
                        salaryRecords.push(salaryRecord);
                        showNotification('Salary record saved successfully!');
                    }
                    
                    saveSalaryRecords();
                    
                    // Add expense record for business finance
                    addPayrollExpense(calculation);
                    
                    // Reset form
                    salaryForm.reset();
                    salaryCalculations.style.display = 'none';
                    salaryFormContainer.style.display = 'none';
                    salaryEmployee.value = '';
                    salaryMonth.value = '';
                    salaryYear.value = new Date().getFullYear();
                    
                    // Clear calculation data
                    window.currentSalaryCalculation = null;
                });
                
                // Generate report button
                generateReportBtn.addEventListener('click', () => {
                    const employeeId = parseInt(reportEmployee.value);
                    const year = parseInt(reportYear.value);
                    
                    if (!employeeId || !year) {
                        showNotification('Please select an employee and year', 'error');
                        return;
                    }
                    
                    const employee = employees.find(emp => emp.id === employeeId);
                    if (!employee) {
                        showNotification('Employee not found', 'error');
                        return;
                    }
                    
                    // Filter salary records for the selected employee and year
                    const employeeRecords = salaryRecords.filter(record => 
                        record.employeeId === employeeId && record.year === year
                    );
                    
                    if (employeeRecords.length === 0) {
                        payrollReports.innerHTML = `
                            <div class="empty-state">
                                <i class="fas fa-file-invoice-dollar"></i>
                                <h3>No records found</h3>
                                <p>No salary records found for ${employee.name} in ${year}</p>
                            </div>
                        `;
                        return;
                    }
                    
                    // Sort records by month
                    employeeRecords.sort((a, b) => a.month - b.month);
                    
                    // Generate report HTML
                    const monthNames = [
                        'January', 'February', 'March', 'April', 'May', 'June',
                        'July', 'August', 'September', 'October', 'November', 'December'
                    ];
                    
                    const reportHtml = employeeRecords.map(record => `
                        <div class="record-card">
                            <div class="record-header">
                                <div class="record-month">${monthNames[record.month]} ${record.year}</div>
                                <div class="record-year">${record.netSalary > 0 ? 'Paid' : 'Unpaid'}</div>
                            </div>
                            <div class="record-details">
                                <div class="record-detail">
                                    <i class="fas fa-calendar"></i>
                                    <span>Days Worked: ${record.daysWorked}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-calendar-times"></i>
                                    <span>Leave Days: ${record.leaveDays}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-clock"></i>
                                    <span>OT Hours: ${record.otHours}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-money-bill-wave"></i>
                                    <span>Basic Salary: LKR ${record.basicSalary.toFixed(2)}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-plus-circle"></i>
                                    <span>Bonus: LKR ${record.bonus.toFixed(2)}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-minus-circle"></i>
                                    <span>Deductions: LKR ${record.deductions.toFixed(2)}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-piggy-bank"></i>
                                    <span>ETF: LKR ${record.etfDeduction.toFixed(2)}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-piggy-bank"></i>
                                    <span>EPF: LKR ${record.epfDeduction.toFixed(2)}</span>
                                </div>
                                <div class="record-detail">
                                    <i class="fas fa-money-check-alt"></i>
                                    <span>Net Salary: LKR ${record.netSalary.toFixed(2)}</span>
                                </div>
                            </div>
                            <div class="record-actions">
                                <button class="btn-secondary" data-id="${record.id}" data-action="view-salary">
                                    <i class="fas fa-eye"></i> View
                                </button>
                                <button class="btn-secondary" data-id="${record.id}" data-action="download-salary">
                                    <i class="fas fa-download"></i> PDF
                                </button>
                            </div>
                        </div>
                    `).join('');
                    
                    payrollReports.innerHTML = reportHtml;
                    
                    // Add event listeners to buttons
                    const viewButtons = payrollReports.querySelectorAll('[data-action="view-salary"]');
                    const downloadButtons = payrollReports.querySelectorAll('[data-action="download-salary"]');
                    
                    viewButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const recordId = parseInt(button.getAttribute('data-id'));
                            viewSalaryRecord(recordId);
                        });
                    });
                    
                    downloadButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const recordId = parseInt(button.getAttribute('data-id'));
                            downloadSalaryRecordAsPDF(recordId);
                        });
                    });
                });
                
                // Business Finance functions
                // Add income button
                addIncomeBtn.addEventListener('click', () => {
                    incomeFormContainer.style.display = incomeFormContainer.style.display === 'none' ? 'block' : 'none';
                });
                
                // Add income form
                incomeForm.addEventListener('submit', (e) => {
                    e.preventDefault();
                    
                    const source = document.getElementById('income-source').value;
                    const description = document.getElementById('income-description').value;
                    const amount = parseFloat(document.getElementById('income-amount').value);
                    const date = document.getElementById('income-date').value;
                    const month = parseInt(document.getElementById('income-month').value);
                    const year = parseInt(document.getElementById('income-year').value);
                    
                    const newIncome = {
                        id: Date.now(),
                        source,
                        description,
                        amount,
                        date,
                        month,
                        year,
                        createdAt: new Date().toISOString()
                    };
                    
                    incomeRecords.push(newIncome);
                    saveIncomeRecords();
                    displayIncome();
                    
                    // Reset form
                    incomeForm.reset();
                    incomeFormContainer.style.display = 'none';
                    
                    showNotification('Income record added successfully!');
                });
                
                // Add expense button
                addExpenseBtn.addEventListener('click', () => {
                    expenseFormContainer.style.display = expenseFormContainer.style.display === 'none' ? 'block' : 'none';
                });
                
                // Add expense form
                expenseForm.addEventListener('submit', (e) => {
                    e.preventDefault();
                    
                    const source = document.getElementById('expense-source').value;
                    const description = document.getElementById('expense-description').value;
                    const amount = parseFloat(document.getElementById('expense-amount').value);
                    const date = document.getElementById('expense-date').value;
                    const month = parseInt(document.getElementById('expense-month').value);
                    const year = parseInt(document.getElementById('expense-year').value);
                    
                    const newExpense = {
                        id: Date.now(),
                        source,
                        description,
                        amount,
                        date,
                        month,
                        year,
                        createdAt: new Date().toISOString()
                    };
                    
                    expenseRecords.push(newExpense);
                    saveExpenseRecords();
                    displayExpenses();
                    
                    // Reset form
                    expenseForm.reset();
                    expenseFormContainer.style.display = 'none';
                    
                    showNotification('Expense record added successfully!');
                });
                
                // Generate finance report button
                generateFinanceReportBtn.addEventListener('click', () => {
                    const month = parseInt(financeReportMonth.value);
                    const year = parseInt(financeReportYear.value);
                    
                    if (isNaN(month) || !year) {
                        showNotification('Please select a valid month and year', 'error');
                        return;
                    }
                    
                    generateFinanceReport(month, year);
                });
                
                // Function to generate finance report
                function generateFinanceReport(month, year) {
                    // Filter income records for the selected month and year
                    const monthIncome = incomeRecords.filter(record => 
                        record.month === month && record.year === year
                    );
                    
                    // Filter expense records for the selected month and year
                    const monthExpenses = expenseRecords.filter(record => 
                        record.month === month && record.year === year
                    );
                    
                    // Calculate totals
                    const totalIncome = monthIncome.reduce((sum, record) => sum + record.amount, 0);
                    const totalExpenses = monthExpenses.reduce((sum, record) => sum + record.amount, 0);
                    const profitLoss = totalIncome - totalExpenses;
                    
                    const monthNames = [
                        'January', 'February', 'March', 'April', 'May', 'June',
                        'July', 'August', 'September', 'October', 'November', 'December'
                    ];
                    
                    // Generate report HTML
                    const reportHtml = `
                        <div class="finance-report">
                            <div class="report-header">
                                <div class="report-title">Financial Report</div>
                                <div class="report-period">${monthNames[month]} ${year}</div>
                            </div>
                            
                            <div class="report-summary">
                                <div class="report-summary-item">
                                    <div class="report-summary-label">Total Income</div>
                                    <div class="report-summary-value income">LKR ${totalIncome.toFixed(2)}</div>
                                </div>
                                <div class="report-summary-item">
                                    <div class="report-summary-label">Total Expenses</div>
                                    <div class="report-summary-value expense">LKR ${totalExpenses.toFixed(2)}</div>
                                </div>
                                <div class="report-summary-item">
                                    <div class="report-summary-label">Net ${profitLoss >= 0 ? 'Profit' : 'Loss'}</div>
                                    <div class="report-summary-value ${profitLoss >= 0 ? 'profit' : 'loss'}">LKR ${Math.abs(profitLoss).toFixed(2)}</div>
                                </div>
                            </div>
                            
                            <div class="report-details">
                                <div class="report-section">
                                    <div class="report-section-title income">
                                        <i class="fas fa-plus-circle"></i> Income Sources
                                    </div>
                                    ${monthIncome.length === 0 ? 
                                        '<div class="empty-state">No income records for this period</div>' :
                                        monthIncome.map(record => `
                                            <div class="report-item">
                                                <div class="report-item-description">${record.description}</div>
                                                <div class="report-item-amount income">LKR ${record.amount.toFixed(2)}</div>
                                            </div>
                                        `).join('')
                                    }
                                </div>
                                
                                <div class="report-section">
                                    <div class="report-section-title expense">
                                        <i class="fas fa-minus-circle"></i> Expense Sources
                                    </div>
                                    ${monthExpenses.length === 0 ? 
                                        '<div class="empty-state">No expense records for this period</div>' :
                                        monthExpenses.map(record => `
                                            <div class="report-item">
                                                <div class="report-item-description">${record.description}</div>
                                                <div class="report-item-amount expense">LKR ${record.amount.toFixed(2)}</div>
                                            </div>
                                        `).join('')
                                    }
                                </div>
                            </div>
                            
                            <div style="text-align: center; margin-top: 20px;">
                                <button class="btn-finance" onclick="downloadFinanceReportAsPDF(${month}, ${year})">
                                    <i class="fas fa-download"></i> Download PDF
                                </button>
                            </div>
                        </div>
                    `;
                    
                    financeReports.innerHTML = reportHtml;
                }
                
                // Function to download finance report as PDF
                window.downloadFinanceReportAsPDF = function(month, year) {
                    const { jsPDF } = window.jspdf;
                    const doc = new jsPDF();
                    
                    const monthNames = [
                        'January', 'February', 'March', 'April', 'May', 'June',
                        'July', 'August', 'September', 'October', 'November', 'December'
                    ];
                    
                    // Filter income records for the selected month and year
                    const monthIncome = incomeRecords.filter(record => 
                        record.month === month && record.year === year
                    );
                    
                    // Filter expense records for the selected month and year
                    const monthExpenses = expenseRecords.filter(record => 
                        record.month === month && record.year === year
                    );
                    
                    // Calculate totals
                    const totalIncome = monthIncome.reduce((sum, record) => sum + record.amount, 0);
                    const totalExpenses = monthExpenses.reduce((sum, record) => sum + record.amount, 0);
                    const profitLoss = totalIncome - totalExpenses;
                    
                    // Add title
                    doc.setFontSize(20);
                    doc.text('Financial Report', 105, 20, { align: 'center' });
                    
                    // Add period
                    doc.setFontSize(14);
                    doc.text(`Period: ${monthNames[month]} ${year}`, 105, 35, { align: 'center' });
                    
                    // Add summary
                    doc.setFontSize(12);
                    doc.text('Summary:', 20, 55);
                    doc.text(`Total Income: LKR ${totalIncome.toFixed(2)}`, 20, 65);
                    doc.text(`Total Expenses: LKR ${totalExpenses.toFixed(2)}`, 20, 75);
                    doc.text(`Net ${profitLoss >= 0 ? 'Profit' : 'Loss'}: LKR ${Math.abs(profitLoss).toFixed(2)}`, 20, 85);
                    
                    // Add income details
                    doc.text('Income Sources:', 20, 105);
                    let yPos = 115;
                    monthIncome.forEach(record => {
                        doc.text(`${record.description}: LKR ${record.amount.toFixed(2)}`, 25, yPos);
                        yPos += 10;
                    });
                    
                    // Add expense details
                    yPos += 10;
                    doc.text('Expense Sources:', 20, yPos);
                    yPos += 10;
                    monthExpenses.forEach(record => {
                        doc.text(`${record.description}: LKR ${record.amount.toFixed(2)}`, 25, yPos);
                        yPos += 10;
                    });
                    
                    // Save the PDF
                    doc.save(`financial-report-${monthNames[month]}-${year}.pdf`);
                    
                    showNotification('Financial report downloaded as PDF!');
                };
                
                // Function to add payroll expense to business finance
                function addPayrollExpense(calculation) {
                    const month = calculation.month;
                    const year = calculation.year;
                    
                    // Check if payroll expense already exists for this month
                    const existingPayrollExpense = expenseRecords.find(record => 
                        record.source === 'payroll' && 
                        record.month === month && 
                        record.year === year
                    );
                    
                    if (existingPayrollExpense) {
                        // Update existing payroll expense
                        existingPayrollExpense.amount = calculation.netSalary;
                        saveExpenseRecords();
                    } else {
                        // Add new payroll expense
                        const payrollExpense = {
                            id: Date.now(),
                            source: 'payroll',
                            description: `Payroll for ${calculation.employee.name}`,
                            amount: calculation.netSalary,
                            date: new Date().toISOString().split('T')[0],
                            month: month,
                            year: year,
                            createdAt: new Date().toISOString()
                        };
                        
                        expenseRecords.push(payrollExpense);
                        saveExpenseRecords();
                    }
                }
                
                // Function to add job completion income automatically
                function addJobCompletionIncome(invoice) {
                    const job = jobs.find(j => j.id === invoice.jobId);
                    if (!job) return;
                    
                    const date = new Date(invoice.date);
                    const month = date.getMonth();
                    const year = date.getFullYear();
                    
                    const jobIncome = {
                        id: Date.now(),
                        source: 'job-completion',
                        description: `Payment for job: ${job.title}`,
                        amount: job.cost,
                        date: date.toISOString().split('T')[0],
                        month: month,
                        year: year,
                        createdAt: new Date().toISOString()
                    };
                    
                    incomeRecords.push(jobIncome);
                    saveIncomeRecords();
                }
                
                // Function to save jobs to local storage
                function saveJobs() {
                    localStorage.setItem('jobs', JSON.stringify(jobs));
                }
                
                // Function to save comments to local storage
                function saveComments() {
                    localStorage.setItem('comments', JSON.stringify(comments));
                }
                
                // Function to save invoices to local storage
                function saveInvoices() {
                    localStorage.setItem('invoices', JSON.stringify(invoices));
                    localStorage.setItem('nextInvoiceNumber', nextInvoiceNumber.toString());
                }
                
                // Function to save employees to local storage
                function saveEmployees() {
                    localStorage.setItem('employees', JSON.stringify(employees));
                }
                
                // Function to save salary records to local storage
                function saveSalaryRecords() {
                    localStorage.setItem('salaryRecords', JSON.stringify(salaryRecords));
                }
                
                // Function to save income records to local storage
                function saveIncomeRecords() {
                    localStorage.setItem('incomeRecords', JSON.stringify(incomeRecords));
                }
                
                // Function to save expense records to local storage
                function saveExpenseRecords() {
                    localStorage.setItem('expenseRecords', JSON.stringify(expenseRecords));
                }
                
                // Function to filter dashboard jobs
                function filterDashboardJobs() {
                    const searchTerm = searchInput.value.toLowerCase();
                    const categoryValue = categoryFilter.value;
                    const deadlineFromValue = deadlineFrom.value;
                    const deadlineToValue = deadlineTo.value;
                    const minCostValue = parseFloat(minCost.value) || 0;
                    const maxCostValue = parseFloat(maxCost.value) || Infinity;
                    
                    // Get all jobs
                    const pendingJobs = jobs.filter(job => !job.completed);
                    const completedJobs = jobs.filter(job => job.completed);
                    
                    // Filter pending jobs
                    const filteredPending = pendingJobs.filter(job => {
                        // Search filter
                        const matchesSearch = job.title.toLowerCase().includes(searchTerm) || 
                                            job.description.toLowerCase().includes(searchTerm);
                        // Category filter
                        const matchesCategory = !categoryValue || job.category === categoryValue;
                        // Deadline range filter
                        const jobDeadline = new Date(job.deadline);
                        const matchesDeadlineFrom = !deadlineFromValue || jobDeadline >= new Date(deadlineFromValue);
                        const matchesDeadlineTo = !deadlineToValue || jobDeadline <= new Date(deadlineToValue);
                        // Cost range filter
                        const matchesCost = job.cost >= minCostValue && job.cost <= maxCostValue;
                        
                        return matchesSearch && matchesCategory && matchesDeadlineFrom && matchesDeadlineTo && matchesCost;
                    });
                    
                    // Filter completed jobs
                    const filteredCompleted = completedJobs.filter(job => {
                        const matchesSearch = job.title.toLowerCase().includes(searchTerm) || 
                                            job.description.toLowerCase().includes(searchTerm);
                        const matchesCategory = !categoryValue || job.category === categoryValue;
                        const jobDeadline = new Date(job.deadline);
                        const matchesDeadlineFrom = !deadlineFromValue || jobDeadline >= new Date(deadlineFromValue);
                        const matchesDeadlineTo = !deadlineToValue || jobDeadline <= new Date(deadlineToValue);
                        const matchesCost = job.cost >= minCostValue && job.cost <= maxCostValue;
                        
                        return matchesSearch && matchesCategory && matchesDeadlineFrom && matchesDeadlineTo && matchesCost;
                    });
                    
                    // Update counts
                    pendingCount.textContent = filteredPending.length;
                    completedCount.textContent = filteredCompleted.length;
                    
                    // Display filtered jobs
                    displayFilteredJobs(filteredPending, filteredCompleted);
                }
                
                // Function to display filtered jobs
                function displayFilteredJobs(pendingJobs, completedJobs) {
                    // Clear containers
                    pendingJobsContainer.innerHTML = '';
                    completedJobsContainer.innerHTML = '';
                    
                    // Display pending jobs
                    if (pendingJobs.length === 0) {
                        pendingJobsContainer.innerHTML = `
                            <div class="empty-state">
                                <i class="fas fa-clipboard-list"></i>
                                <h3>No pending jobs</h3>
                                <p>No jobs match your current filters</p>
                            </div>
                        `;
                    } else {
                        pendingJobs.forEach(job => {
                            pendingJobsContainer.appendChild(createJobElement(job));
                        });
                    }
                    
                    // Display completed jobs
                    if (completedJobs.length === 0) {
                        completedJobsContainer.innerHTML = `
                            <div class="empty-state">
                                <i class="fas fa-clipboard-check"></i>
                                <h3>No completed jobs</h3>
                                <p>No jobs match your current filters</p>
                            </div>
                        `;
                    } else {
                        completedJobs.forEach(job => {
                            completedJobsContainer.appendChild(createJobElement(job));
                        });
                    }
                }
                
                // Function to display jobs
                function displayJobs() {
                    // Filter jobs
                    const pendingJobs = jobs.filter(job => !job.completed);
                    const completedJobs = jobs.filter(job => job.completed);
                    
                    // Update counts
                    pendingCount.textContent = pendingJobs.length;
                    completedCount.textContent = completedJobs.length;
                    
                    // Display all jobs
                    displayFilteredJobs(pendingJobs, completedJobs);
                }
                
                // Function to create job element
                function createJobElement(job) {
                    const jobElement = document.createElement('div');
                    jobElement.className = 'task-item';
                    jobElement.dataset.id = job.id;
                    
                    // Format deadline date
                    const deadlineDate = new Date(job.deadline);
                    const formattedDeadline = deadlineDate.toLocaleDateString('en-US', {
                        year: 'numeric',
                        month: 'short',
                        day: 'numeric'
                    });
                    
                    // Calculate remaining time
                    const now = new Date();
                    const diffTime = deadlineDate - now;
                    const diffDays = Math.ceil(diffTime / (1000 * 60 * 60 * 24));
                    
                    let remainingTimeClass = 'time-normal';
                    let remainingTimeText = `${diffDays} days remaining`;
                    
                    if (diffDays < 0) {
                        remainingTimeClass = 'time-overdue';
                        remainingTimeText = `${Math.abs(diffDays)} days overdue`;
                    } else if (diffDays <= 3) {
                        remainingTimeClass = 'time-warning';
                    }
                    
                    // Format start time
                    const startTime = job.startTime ? new Date(job.startTime).toLocaleString() : 'Not started';
                    
                    // Format end time
                    const endTime = job.endTime ? new Date(job.endTime).toLocaleString() : 'Not completed';
                    
                    // Priority badge class
                    let priorityClass = `priority-${job.category}`;
                    
                    jobElement.innerHTML = `
                        <div class="priority-badge ${priorityClass}">${job.category.replace('-', ' ').toUpperCase()}</div>
                        <div class="task-title">${job.title}</div>
                        <div class="task-meta">
                            <div class="task-deadline">
                                <i class="fas fa-calendar"></i> ${formattedDeadline}
                            </div>
                            <div class="task-cost">
                                <i class="fas fa-money-bill-wave"></i> LKR ${job.cost.toFixed(2)}
                            </div>
                        </div>
                        <div class="remaining-time ${remainingTimeClass}">
                            <i class="fas fa-clock"></i> ${remainingTimeText}
                        </div>
                        <div class="task-actions">
                            <button class="btn-secondary" data-id="${job.id}" data-action="view">
                                <i class="fas fa-eye"></i> View
                            </button>
                            ${!job.completed ? `<button class="btn-success" data-id="${job.id}" data-action="complete">
                                <i class="fas fa-check"></i> Complete
                            </button>` : ''}
                            ${!job.completed ? `<button class="btn-secondary" data-id="${job.id}" data-action="postpone">
                                <i class="fas fa-clock"></i> Postpone
                            </button>` : ''}
                            ${job.completed ? `<button class="btn-secondary" data-id="${job.id}" data-action="invoice">
                                <i class="fas fa-file-invoice"></i> Invoice
                            </button>` : ''}
                            <button class="btn-danger" data-id="${job.id}" data-action="delete">
                                <i class="fas fa-trash"></i> Delete
                            </button>
                        </div>
                    `;
                    
                    // Add event listeners to buttons
                    const buttons = jobElement.querySelectorAll('button');
                    buttons.forEach(button => {
                        button.addEventListener('click', function() {
                            const jobId = parseInt(this.getAttribute('data-id'));
                            const action = this.getAttribute('data-action');
                            
                            switch (action) {
                                case 'view':
                                    viewJob(jobId);
                                    break;
                                case 'complete':
                                    completeJob(jobId);
                                    break;
                                case 'postpone':
                                    postponeJob(jobId);
                                    break;
                                case 'delete':
                                    deleteJob(jobId);
                                    break;
                                case 'invoice':
                                    generateInvoice(jobId);
                                    break;
                            }
                        });
                    });
                    
                    return jobElement;
                }
                
                // Function to view job details
                function viewJob(jobId) {
                    const job = jobs.find(j => j.id === jobId);
                    if (!job) return;
                    
                    const jobComments = comments[jobId] || [];
                    
                    let commentsHtml = '';
                    if (jobComments.length > 0) {
                        commentsHtml = jobComments.map(comment => `
                            <div class="comment">
                                <div class="comment-date">${new Date(comment.date).toLocaleString()}</div>
                                <div>${comment.text}</div>
                            </div>
                        `).join('');
                    } else {
                        commentsHtml = '<div class="empty-state">No comments yet</div>';
                    }
                    
                    let filesHtml = '';
                    if (job.files && job.files.length > 0) {
                        filesHtml = '<div class="file-preview">';
                        job.files.forEach((file, index) => {
                            if (file.type.startsWith('image/')) {
                                filesHtml += `
                                    <div class="file-item">
                                        <img src="${file.data}" alt="${file.name}">
                                    </div>
                                `;
                            } else {
                                filesHtml += `
                                    <div class="file-item">
                                        <div style="display: flex; align-items: center; justify-content: center; height: 100%; background-color: #f2f2f2;">
                                            <i class="fas fa-file" style="font-size: 2rem; color: #777;"></i>
                                        </div>
                                    </div>
                                `;
                            }
                        });
                        filesHtml += '</div>';
                    }
                    
                    // Format start and end times
                    const startTime = job.startTime ? new Date(job.startTime).toLocaleString() : 'Not started';
                    const endTime = job.endTime ? new Date(job.endTime).toLocaleString() : 'Not completed';
                    
                    const jobDetailsHtml = `
                        <h2>${job.title}</h2>
                        <div class="form-group">
                            <label>Description</label>
                            <p>${job.description}</p>
                        </div>
                        <div class="form-group">
                            <label>Category</label>
                            <p>${job.category.replace('-', ' ').toUpperCase()}</p>
                        </div>
                        <div class="form-group">
                            <label>Deadline</label>
                            <p>${new Date(job.deadline).toLocaleDateString()}</p>
                        </div>
                        <div class="form-group">
                            <label>Start Time</label>
                            <p>${startTime}</p>
                        </div>
                        <div class="form-group">
                            <label>End Time</label>
                            <p>${endTime}</p>
                        </div>
                        <div class="form-group">
                            <label>Cost</label>
                            <p>LKR ${job.cost.toFixed(2)}</p>
                        </div>
                        <div class="form-group">
                            <label>Status</label>
                            <p>${job.completed ? 'Completed' : 'Pending'}</p>
                        </div>
                        <div class="form-group">
                            <label>Attachments</label>
                            ${filesHtml || '<p>No attachments</p>'}
                        </div>
                        <div class="comments-section">
                            <h3>Comments</h3>
                            <div id="job-comments">
                                ${commentsHtml}
                            </div>
                            <div class="form-group">
                                <label for="new-comment">Add Comment</label>
                                <textarea id="new-comment" placeholder="Enter your comment"></textarea>
                                <button id="add-comment-btn" data-id="${job.id}"><i class="fas fa-comment"></i> Add Comment</button>
                            </div>
                        </div>
                    `;
                    
                    document.getElementById('job-details').innerHTML = jobDetailsHtml;
                    jobModal.style.display = 'block';
                    
                    // Add event listener to add comment button
                    document.getElementById('add-comment-btn').addEventListener('click', function() {
                        const commentText = document.getElementById('new-comment').value.trim();
                        if (commentText) {
                            addComment(jobId, commentText);
                        }
                    });
                }
                
                // Function to add comment
                function addComment(jobId, commentText) {
                    if (!comments[jobId]) {
                        comments[jobId] = [];
                    }
                    
                    comments[jobId].push({
                        text: commentText,
                        date: new Date().toISOString()
                    });
                    
                    saveComments();
                    
                    // Refresh job details
                    viewJob(jobId);
                    
                    showNotification('Comment added successfully!');
                }
                
                // Function to complete job
                function completeJob(jobId) {
                    const jobIndex = jobs.findIndex(job => job.id === jobId);
                    if (jobIndex !== -1) {
                        jobs[jobIndex].completed = true;
                        jobs[jobIndex].endTime = new Date().toISOString();
                        saveJobs();
                        displayJobs();
                        updateInvoiceJobSelect();
                        showNotification('Job marked as completed!');
                    }
                }
                
                // Function to postpone job
                function postponeJob(jobId) {
                    const job = jobs.find(job => job.id === jobId);
                    if (!job) return;
                    
                    const newDeadline = prompt('Enter new deadline (YYYY-MM-DD):', job.deadline);
                    if (newDeadline) {
                        const jobIndex = jobs.findIndex(j => j.id === jobId);
                        if (jobIndex !== -1) {
                            jobs[jobIndex].deadline = newDeadline;
                            saveJobs();
                            displayJobs();
                            showNotification('Job postponed successfully!');
                        }
                    }
                }
                
                // Function to delete job
                function deleteJob(jobId) {
                    if (confirm('Are you sure you want to delete this job?')) {
                        jobs = jobs.filter(job => job.id !== jobId);
                        saveJobs();
                        displayJobs();
                        updateInvoiceJobSelect();
                        showNotification('Job deleted!');
                    }
                }
                
                // Function to update invoice job select
                function updateInvoiceJobSelect() {
                    const completedJobs = jobs.filter(job => job.completed);
                    
                    invoiceJobSelect.innerHTML = '<option value="">Select a job</option>';
                    
                    completedJobs.forEach(job => {
                        const option = document.createElement('option');
                        option.value = job.id;
                        option.textContent = `${job.title} - LKR ${job.cost.toFixed(2)}`;
                        invoiceJobSelect.appendChild(option);
                    });
                }
                
                // Function to generate invoice
                function generateInvoice(jobId) {
                    const job = jobs.find(j => j.id === jobId);
                    if (!job) return;
                    
                    const invoiceId = Date.now();
                    const invoiceDate = new Date().toISOString();
                    const invoiceNumber = String(nextInvoiceNumber++).padStart(9, '0');
                    
                    const newInvoice = {
                        id: invoiceId,
                        jobId: jobId,
                        invoiceNumber: invoiceNumber,
                        date: invoiceDate,
                        items: [{
                            description: job.title,
                            category: job.category,
                            cost: job.cost,
                            startTime: job.startTime,
                            endTime: job.endTime
                        }],
                        total: job.cost
                    };
                    
                    invoices.push(newInvoice);
                    saveInvoices();
                    displayInvoices();
                    
                    // Add income record for business finance
                    addJobCompletionIncome(newInvoice);
                    
                    showNotification('Invoice generated successfully!');
                    
                    // Show invoice
                    viewInvoice(invoiceId);
                }
                
                // Function to view invoice
                function viewInvoice(invoiceId) {
                    const invoice = invoices.find(i => i.id === invoiceId);
                    if (!invoice) return;
                    
                    const job = jobs.find(j => j.id === invoice.jobId);
                    if (!job) return;
                    
                    // Format start and end times
                    const startTime = job.startTime ? new Date(job.startTime).toLocaleString() : 'Not started';
                    const endTime = job.endTime ? new Date(job.endTime).toLocaleString() : 'Not completed';
                    
                    const invoiceHtml = `
                        <div class="invoice-container">
                            <div class="invoice-header">
                                <div>
                                    <h2>INVOICE</h2>
                                    <p>Invoice #${invoice.invoiceNumber}</p>
                                </div>
                                <div>
                                    <p>Date: ${new Date(invoice.date).toLocaleDateString()}</p>
                                    <p>Due Date: ${new Date(invoice.date).toLocaleDateString()}</p>
                                </div>
                            </div>
                            
                            <div class="invoice-details">
                                <h3>Job Details</h3>
                                <p><strong>Title:</strong> ${job.title}</p>
                                <p><strong>Category:</strong> ${job.category.replace('-', ' ').toUpperCase()}</p>
                                <p><strong>Description:</strong> ${job.description}</p>
                                <p><strong>Start Time:</strong> ${startTime}</p>
                                <p><strong>End Time:</strong> ${endTime}</p>
                            </div>
                            
                            <table class="invoice-table">
                                <thead>
                                    <tr>
                                        <th>Description</th>
                                        <th>Category</th>
                                        <th>Cost (LKR)</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <td>${job.title}</td>
                                        <td>${job.category.replace('-', ' ').toUpperCase()}</td>
                                        <td>${job.cost.toFixed(2)}</td>
                                    </tr>
                                </tbody>
                                <tfoot>
                                    <tr>
                                        <td colspan="2" class="invoice-total">Total:</td>
                                        <td class="invoice-total">${invoice.total.toFixed(2)}</td>
                                    </tr>
                                </tfoot>
                            </table>
                            
                            <div style="text-align: center; margin-top: 20px;">
                                <button id="print-invoice"><i class="fas fa-print"></i> Print Invoice</button>
                                <button id="download-pdf" class="btn-secondary"><i class="fas fa-file-pdf"></i> Download PDF</button>
                            </div>
                        </div>
                    `;
                    
                    document.getElementById('invoice-content').innerHTML = invoiceHtml;
                    invoiceModal.style.display = 'block';
                    
                    // Add event listeners
                    document.getElementById('print-invoice').addEventListener('click', function() {
                        window.print();
                    });
                    
                    document.getElementById('download-pdf').addEventListener('click', function() {
                        downloadInvoiceAsPDF(invoice, job);
                    });
                }
                
                // Function to download invoice as PDF
                function downloadInvoiceAsPDF(invoice, job) {
                    const { jsPDF } = window.jspdf;
                    const doc = new jsPDF();
                    
                    // Format start and end times
                    const startTime = job.startTime ? new Date(job.startTime).toLocaleString() : 'Not started';
                    const endTime = job.endTime ? new Date(job.endTime).toLocaleString() : 'Not completed';
                    
                    // Add title
                    doc.setFontSize(20);
                    doc.text('INVOICE', 105, 20, { align: 'center' });
                    
                    // Add invoice details
                    doc.setFontSize(12);
                    doc.text(`Invoice #: ${invoice.invoiceNumber}`, 20, 40);
                    doc.text(`Date: ${new Date(invoice.date).toLocaleDateString()}`, 20, 50);
                    doc.text(`Due Date: ${new Date(invoice.date).toLocaleDateString()}`, 20, 60);
                    
                    // Add job details
                    doc.text('Job Details:', 20, 80);
                    doc.text(`Title: ${job.title}`, 20, 90);
                    doc.text(`Category: ${job.category.replace('-', ' ').toUpperCase()}`, 20, 100);
                    doc.text(`Start Time: ${startTime}`, 20, 110);
                    doc.text(`End Time: ${endTime}`, 20, 120);
                    
                    // Add cost
                    doc.text(`Cost: LKR ${job.cost.toFixed(2)}`, 20, 140);
                    
                    // Add total
                    doc.setFontSize(14);
                    doc.text(`Total: LKR ${invoice.total.toFixed(2)}`, 20, 160);
                    
                    // Save the PDF
                    doc.save(`invoice-${invoice.invoiceNumber}.pdf`);
                    
                    showNotification('Invoice downloaded as PDF!');
                }
                
                // Function to display invoices
                function displayInvoices() {
                    if (invoices.length === 0) {
                        invoicesList.innerHTML = '<div class="empty-state">No invoices generated yet</div>';
                        return;
                    }
                    
                    const invoicesHtml = invoices.map(invoice => {
                        const job = jobs.find(j => j.id === invoice.jobId);
                        if (!job) return '';
                        
                        return `
                            <div class="invoice-archive-item">
                                <div class="invoice-details-summary">
                                    <div class="task-title">Invoice #${invoice.invoiceNumber}</div>
                                    <div class="task-description">Job: ${job.title}</div>
                                    <div class="task-deadline">Date: ${new Date(invoice.date).toLocaleDateString()}</div>
                                    <div class="task-cost">Total: LKR ${invoice.total.toFixed(2)}</div>
                                </div>
                                <div class="invoice-actions">
                                    <button class="btn-secondary" data-id="${invoice.id}" data-action="view-invoice">
                                        <i class="fas fa-eye"></i> View
                                    </button>
                                    <button class="btn-secondary" data-id="${invoice.id}" data-action="download-invoice">
                                        <i class="fas fa-download"></i> PDF
                                    </button>
                                    <button class="btn-danger" data-id="${invoice.id}" data-action="delete-invoice">
                                        <i class="fas fa-trash"></i> Delete
                                    </button>
                                </div>
                            </div>
                        `;
                    }).join('');
                    
                    invoicesList.innerHTML = invoicesHtml;
                    
                    // Add event listeners to invoice buttons
                    const invoiceButtons = invoicesList.querySelectorAll('button');
                    invoiceButtons.forEach(button => {
                        button.addEventListener('click', function() {
                            const invoiceId = parseInt(this.getAttribute('data-id'));
                            const action = this.getAttribute('data-action');
                            
                            if (action === 'view-invoice') {
                                viewInvoice(invoiceId);
                            } else if (action === 'download-invoice') {
                                const invoice = invoices.find(i => i.id === invoiceId);
                                const job = jobs.find(j => j.id === invoice.jobId);
                                if (invoice && job) {
                                    downloadInvoiceAsPDF(invoice, job);
                                }
                            } else if (action === 'delete-invoice') {
                                deleteInvoice(invoiceId);
                            }
                        });
                    });
                }
                
                // Function to delete invoice
                function deleteInvoice(invoiceId) {
                    if (confirm('Are you sure you want to delete this invoice?')) {
                        invoices = invoices.filter(invoice => invoice.id !== invoiceId);
                        saveInvoices();
                        displayInvoices();
                        showNotification('Invoice deleted!');
                    }
                }
                
                // Payroll functions
                // Function to update employee selects
                function updateEmployeeSelects() {
                    // Update salary employee select
                    salaryEmployee.innerHTML = '<option value="">Select an employee</option>';
                    employees.forEach(employee => {
                        const option = document.createElement('option');
                        option.value = employee.id;
                        option.textContent = `${employee.employeeNumber} - ${employee.name}`;
                        salaryEmployee.appendChild(option);
                    });
                    
                    // Update report employee select
                    reportEmployee.innerHTML = '<option value="">Select an employee</option>';
                    employees.forEach(employee => {
                        const option = document.createElement('option');
                        option.value = employee.id;
                        option.textContent = `${employee.employeeNumber} - ${employee.name}`;
                        reportEmployee.appendChild(option);
                    });
                }
                
                // Function to display employees
                function displayEmployees() {
                    if (employees.length === 0) {
                        employeeList.innerHTML = `
                            <div class="empty-state">
                                <i class="fas fa-users"></i>
                                <h3>No employees found</h3>
                                <p>Add a new employee to get started</p>
                            </div>
                        `;
                        return;
                    }
                    
                    const employeesHtml = employees.map(employee => {
                        return `
                            <div class="employee-card">
                                <div class="employee-header">
                                    <div class="employee-name">${employee.name}</div>
                                    <div class="employee-number">${employee.employeeNumber}</div>
                                </div>
                                <div class="employee-details">
                                    <div class="employee-detail">
                                        <i class="fas fa-map-marker-alt"></i>
                                        <span>${employee.address}</span>
                                    </div>
                                    <div class="employee-detail">
                                        <i class="fas fa-birthday-cake"></i>
                                        <span>Age: ${employee.age}</span>
                                    </div>
                                    <div class="employee-detail">
                                        <i class="fas fa-calendar"></i>
                                        <span>DOB: ${new Date(employee.dob).toLocaleDateString()}</span>
                                    </div>
                                    <div class="employee-detail">
                                        <i class="fas fa-mobile-alt"></i>
                                        <span>${employee.mobile}</span>
                                    </div>
                                    <div class="employee-detail">
                                        <i class="fas fa-money-bill-wave"></i>
                                        <span>Basic Salary: LKR ${employee.basicSalary.toFixed(2)}</span>
                                    </div>
                                    <div class="employee-detail">
                                        <i class="fas fa-percentage"></i>
                                        <span>ETF: ${employee.etf}%, EPF: ${employee.epf}%</span>
                                    </div>
                                </div>
                                <div class="employee-actions">
                                    <button class="btn-secondary" data-id="${employee.id}" data-action="view-employee">
                                        <i class="fas fa-eye"></i> View
                                    </button>
                                    <button class="btn-secondary" data-id="${employee.id}" data-action="edit-employee">
                                        <i class="fas fa-edit"></i> Edit
                                    </button>
                                    <button class="btn-danger" data-id="${employee.id}" data-action="delete-employee">
                                        <i class="fas fa-trash"></i> Delete
                                    </button>
                                </div>
                            </div>
                        `;
                    }).join('');
                    
                    employeeList.innerHTML = employeesHtml;
                    
                    // Add event listeners to buttons
                    const viewButtons = employeeList.querySelectorAll('[data-action="view-employee"]');
                    const editButtons = employeeList.querySelectorAll('[data-action="edit-employee"]');
                    const deleteButtons = employeeList.querySelectorAll('[data-action="delete-employee"]');
                    
                    viewButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const employeeId = parseInt(button.getAttribute('data-id'));
                            viewEmployee(employeeId);
                        });
                    });
                    
                    editButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const employeeId = parseInt(button.getAttribute('data-id'));
                            editEmployee(employeeId);
                        });
                    });
                    
                    deleteButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const employeeId = parseInt(button.getAttribute('data-id'));
                            deleteEmployee(employeeId);
                        });
                    });
                }
                
                // Function to view employee
                function viewEmployee(employeeId) {
                    const employee = employees.find(emp => emp.id === employeeId);
                    if (!employee) return;
                    
                    const employeeDetailsHtml = `
                        <h2>${employee.name}</h2>
                        <div class="form-group">
                            <label>Employee Number</label>
                            <p>${employee.employeeNumber}</p>
                        </div>
                        <div class="form-group">
                            <label>Address</label>
                            <p>${employee.address}</p>
                        </div>
                        <div class="form-group">
                            <label>Age</label>
                            <p>${employee.age}</p>
                        </div>
                        <div class="form-group">
                            <label>Date of Birth</label>
                            <p>${new Date(employee.dob).toLocaleDateString()}</p>
                        </div>
                        <div class="form-group">
                            <label>Mobile Number</label>
                            <p>${employee.mobile}</p>
                        </div>
                        <div class="form-group">
                            <label>Basic Salary</label>
                            <p>LKR ${employee.basicSalary.toFixed(2)}</p>
                        </div>
                        <div class="form-group">
                            <label>ETF %</label>
                            <p>${employee.etf}%</p>
                        </div>
                        <div class="form-group">
                            <label>EPF %</label>
                            <p>${employee.epf}%</p>
                        </div>
                    `;
                    
                    document.getElementById('employee-details').innerHTML = employeeDetailsHtml;
                    employeeModal.style.display = 'block';
                }
                
                // Function to edit employee
                function editEmployee(employeeId) {
                    const employee = employees.find(emp => emp.id === employeeId);
                    if (!employee) return;
                    
                    // Fill form with employee data
                    document.getElementById('employee-number').value = employee.employeeNumber;
                    document.getElementById('employee-name').value = employee.name;
                    document.getElementById('employee-address').value = employee.address;
                    document.getElementById('employee-age').value = employee.age;
                    document.getElementById('employee-dob').value = employee.dob;
                    document.getElementById('employee-mobile').value = employee.mobile;
                    document.getElementById('employee-basic-salary').value = employee.basicSalary;
                    document.getElementById('employee-etf').value = employee.etf;
                    document.getElementById('employee-epf').value = employee.epf;
                    
                    // Show form
                    employeeFormContainer.style.display = 'block';
                    
                    // Change form submit behavior to update
                    employeeForm.onsubmit = function(e) {
                        e.preventDefault();
                        
                        // Update employee data
                        employee.employeeNumber = document.getElementById('employee-number').value;
                        employee.name = document.getElementById('employee-name').value;
                        employee.address = document.getElementById('employee-address').value;
                        employee.age = parseInt(document.getElementById('employee-age').value);
                        employee.dob = document.getElementById('employee-dob').value;
                        employee.mobile = document.getElementById('employee-mobile').value;
                        employee.basicSalary = parseFloat(document.getElementById('employee-basic-salary').value);
                        employee.etf = parseFloat(document.getElementById('employee-etf').value);
                        employee.epf = parseFloat(document.getElementById('employee-epf').value);
                        
                        saveEmployees();
                        displayEmployees();
                        updateEmployeeSelects();
                        
                        // Reset form
                        employeeForm.reset();
                        employeeFormContainer.style.display = 'none';
                        
                        // Reset form submit behavior
                        employeeForm.onsubmit = null;
                        
                        showNotification('Employee updated successfully!');
                    };
                }
                
                // Function to delete employee
                function deleteEmployee(employeeId) {
                    if (confirm('Are you sure you want to delete this employee?')) {
                        employees = employees.filter(employee => employee.id !== employeeId);
                        saveEmployees();
                        displayEmployees();
                        updateEmployeeSelects();
                        showNotification('Employee deleted!');
                    }
                }
                
                // Function to view salary record
                function viewSalaryRecord(recordId) {
                    const record = salaryRecords.find(r => r.id === recordId);
                    if (!record) return;
                    
                    const monthNames = [
                        'January', 'February', 'March', 'April', 'May', 'June',
                        'July', 'August', 'September', 'October', 'November', 'December'
                    ];
                    
                    const recordDetailsHtml = `
                        <h2>Salary Record - ${record.employeeName}</h2>
                        <div class="form-group">
                            <label>Period</label>
                            <p>${monthNames[record.month]} ${record.year}</p>
                        </div>
                        <div class="form-group">
                            <label>Employee Number</label>
                            <p>${record.employeeNumber}</p>
                        </div>
                        <div class="form-group">
                            <label>Days Worked</label>
                            <p>${record.daysWorked}</p>
                        </div>
                        <div class="form-group">
                            <label>Leave Days</label>
                            <p>${record.leaveDays}</p>
                        </div>
                        <div class="form-group">
                            <label>OT Hours</label>
                            <p>${record.otHours} hours @ LKR ${record.otRate.toFixed(2)}/hour</p>
                        </div>
                        <div class="form-group">
                            <label>Basic Salary</label>
                            <p>LKR ${record.basicSalary.toFixed(2)}</p>
                        </div>
                        <div class="form-group">
                            <label>Bonus</label>
                            <p>LKR ${record.bonus.toFixed(2)} (${record.bonusPercent}% + LKR ${record.bonusAmount.toFixed(2)})</p>
                        </div>
                        <div class="form-group">
                            <label>Deductions</label>
                            <p>LKR ${record.deductions.toFixed(2)} (${record.deductionPercent}% + LKR ${record.deductionAmount.toFixed(2)})</p>
                        </div>
                        <div class="form-group">
                            <label>ETF Deduction</label>
                            <p>LKR ${record.etfDeduction.toFixed(2)} (${record.etfPercent}%)</p>
                        </div>
                        <div class="form-group">
                            <label>EPF Deduction</label>
                            <p>LKR ${record.epfDeduction.toFixed(2)} (${record.epfPercent}%)</p>
                        </div>
                        <div class="form-group">
                            <label>Net Salary</label>
                            <p style="font-size: 1.2rem; font-weight: bold; color: #2ecc71;">LKR ${record.netSalary.toFixed(2)}</p>
                        </div>
                    `;
                    
                    document.getElementById('employee-details').innerHTML = recordDetailsHtml;
                    employeeModal.style.display = 'block';
                }
                
                // Function to download salary record as PDF
                function downloadSalaryRecordAsPDF(recordId) {
                    const record = salaryRecords.find(r => r.id === recordId);
                    if (!record) return;
                    
                    const { jsPDF } = window.jspdf;
                    const doc = new jsPDF();
                    
                    const monthNames = [
                        'January', 'February', 'March', 'April', 'May', 'June',
                        'July', 'August', 'September', 'October', 'November', 'December'
                    ];
                    
                    // Add title
                    doc.setFontSize(20);
                    doc.text('Salary Record', 105, 20, { align: 'center' });
                    
                    // Add employee details
                    doc.setFontSize(12);
                    doc.text(`Employee: ${record.employeeName}`, 20, 40);
                    doc.text(`Employee Number: ${record.employeeNumber}`, 20, 50);
                    doc.text(`Period: ${monthNames[record.month]} ${record.year}`, 20, 60);
                    
                    // Add salary details
                    doc.text('Salary Details:', 20, 80);
                    doc.text(`Days Worked: ${record.daysWorked}`, 20, 90);
                    doc.text(`Leave Days: ${record.leaveDays}`, 20, 100);
                    doc.text(`OT Hours: ${record.otHours} hours @ LKR ${record.otRate.toFixed(2)}/hour`, 20, 110);
                    doc.text(`OT Payment: LKR ${record.otPayment.toFixed(2)}`, 20, 120);
                    doc.text(`Basic Salary: LKR ${record.basicSalary.toFixed(2)}`, 20, 130);
                    doc.text(`Bonus: LKR ${record.bonus.toFixed(2)}`, 20, 140);
                    doc.text(`Deductions: LKR ${record.deductions.toFixed(2)}`, 20, 150);
                    doc.text(`ETF Deduction: LKR ${record.etfDeduction.toFixed(2)}`, 20, 160);
                    doc.text(`EPF Deduction: LKR ${record.epfDeduction.toFixed(2)}`, 20, 170);
                    
                    // Add net salary
                    doc.setFontSize(14);
                    doc.text(`Net Salary: LKR ${record.netSalary.toFixed(2)}`, 20, 190);
                    
                    // Save the PDF
                    doc.save(`salary-record-${record.employeeNumber}-${monthNames[record.month]}-${record.year}.pdf`);
                    
                    showNotification('Salary record downloaded as PDF!');
                }
                
                // Business Finance functions
                // Function to display income
                function displayIncome() {
                    if (incomeRecords.length === 0) {
                        incomeList.innerHTML = `
                            <div class="empty-state">
                                <i class="fas fa-plus-circle"></i>
                                <h3>No income records found</h3>
                                <p>Add income records to get started</p>
                            </div>
                        `;
                        return;
                    }
                    
                    const incomeHtml = incomeRecords.map(record => {
                        const monthNames = [
                            'January', 'February', 'March', 'April', 'May', 'June',
                            'July', 'August', 'September', 'October', 'November', 'December'
                        ];
                        
                        return `
                            <div class="finance-card income">
                                <div class="finance-header-card">
                                    <div class="finance-title-card">${record.description}</div>
                                    <div class="finance-amount income">LKR ${record.amount.toFixed(2)}</div>
                                </div>
                                <div class="finance-details">
                                    <div class="finance-detail income">
                                        <i class="fas fa-tag"></i>
                                        <span>Source: ${record.source === 'job-completion' ? 'Job Completion' : 'Other'}</span>
                                    </div>
                                    <div class="finance-detail income">
                                        <i class="fas fa-calendar"></i>
                                        <span>Date: ${new Date(record.date).toLocaleDateString()}</span>
                                    </div>
                                    <div class="finance-detail income">
                                        <i class="fas fa-calendar-alt"></i>
                                        <span>Month: ${monthNames[record.month]} ${record.year}</span>
                                    </div>
                                </div>
                                <div class="finance-actions">
                                    <button class="btn-secondary" data-id="${record.id}" data-action="view-income">
                                        <i class="fas fa-eye"></i> View
                                    </button>
                                    <button class="btn-danger" data-id="${record.id}" data-action="delete-income">
                                        <i class="fas fa-trash"></i> Delete
                                    </button>
                                </div>
                            </div>
                        `;
                    }).join('');
                    
                    incomeList.innerHTML = incomeHtml;
                    
                    // Add event listeners to buttons
                    const viewButtons = incomeList.querySelectorAll('[data-action="view-income"]');
                    const deleteButtons = incomeList.querySelectorAll('[data-action="delete-income"]');
                    
                    viewButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const recordId = parseInt(button.getAttribute('data-id'));
                            viewIncomeRecord(recordId);
                        });
                    });
                    
                    deleteButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const recordId = parseInt(button.getAttribute('data-id'));
                            deleteIncomeRecord(recordId);
                        });
                    });
                }
                
                // Function to display expenses
                function displayExpenses() {
                    if (expenseRecords.length === 0) {
                        expenseList.innerHTML = `
                            <div class="empty-state">
                                <i class="fas fa-minus-circle"></i>
                                <h3>No expense records found</h3>
                                <p>Add expense records to get started</p>
                            </div>
                        `;
                        return;
                    }
                    
                    const expensesHtml = expenseRecords.map(record => {
                        const monthNames = [
                            'January', 'February', 'March', 'April', 'May', 'June',
                            'July', 'August', 'September', 'October', 'November', 'December'
                        ];
                        
                        return `
                            <div class="finance-card expense">
                                <div class="finance-header-card">
                                    <div class="finance-title-card">${record.description}</div>
                                    <div class="finance-amount expense">LKR ${record.amount.toFixed(2)}</div>
                                </div>
                                <div class="finance-details">
                                    <div class="finance-detail expense">
                                        <i class="fas fa-tag"></i>
                                        <span>Source: ${record.source === 'payroll' ? 'Payroll' : 'Other'}</span>
                                    </div>
                                    <div class="finance-detail expense">
                                        <i class="fas fa-calendar"></i>
                                        <span>Date: ${new Date(record.date).toLocaleDateString()}</span>
                                    </div>
                                    <div class="finance-detail expense">
                                        <i class="fas fa-calendar-alt"></i>
                                        <span>Month: ${monthNames[record.month]} ${record.year}</span>
                                    </div>
                                </div>
                                <div class="finance-actions">
                                    <button class="btn-secondary" data-id="${record.id}" data-action="view-expense">
                                        <i class="fas fa-eye"></i> View
                                    </button>
                                    <button class="btn-danger" data-id="${record.id}" data-action="delete-expense">
                                        <i class="fas fa-trash"></i> Delete
                                    </button>
                                </div>
                            </div>
                        `;
                    }).join('');
                    
                    expenseList.innerHTML = expensesHtml;
                    
                    // Add event listeners to buttons
                    const viewButtons = expenseList.querySelectorAll('[data-action="view-expense"]');
                    const deleteButtons = expenseList.querySelectorAll('[data-action="delete-expense"]');
                    
                    viewButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const recordId = parseInt(button.getAttribute('data-id'));
                            viewExpenseRecord(recordId);
                        });
                    });
                    
                    deleteButtons.forEach(button => {
                        button.addEventListener('click', () => {
                            const recordId = parseInt(button.getAttribute('data-id'));
                            deleteExpenseRecord(recordId);
                        });
                    });
                }
                
                // Function to view income record
                function viewIncomeRecord(recordId) {
                    const record = incomeRecords.find(r => r.id === recordId);
                    if (!record) return;
                    
                    const monthNames = [
                        'January', 'February', 'March', 'April', 'May', 'June',
                        'July', 'August', 'September', 'October', 'November', 'December'
                    ];
                    
                    const recordDetailsHtml = `
                        <h2>Income Record</h2>
                        <div class="form-group">
                            <label>Source</label>
                            <p>${record.source === 'job-completion' ? 'Job Completion' : 'Other'}</p>
                        </div>
                        <div class="form-group">
                            <label>Description</label>
                            <p>${record.description}</p>
                        </div>
                        <div class="form-group">
                            <label>Amount</label>
                            <p>LKR ${record.amount.toFixed(2)}</p>
                        </div>
                        <div class="form-group">
                            <label>Date</label>
                            <p>${new Date(record.date).toLocaleDateString()}</p>
                        </div>
                        <div class="form-group">
                            <label>Month</label>
                            <p>${monthNames[record.month]} ${record.year}</p>
                        </div>
                    `;
                    
                    document.getElementById('finance-details').innerHTML = recordDetailsHtml;
                    financeModal.style.display = 'block';
                }
                
                // Function to view expense record
                function viewExpenseRecord(recordId) {
                    const record = expenseRecords.find(r => r.id === recordId);
                    if (!record) return;
                    
                    const monthNames = [
                        'January', 'February', 'March', 'April', 'May', 'June',
                        'July', 'August', 'September', 'October', 'November', 'December'
                    ];
                    
                    const recordDetailsHtml = `
                        <h2>Expense Record</h2>
                        <div class="form-group">
                            <label>Source</label>
                            <p>${record.source === 'payroll' ? 'Payroll' : 'Other'}</p>
                        </div>
                        <div class="form-group">
                            <label>Description</label>
                            <p>${record.description}</p>
                        </div>
                        <div class="form-group">
                            <label>Amount</label>
                            <p>LKR ${record.amount.toFixed(2)}</p>
                        </div>
                        <div class="form-group">
                            <label>Date</label>
                            <p>${new Date(record.date).toLocaleDateString()}</p>
                        </div>
                        <div class="form-group">
                            <label>Month</label>
                            <p>${monthNames[record.month]} ${record.year}</p>
                        </div>
                    `;
                    
                    document.getElementById('finance-details').innerHTML = recordDetailsHtml;
                    financeModal.style.display = 'block';
                }
                
                // Function to delete income record
                function deleteIncomeRecord(recordId) {
                    if (confirm('Are you sure you want to delete this income record?')) {
                        incomeRecords = incomeRecords.filter(record => record.id !== recordId);
                        saveIncomeRecords();
                        displayIncome();
                        showNotification('Income record deleted!');
                    }
                }
                
                // Function to delete expense record
                function deleteExpenseRecord(recordId) {
                    if (confirm('Are you sure you want to delete this expense record?')) {
                        expenseRecords = expenseRecords.filter(record => record.id !== recordId);
                        saveExpenseRecords();
                        displayExpenses();
                        showNotification('Expense record deleted!');
                    }
                }
                
                // Function to initialize chart
                function initializeChart() {
                    const ctx = document.getElementById('completion-chart').getContext('2d');
                    
                    // Destroy existing chart if it exists
                    if (completionChart) {
                        completionChart.destroy();
                    }
                    
                    // Prepare data for chart
                    const categories = ['normal', 'important', 'very-important', 'errors', 'fixes', 'bugs', 'repairs', 'not-working'];
                    const categoryLabels = categories.map(cat => cat.replace('-', ' ').toUpperCase());
                    
                    const pendingData = categories.map(cat => 
                        jobs.filter(job => job.category === cat && !job.completed).length
                    );
                    
                    const completedData = categories.map(cat => 
                        jobs.filter(job => job.category === cat && job.completed).length
                    );
                    
                    // Create new chart
                    completionChart = new Chart(ctx, {
                        type: 'bar',
                        data: {
                            labels: categoryLabels,
                            datasets: [
                                {
                                    label: 'Pending Jobs',
                                    data: pendingData,
                                    backgroundColor: 'rgba(243, 156, 18, 0.7)',
                                    borderColor: 'rgba(243, 156, 18, 1)',
                                    borderWidth: 1
                                },
                                {
                                    label: 'Completed Jobs',
                                    data: completedData,
                                    backgroundColor: 'rgba(46, 204, 113, 0.7)',
                                    borderColor: 'rgba(46, 204, 113, 1)',
                                    borderWidth: 1
                                }
                            ]
                        },
                        options: {
                            responsive: true,
                            maintainAspectRatio: false,
                            scales: {
                                y: {
                                    beginAtZero: true,
                                    ticks: {
                                        precision: 0
                                    }
                                }
                            },
                            plugins: {
                                title: {
                                    display: true,
                                    text: 'Job Completion by Category'
                                },
                                legend: {
                                    position: 'top'
                                }
                            }
                        }
                    });
                }
                
                // Function to apply filters
                function applyFilters() {
                    const categoryValue = filterCategory.value;
                    const statusValue = filterStatus.value;
                    const dateFrom = filterDateFrom.value;
                    const dateTo = filterDateTo.value;
                    
                    // Filter jobs based on selected criteria
                    const filteredJobs = jobs.filter(job => {
                        // Category filter
                        if (categoryValue && job.category !== categoryValue) {
                            return false;
                        }
                        
                        // Status filter
                        if (statusValue === 'pending' && job.completed) {
                            return false;
                        }
                        
                        if (statusValue === 'completed' && !job.completed) {
                            return false;
                        }
                        
                        // Date from filter
                        if (dateFrom && new Date(job.createdAt) < new Date(dateFrom)) {
                            return false;
                        }
                        
                        // Date to filter
                        if (dateTo && new Date(job.createdAt) > new Date(dateTo)) {
                            return false;
                        }
                        
                        return true;
                    });
                    
                    // Update report table
                    reportTableBody.innerHTML = '';
                    
                    if (filteredJobs.length === 0) {
                        reportTableBody.innerHTML = `
                            <tr>
                                <td colspan="7" class="empty-state">No jobs match the selected filters</td>
                            </tr>
                        `;
                        return;
                    }
                    
                    // Add filtered jobs to table
                    filteredJobs.forEach(job => {
                        const row = document.createElement('tr');
                        
                        // Format dates
                        const startTime = job.startTime ? new Date(job.startTime).toLocaleString() : 'Not started';
                        const endTime = job.endTime ? new Date(job.endTime).toLocaleString() : 'Not completed';
                        
                        row.innerHTML = `
                            <td>${job.id}</td>
                            <td>${job.title}</td>
                            <td>${job.category.replace('-', ' ').toUpperCase()}</td>
                            <td>${job.completed ? 'Completed' : 'Pending'}</td>
                            <td>${startTime}</td>
                            <td>${endTime}</td>
                            <td>LKR ${job.cost.toFixed(2)}</td>
                        `;
                        
                        reportTableBody.appendChild(row);
                    });
                }
                
                // Function to show notification
                function showNotification(message, type = 'success') {
                    notification.textContent = message;
                    notification.className = 'notification';
                    
                    if (type === 'error') {
                        notification.style.backgroundColor = '#e74c3c';
                    } else {
                        notification.style.backgroundColor = '#2ecc71';
                    }
                    
                    notification.classList.add('show');
                    
                    setTimeout(() => {
                        notification.classList.remove('show');
                    }, 3000);
                }
            });
        </script>
    </body>
</html>
