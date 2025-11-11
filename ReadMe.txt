Frontend: React form with controlled inputs and dynamic premium calculation.
Backend: ASP.NET Core Web API with EF Core InMemory database.

Monthly Premium Calculator

This project is a full-stack application built with React (frontend) and .NET C# (backend) that allows users to input personal and occupational details to calculate their monthly insurance premium.

Project Features

Form inputs for:
  - Name
  - Age Next Birthday
  - Date of Birth (MM/YYYY)
  - Occupation (dropdown)
  - Death Sum Insured
- Real-time premium calculation triggered by occupation selection
- Backend API for premium computation
- Occupation rating and factor mapping
- Clean UI with responsive feedback

Technologies

- Frontend: React (JavaScript)
- Backend: ASP.NET Core Web API (C#)
- Database: SQL Server (schema only)

Premium Formula
Death Premium = (Death Cover Amount × Occupation Rating Factor × Age) / 1000 × 12
		
Assumptions:
  ⁠◦  Age is provided directly.
  ⁠◦  DOB is not used for age calculation.
  ⁠◦  Occupation dropdown triggers premium calculation.
•  Setup instructions for React and .NET backend.
•  API endpoint: POST /api/premium/calculate
•  All fields are mandatory.
				
Database Design
-- Table: Occupations
CREATE TABLE Occupations (
    OccupationId INT PRIMARY KEY IDENTITY(1,1),
    Name VARCHAR(100) NOT NULL,
    Rating VARCHAR(50) NOT NULL,
    Factor DECIMAL(6,2) NOT NULL
);

-- Table: Members
CREATE TABLE Members (
    MemberId INT PRIMARY KEY IDENTITY(1,1),
    Name VARCHAR(100) NOT NULL,
    AgeNextBirthday INT NOT NULL,
    DateOfBirth DATE NOT NULL,
    OccupationId INT NOT NULL,
    DeathSumInsured DECIMAL(12,2) NOT NULL,
    MonthlyPremium DECIMAL(12,2) NOT NULL,
    FOREIGN KEY (OccupationId) REFERENCES Occupations(OccupationId)
);

-- Sample Data
INSERT INTO Occupations (Name, Rating, Factor) VALUES
('Cleaner', 'Light Manual', 11.50),
('Doctor', 'Professional', 1.50),
('Author', 'White Collar', 2.25),
('Farmer', 'Heavy Manual', 31.75),
('Mechanic', 'Heavy Manual', 31.75),
('Florist', 'Light Manual', 11.50),
('Other', 'Heavy Manual', 31.75);

