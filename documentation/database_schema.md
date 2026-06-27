# Database Schema Documentation (Phase 1)

This document describes the MongoDB database schemas designed for the Community Resource Sharing Platform. All schemas are implemented using Mongoose ODM.

---

## 1. User Schema (`User`)
Represents a registered neighborhood community member.

| Field | Type | Description | Constraints |
| :--- | :--- | :--- | :--- |
| `_id` | ObjectId | Unique identifier | Auto-generated |
| `name` | String | User's full name | Required |
| `email` | String | Unique email address | Required, unique, regex format validated |
| `password` | String | Encrypted password | Required, bcrypt-hashed (10 salt rounds) |
| `phone` | String | Contact phone number | Optional, default: `""` |
| `address` | String | Street address details | Optional, default: `""` |
| `locationName` | String | General neighborhood area | Optional, default: `""` |
| `skills` | Array (Strings) | Custom tag list of skills/capabilities | Optional |
| `resources` | Array (Strings) | Custom tag list of resources owned | Optional |
| `createdAt` | Date | Record creation timestamp | Auto-generated (`timestamps: true`) |
| `updatedAt` | Date | Record update timestamp | Auto-generated (`timestamps: true`) |

---

## 2. Resource Schema (`Resource`)
Represents an item listed by a resident that can be borrowed.

| Field | Type | Description | Constraints |
| :--- | :--- | :--- | :--- |
| `_id` | ObjectId | Unique identifier | Auto-generated |
| `owner` | ObjectId | Reference to `User` | Required, Populated |
| `name` | String | Resource name | Required |
| `description` | String | Details or conditions of lending | Required |
| `category` | String | Resource categorization | Required, Enum: `['Tools', 'Books', 'Equipment', 'Electronics', 'Educational', 'Other']` |
| `availabilityStatus`| String | Borrow status | Required, Enum: `['Available', 'Requested', 'Borrowed']`, Default: `"Available"` |
| `location` | String | Pickup location area | Required |
| `borrowedBy` | ObjectId | Reference to `User` | Optional, reference to borrower |
| `requests` | Array (ObjectIds) | References to `User` | Users who have requested to borrow this resource |
| `createdAt` | Date | Record creation timestamp | Auto-generated (`timestamps: true`) |
| `updatedAt` | Date | Record update timestamp | Auto-generated (`timestamps: true`) |

---

## 3. Skill/Service Schema (`Skill`)
Represents a skill or service offered by a resident to assist others.

| Field | Type | Description | Constraints |
| :--- | :--- | :--- | :--- |
| `_id` | ObjectId | Unique identifier | Auto-generated |
| `owner` | ObjectId | Reference to `User` | Required, Populated |
| `title` | String | Service title | Required |
| `description` | String | Details of expertise/service | Required |
| `category` | String | Service categorization | Required, Enum: `['Tutoring', 'Technical Support', 'Home Maintenance', 'Mentorship', 'Other']` |
| `availability` | String | Days/times available | Required |
| `requests` | Array (Objects) | Embedded array of help requests | See Subschema details below |
| `createdAt` | Date | Record creation timestamp | Auto-generated (`timestamps: true`) |
| `updatedAt` | Date | Record update timestamp | Auto-generated (`timestamps: true`) |

### Skill Request Subschema (`requests`)
Embedded schema inside each skill listing.

| Field | Type | Description | Constraints |
| :--- | :--- | :--- | :--- |
| `_id` | ObjectId | Unique identifier | Auto-generated |
| `user` | ObjectId | Reference to requesting `User` | Required, Populated |
| `message` | String | Details of assistance requested | Required |
| `status` | String | State of request | Enum: `['Pending', 'Accepted', 'Declined']`, Default: `"Pending"` |
| `createdAt` | Date | Creation timestamp | Auto-generated |
