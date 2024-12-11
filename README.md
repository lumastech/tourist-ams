# Attractions Management Subsystem (AMS)

## Overview
The Attractions Management Subsystem (AMS) is an integrated solution designed to enhance tourists' experiences while streamlining the management of scenic spots. This system employs cutting-edge technologies to improve efficiency, resource allocation, and decision-making for attraction management.

---

## Key Features

### 1. Ticket Management and Visitor Support
- **Online Ticketing**: Simplifies ticket purchases and visit scheduling via websites, mobile apps, and third-party platforms.
- **Quick Verification**: Utilizes QR codes, RFID, and other technologies for fast and efficient ticket validation.
- **Sales Channel Management**: Supports multiple sales channels and provides detailed analytics for operational insights.

### 2. Visitor Experience Enhancements
- **Digital Navigation Tools**: Offers electronic maps, voice guides, and augmented reality (AR) guides.
- **Feedback and Complaints**: Provides an online feedback system to enhance service quality.

### 3. Scenic Area and Resource Management
- **Facility Management**: Centralized tracking of parking lots, dining areas, and maintenance schedules.
- **Environmental Monitoring**: Real-time monitoring of air quality, safety conditions, and passenger flow.
- **Intelligent Resource Allocation**: Adjusts operations dynamically based on visitor demand.

### 4. Employee Management
- **Employee Records**: Maintains detailed employee information and performance evaluations.
- **Shift Scheduling**: Intelligent and flexible shift arrangements.
- **Training and Development**: Provides resources for professional growth.

### 5. Revenue and Cost Management
- **Revenue Tracking**: Manages income from tickets, catering, and souvenirs.
- **Cost Monitoring**: Tracks expenses to optimize spending and control costs.
- **Automated Financial Reporting**: Generates comprehensive financial statements.

### 6. Data Analysis and Decision Support
- **Tourist Behavior Analysis**: Examines patterns in ticket purchases, routes, and visit durations.
- **Market Forecasting**: Predicts trends using historical data and market analysis.
- **Operational Insights**: Recommends improvements in marketing, resource allocation, and operations.

---

## Potential Benefits
1. Enhanced tourist satisfaction through digital tools and efficient management.
2. Improved resource utilization and safety protocols.
3. Streamlined operations with data-driven insights.
4. Better employee performance and training opportunities.
5. Comprehensive oversight of financial performance.

---
Here’s a well-structured database schema to support the **Attractions Management Subsystem**. We’ll break this into main entities and their relationships to cover all functionalities.

---

### **Key Entities and Their Relationships**
1. **Tourists**  
   - Stores visitor information, including feedback and complaints.
   - Related to tickets (one-to-many).

2. **Tickets**  
   - Represents tickets purchased, including purchase date, type, and booking details.
   - Related to attractions (many-to-one).

3. **Attractions**  
   - Information about attractions, including guides and locations.
   - Related to facilities and visitor behaviors (one-to-many).

4. **Facilities**  
   - Stores facility information (parking, toilets, dining spots).
   - Related to attractions (many-to-one).

5. **Employees**  
   - Stores employee details, schedules, and performance data.
   - Related to roles and attendance (one-to-many).

6. **Revenues**  
   - Tracks ticket, catering, and souvenir sales.
   - Related to tickets, facilities, and time periods (one-to-many).

7. **Costs**  
   - Tracks expenses like maintenance, labor, and procurement.
   - Related to facilities and time periods (one-to-many).

8. **Analytics**  
   - Tracks visitor behaviors, routes, and preferences.
   - Related to attractions and tickets (many-to-many).

---

### **Database Schema**

#### **1. Tourists Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `tourist_id`      | INT (PK)       | Unique ID for tourists.              |
| `name`            | VARCHAR(255)   | Tourist name.                        |
| `email`           | VARCHAR(255)   | Contact email.                       |
| `feedback`        | TEXT           | Feedback or complaints.              |
| `created_at`      | TIMESTAMP      | Registration or first visit date.    |

---

#### **2. Tickets Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `ticket_id`       | INT (PK)       | Unique ID for the ticket.            |
| `tourist_id`      | INT (FK)       | Related to the tourist.              |
| `attraction_id`   | INT (FK)       | Related to the attraction.           |
| `purchase_date`   | DATE           | Date of purchase.                    |
| `visit_date`      | DATE           | Scheduled visit date.                |
| `price`           | DECIMAL(10, 2) | Ticket price.                        |
| `qr_code`         | VARCHAR(255)   | QR code for ticket validation.       |

---

#### **3. Attractions Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `attraction_id`   | INT (PK)       | Unique ID for the attraction.        |
| `name`            | VARCHAR(255)   | Attraction name.                     |
| `description`     | TEXT           | Attraction description.              |
| `location`        | VARCHAR(255)   | Address or coordinates.              |
| `map_url`         | VARCHAR(255)   | Link to the digital map.             |

---

#### **4. Facilities Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `facility_id`     | INT (PK)       | Unique ID for the facility.          |
| `attraction_id`   | INT (FK)       | Related to the attraction.           |
| `type`            | ENUM           | Facility type (e.g., parking, dining).|
| `status`          | ENUM           | Status (available, under maintenance).|
| `last_updated`    | TIMESTAMP      | Last maintenance date.               |

---

#### **5. Employees Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `employee_id`     | INT (PK)       | Unique ID for the employee.          |
| `name`            | VARCHAR(255)   | Employee name.                       |
| `role`            | VARCHAR(255)   | Job role or position.                |
| `shift_schedule`  | JSON           | JSON object for shifts.              |
| `attendance`      | JSON           | JSON object for attendance records.  |

---

#### **6. Revenues Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `revenue_id`      | INT (PK)       | Unique ID for the revenue entry.     |
| `source`          | ENUM           | Source (ticket, catering, souvenirs).|
| `amount`          | DECIMAL(10, 2) | Amount of revenue.                   |
| `date`            | DATE           | Date of revenue generation.          |

---

#### **7. Costs Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `cost_id`         | INT (PK)       | Unique ID for the cost entry.        |
| `type`            | ENUM           | Type (labor, maintenance, procurement).|
| `amount`          | DECIMAL(10, 2) | Amount of cost.                      |
| `date`            | DATE           | Date of expense.                     |

---

#### **8. Analytics Table**
| Column Name       | Data Type      | Description                          |
|-------------------|----------------|--------------------------------------|
| `analysis_id`     | INT (PK)       | Unique ID for the analysis entry.    |
| `ticket_id`       | INT (FK)       | Related to a ticket.                 |
| `behavior_data`   | JSON           | JSON object for visitor behavior.    |
| `created_at`      | TIMESTAMP      | Analysis generation timestamp.       |

---

### **Relationships**
1. **Tourists ↔ Tickets** (1:N)
2. **Tickets ↔ Attractions** (N:1)
3. **Attractions ↔ Facilities** (1:N)
4. **Employees ↔ Roles/Attendance** (1:N)
5. **Tickets ↔ Analytics** (N:N through analytics table)
6. **Attractions ↔ Analytics** (N:N through analytics table)
---

## Conclusion
The Attractions Management Subsystem is a comprehensive tool for modernizing attraction management, enhancing tourist experiences, and driving operational efficiency through data-driven decision-making.

