### Normalization conducted in the bottom up project of Passport Form.

**Objective:**

The normalization process has been done so that there is no data repeated in our project and that each and every table in the database is well connected and seamlessly integrated with each other.


**Normalization**

Let’s normalize the passport application database step by step, from 1NF to 3NF.

1NF (First Normal Form)
To achieve 1NF, we must ensure the following for each table:

Every column must contain atomic (indivisible) values.
There should be no repeating groups or arrays.
Each table must have a unique primary key.
We already have a good starting point with your entities, but we'll review and adjust them to ensure they meet the criteria for 1NF.

Identified Issues:
Multiple contact numbers for emergency contacts.
Multiple addresses for applicants.
Possible multiple criminal proceedings for applicants.
Normalized Tables in 1NF:
Applicant Table:

Primary Key: ApplicantID
Attributes: GivenName, Surname, DateOfBirth, RaceOfBirth, Gender, MaritalStatus, Citizenship, PAN, VoterID, EmploymentType, OrganizationName, EducationalQualification, AadhaarNumber
All attributes are atomic, so no changes needed.

FamilyDetails Table:

Primary Key: FamilyID
Attributes: ApplicantID (Foreign Key), FatherName, MotherName, LegalGuardianName, SpouseName, FatherPassportNumber, MotherPassportNumber, FatherNationality, MotherNationality, MotherStatus
This is already in 1NF since each attribute contains atomic values.

EmergencyContact Table:

Primary Key: ContactID
Attributes: ApplicantID (Foreign Key), Name, ContactAddress, MobileNumber, TelephoneNumber, EmailID
Since applicants can have multiple emergency contacts, this structure supports a one-to-many relationship and complies with 1NF.

Address Table:

Primary Key: AddressID
Attributes: ApplicantID (Foreign Key), AddressType, HouseNoStreetName, City, District, State, PIN, PoliceStation, MobileNumber, TelephoneNumber, EmailID
Each applicant can have multiple addresses (e.g., permanent, temporary), and this table supports that with a one-to-many relationship.

CriminalProceedings Table:

Primary Key: ProceedingID
Attributes: ApplicantID (Foreign Key), OffenceDescription, Pending, CourtDetails, WarrantDetails, ArrestDetails, DepartureProhibition
Since there could be multiple criminal proceedings for one applicant, this structure is already in 1NF.

Passport Table:

Primary Key: PassportID
Attributes: ApplicantID (Foreign Key), PassportNumber, TypeOfApplication, TypeOfBooklet, ValidityRequired, DateOfIssue, DateOfExpiry, ReissueReason, PersonalParticularsChronology
This table contains atomic values and complies with 1NF.

FeeDetails Table:

Primary Key: FeeID
Attributes: ApplicantID (Foreign Key), FeeAmount, DDNumber, DDIssueDate, BankName, BranchName
Fee details are atomic, so no changes needed.

2NF (Second Normal Form)
To achieve 2NF, the following must be ensured:

The table is already in 1NF.
All non-key attributes are fully dependent on the entire primary key (no partial dependencies).
Issues Identified:
Some non-key attributes are dependent only on a part of the primary key (such as in cases where composite keys are used).
Steps for 2NF:
Applicant Table:

The Applicant table is in 2NF since all attributes depend on the primary key ApplicantID.
FamilyDetails Table:

All attributes depend on FamilyID, and the table is in 2NF.
EmergencyContact Table:

No partial dependencies; ContactID uniquely identifies each emergency contact, so the table is in 2NF.
Address Table:

Each address is uniquely identified by AddressID, and all attributes are dependent on it. Therefore, this table is also in 2NF.
CriminalProceedings Table:

All attributes depend on ProceedingID, and the table is in 2NF.
Passport Table:

No partial dependencies exist, so the Passport table is in 2NF.
FeeDetails Table:

Each attribute is fully dependent on FeeID, and the table is in 2NF.


3NF (Third Normal Form)
To achieve 3NF, we need to ensure:

The table is already in 2NF.
There are no transitive dependencies (i.e., non-key attributes should not depend on other non-key attributes).
Issues Identified:
There may be transitive dependencies in the FamilyDetails and FeeDetails tables.
Steps for 3NF:
Applicant Table:

The Applicant table does not have transitive dependencies, so it is in 3NF.
FamilyDetails Table:

No transitive dependencies are present. Attributes like FatherName, MotherName, etc., are only dependent on FamilyID. The table is in 3NF.
EmergencyContact Table:

The EmergencyContact table does not have any transitive dependencies. It is in 3NF.
Address Table:

The Address table is free of transitive dependencies, so it is in 3NF.
CriminalProceedings Table:

No transitive dependencies exist here, so the table is in 3NF.
Passport Table:

The Passport table is already in 3NF as there are no transitive dependencies.
FeeDetails Table:

Attributes like BankName and BranchName depend directly on FeeID, and there are no transitive dependencies. Therefore, it is in 3NF.                                          
The passport application database is fully normalized through 1NF, 2NF, and 3NF. It is ensured that each table is well-structured, ensuring data integrity, minimizing redundancy, and making the system scalable and easy to maintain.



### Project Description: Passport Application SQL Database

**Objective:**
The goal of this project is to design and implement a SQL-based relational database system to manage the passport application process. The database will store and organize data related to applicants, their addresses, emergency contacts, criminal proceedings, and fee details for passport issuance or reissue. This system aims to provide a secure and efficient way to track and manage applicant information throughout the passport lifecycle.

**Scope:**
The database manages various aspects of passport applications, from new applications to reissue requests. It handles detailed information such as personal addresses, criminal records, and payment details. This project enables streamlined management of applicant records, ensuring secure storage and fast retrieval of data during processing.

**Components:**
1. **Applicant Table:** Contains detailed information about passport applicants, including application type (new/reissue), passport type (36/60 pages), duration (5/10 years), issue and expiration dates, and issuance location. Special cases like reissue due to lost passports are also tracked.
2. **Address Table:** Stores present and permanent addresses for each applicant, including detailed address components such as house number, street name, city, district, state/UT, PIN, police station, and contact information (mobile, telephone, and email).
3. **EmergencyContact Table:** Records emergency contact details for each applicant, including name, contact address, mobile number, telephone number, and email ID.
4. **CriminalProceedings Table:** Captures any criminal history related to the applicant, including offence descriptions, court and warrant details, arrest history, and any prohibitions against departure from the country.
5. **FeeDetails Table:** Manages payment information related to the passport application process. This includes the fee amount, demand draft (DD) number, issuance and expiry dates, and bank and branch details.

**Features:**
- **Applicant Tracking:** The system stores essential applicant data such as application type, passport specifications, issue/expiry dates, and the reason for reissue when applicable (e.g., lost passport).
- **Address Management:** The database maintains detailed present and permanent address information, which is critical for verification processes during passport issuance.
- **Emergency Contacts:** Each applicant is required to provide emergency contact details, which are stored and can be accessed quickly in case of emergencies.
- **Criminal History:** The system tracks any ongoing criminal proceedings, court cases, and arrests related to the applicant. This helps ensure that passports are not issued to individuals with unresolved legal issues that prevent their travel.
- **Fee Management:** Fee payment details are securely recorded, with each application linked to its corresponding demand draft (DD) information, including banking details and validity periods.

**Use Case:**
This database system is designed to be used by passport officers and processing centers to handle large volumes of passport applications. The database simplifies the workflow by centralizing applicant data, allowing for quick retrieval and processing. It ensures that all required information, such as addresses, emergency contacts, and legal records, is available at a glance for each applicant.


This database system provides a robust solution to efficiently manage the intricate details involved in passport issuance, ensuring security, accuracy, and convenience in handling applicants' sensitive information.
