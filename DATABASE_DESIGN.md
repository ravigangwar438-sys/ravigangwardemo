# Database Design Documentation - AI Traffic Management System

## Overview
This PostgreSQL database is designed to power the AI Traffic & Stolen Vehicle Tracking System. It handles user management, vehicle registrations, document verification, stolen vehicle reports, and automated camera alerts.

## Tables & Schema

### 1. `users`
Stores all system users including citizens, traffic police, and system admins.
- **`user_id`**: Primary Key (Auto-increment)
- **`full_name`**: Full name of the user
- **`email`**: Unique email address for login
- **`phone`**: Unique phone number
- **`password_hash`**: Securely hashed password
- **`role`**: User type (`citizen`, `police`, `admin`)
- **`created_at`**: Timestamp of registration

### 2. `vehicles`
Stores registered vehicles linked to their respective owners.
- **`vehicle_id`**: Primary Key (Auto-increment)
- **`owner_id`**: Foreign Key referencing `users(user_id)`
- **`license_plate`**: Unique registration number
- **`make_model`**: Brand and model of the vehicle
- **`color`**: Vehicle color
- **`created_at`**: Timestamp of entry

### 3. `documents`
Stores document URLs (RC, Insurance, Pollution) linked to vehicles.
- **`document_id`**: Primary Key (Auto-increment)
- **`vehicle_id`**: Foreign Key referencing `vehicles(vehicle_id)`
- **`doc_type`**: Type of document (`RC`, `Insurance`, `PUC`)
- **`doc_url`**: Cloud URL for uploaded document file
- **`uploaded_at`**: Timestamp of upload

### 4. `stolen_vehicles`
Tracks reported stolen vehicles and their recovery status.
- **`stolen_id`**: Primary Key (Auto-increment)
- **`vehicle_id`**: Foreign Key referencing `vehicles(vehicle_id)`
- **`reported_by`**: Foreign Key referencing `users(user_id)`
- **`stolen_date`**: Date and time reported stolen
- **`status`**: Current status (`stolen`, `recovered`)

### 5. `alerts`
Logs automated detections triggered by AI traffic cameras.
- **`alert_id`**: Primary Key (Auto-increment)
- **`vehicle_id`**: Foreign Key referencing `vehicles(vehicle_id)`
- **`camera_location`**: Location string/coordinates of the camera
- **`alert_type`**: Type of alert (default: `stolen_vehicle`)
- **`snapshot_url`**: Cloud URL of camera snapshot
- **`created_at`**: Timestamp of detection
-
