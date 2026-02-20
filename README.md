# MyPet - Mobile app project (Group 5)

### Overview

MyPet is a comprehensive React Native mobile application designed for pet owners to manage and track all aspects of their pets' care and wellbeing. Built with TypeScript and Expo, it provides a centralized platform for organizing pet information, health records, activities, and daily care routines.

### What is MyPet?

MyPet is an all-in-one pet care companion that helps pet owners:

- Organize pet profiles with detailed information about each animal
- Track health records including vaccinations, medications, and veterinary visits
- Monitor pet activities through GPS-based walk tracking with real-time statistics
- Manage weight with historical data and visual progress charts
- Schedule events using an integrated calendar for reminders and appointments
- Share access with family members through sub-user accounts

### Key use cases

1. **Health Management**
    - Record and track vaccinations with expiration dates.
    - Manage ongoing medications with start and end dates.
    - Document veterinary visits with location, costs and notes.
    - Monitor pet weight changes over time with a graphical visualization.

2. **Activity tracking**
    - Record walks with GPS tracking and route mapping.
    - Track distance, duration, speed and step count.
    - View walk history with detailed statistics.
    - Sync walk data to cloud storage (optional)

3. **Organization & Planning**
    - Create calendar events for appointments, grooming and other activities.
    - Manage multiple pets from a single account.
    - Access pet information across devices.

4. **Multi user collaboration**
    - Share pet information to friends, family, veterinarian or a caretaker.
    - Assign roles with different permission levels.
    
## Tech Stack

### **Frontend**
 - **React Native** with **Expo** for cross-platform mobile development (iOS & Android).
 - **TypeScript** for type safety.
 - **React Native Paper** implementing Material Design 3.
 - **Expo Location** & **OSM (Open Street Map)** for GPS tracking and mapping.

### **Backend**
 - **Backend Framework**: Express.js (Node.js).
 - **Database**: PostgreSQL.
 - **Authentication**: JWT (JSON Web Tokens) with bcrypt password hashing.
 - **Security**: Helmet for security headers, CORS protection, rate limiting for API abuse prevention.
 - **Deployment**: Docker containerization support.
 - **API Design**: RESTful architecture designed for mobile app consumption.

### Database Schema

The application uses PostgreSQL with the following Entity Relationship Diagram (ERD):

![Database ERD Schema](images/ERD.png)

The database schema includes tables for users, pets, health records (vaccinations, medications, vet visits), weight tracking, calendar events, and walk routes. The schema supports multi-user collaboration through role-based access control.

### Data Storage
 - **AsyncStorage** for local data persistence.
 - Cloud sync capabilities for walk routes.

### Backend Integration
 - RESTful API communication via Axios.
 - Services for pets health records, walks & calendar events.

### Key features
- Secure user registration & login.
- Protected API endpoints with token-based authentication.
- Data validation and sanitization.
- Rate limiting to prevent brute force attacks.
- Mobile-friendly API response structure

## Design Philosophy

The application follows **Material Design 3** principles, providing:

- Clean, modern interface with consistent styling 
- Intuitive navigation with tab and stack navigators
- Accessible color scheme with proper contrast ratios
- Responsive layouts that work across different screen sizes
- Smooth animations and transitions for better UX

## Repository structures

### Backend

```
server/
├── database.sql              # PostgreSQL database schema
├── LICENSE                   # License information
├── README.md                 # This documentation
│
└── backend/                  # Main application directory
    ├── docker-compose.ci.yml # Docker Compose for CI/testing
    ├── Dockerfile            # Container definition
    ├── package.json          # Node.js dependencies and scripts
    │
    ├── src/                  # Source code
    │   ├── index.js          # Application entry point & server config
    │   ├── PRIVACY_POLICY.html
    │   │
    │   ├── config/           # Configuration modules
    │   │   ├── database.js   # PostgreSQL connection pool
    │   │   └── jwt.js        # JWT token configuration
    │   │
    │   ├── controllers/      # Business logic & request handlers
    │   │   ├── authController.js        # User authentication & account management
    │   │   ├── avatarController.js      # Avatar upload & retrieval
    │   │   ├── calendarEventController.js # Calendar event CRUD operations
    │   │   ├── medicationController.js  # Medication tracking
    │   │   ├── petController.js         # Pet profile management & sharing
    │   │   ├── routeController.js       # GPS route tracking
    │   │   ├── vaccinationController.js # Vaccination records
    │   │   ├── vetVisitController.js    # Vet visit tracking
    │   │   └── weightController.js      # Weight monitoring
    │   │
    │   ├── middleware/       # Request processing pipeline
    │   │   ├── authenticateToken.js           # JWT validation
    │   │   ├── avatarUpload.js                # Multer file upload config
    │   │   ├── resolveEffectiveUser.js        # Multi-user & sub-user resolution
    │   │   ├── validateLogin.js               # Login input validation
    │   │   ├── validateRegistration.js        # Registration input validation
    │   │   ├── validateSubUserRegistration.js # Sub-user creation validation
    │   │   └── validateSubUserRoleUpdate.js   # Role update validation
    │   │
    │   ├── models/           # Database access layer
    │   │   ├── Avatar.js         # Avatar database operations
    │   │   ├── CalendarEvent.js  # Calendar event queries
    │   │   ├── Medication.js     # Medication CRUD
    │   │   ├── Pet.js            # Pet profile & sharing logic
    │   │   ├── Route.js          # GPS route storage
    │   │   ├── User.js           # User & authentication queries
    │   │   ├── Vaccination.js    # Vaccination records
    │   │   ├── VetVisit.js       # Vet visit data
    │   │   └── Weight.js         # Weight tracking
    │   │
    │   ├── routes/           # API endpoint definitions
    │   │   ├── avatarRoutes.js         # /api/avatars/*
    │   │   ├── calendarEventRoutes.js  # /api/calendar-events/*
    │   │   ├── medicationRoutes.js     # /api/medications/*
    │   │   ├── petRoutes.js            # /api/pets/*
    │   │   ├── routeRoutes.js          # /api/routes/*
    │   │   ├── userRoutes.js           # /api/auth/*
    │   │   ├── vaccinationRoutes.js    # /api/vaccinations/*
    │   │   ├── vetVisitRoutes.js       # /api/vet-visits/*
    │   │   └── weightRoutes.js         # /api/weights/*
    │   │
    │   ├── services/         # Business logic services (reserved for future use)
    │   │
    │   ├── types/            # Type definitions (reserved for future use)
    │   │
    │   └── utils/            # Helper functions & utilities
    │       ├── generateToken.js  # JWT token generation
    │       ├── hashPassword.js   # bcrypt password hashing
    │       └── shareCode.js      # Pet sharing code generation
    │
    └── uploads/              # File storage
        └── avatars/          # User & pet avatar images
```

### Application

```
mobile/
├── src/
│   ├── App.tsx                      # Root application component
│   │
│   ├── assets/                      # Static assets
│   │   ├── fonts/                   # Custom fonts
│   │   ├── icons/                   # Icon assets
│   │   └── images/                  # Image assets
│   │
│   ├── components/                  # Reusable UI components
│   │   ├── AvatarDisplay.tsx        # Pet avatar display component
│   │   ├── AvatarUploadDialog.tsx   # Avatar upload modal
│   │   ├── RedeemShareCodeDialog.tsx # Share code redemption
│   │   ├── SharePetDialog.tsx       # Pet sharing dialog
│   │   ├── SwipeableCard.tsx        # Swipeable card component
│   │   └── SyncSetupDialog.tsx      # Sync configuration dialog
│   │
│   ├── screens/                     # Application screens
│   │   ├── AddPetScreen.tsx         # Add new pet
│   │   ├── CalendarScreen.tsx       # Calendar view
│   │   ├── HealthScreen.tsx         # Health records hub
│   │   ├── HomeScreen.tsx           # Main dashboard
│   │   ├── LoginScreen.tsx          # User login
│   │   ├── MapScreen.tsx            # Map view for walks
│   │   ├── MedicationsScreen.tsx    # Medication management
│   │   ├── PetProfileScreen.tsx     # Individual pet profile
│   │   ├── PetsScreen.tsx           # Pet list view
│   │   ├── ProfileScreen.tsx        # User profile
│   │   ├── RegisterScreen.tsx       # User registration
│   │   ├── SettingsScreen.tsx       # App settings
│   │   ├── VaccinationsScreen.tsx   # Vaccination records
│   │   ├── VisitsScreen.tsx         # Veterinary visits
│   │   ├── WalkDetailScreen.tsx     # Walk tracking detail
│   │   ├── WalkHistoryScreen.tsx    # Walk history list
│   │   └── WeightManagementScreen.tsx # Weight tracking
│   │
│   ├── navigation/                  # Navigation configuration
│   │   └── Navigation.tsx           # App navigation structure
│   │
│   ├── services/                    # Business logic & API layer
│   │   ├── api.ts                   # Base API client (Axios)
│   │   ├── authService.ts           # Authentication service
│   │   ├── avatarService.ts         # Avatar management
│   │   ├── calendarService.ts       # Calendar events
│   │   ├── locationService.ts       # GPS & location tracking
│   │   ├── medicationsService.ts    # Medication records
│   │   ├── petService.ts            # Pet data management
│   │   ├── routeService.ts          # Walk route tracking
│   │   ├── storageService.ts        # Local storage (AsyncStorage)
│   │   ├── vaccinationsService.ts   # Vaccination records
│   │   ├── visitsService.ts         # Veterinary visits
│   │   └── weightsService.ts        # Weight tracking
│   │
│   ├── contexts/                    # React Context providers
│   │   ├── AuthContext.tsx          # Authentication state
│   │   ├── SnackbarContext.tsx      # Global notifications
│   │   ├── WalkContext.tsx          # Walk tracking state
│   │   └── index.ts                 # Context exports
│   │
│   ├── hooks/                       # Custom React hooks
│   │   └── index.ts                 # Hook exports
│   │
│   ├── helpers/                     # Helper functions
│   │   └── index.ts                 # Helper exports
│   │
│   ├── utils/                       # Utility functions
│   │   └── constants.ts             # App constants
│   │
│   ├── config/                      # Application configuration
│   │   └── index.ts                 # Config settings (API URLs)
│   │
│   ├── types/                       # TypeScript type definitions
│   │   └── index.ts                 # Type exports
│   │
│   └── styles/                      # Styling & theming
│       ├── theme.ts                 # MD3 theme (colors, typography)
│       ├── authStyles.ts            # Auth screen styles
│       ├── screenStyles.ts          # Screen-specific styles
│       ├── index.ts                 # Style exports
│       └── README.md                # Design system documentation
│
├── android/                         # Android native code
│   ├── app/                         # Android app module
│   │   ├── src/
│   │   │   ├── main/
│   │   │   │   ├── AndroidManifest.xml
│   │   │   │   ├── java/com/mypet/ # Native Java code
│   │   │   │   └── res/             # Android resources
│   │   │   ├── debug/               # Debug build configuration
│   │   │   └── debugOptimized/      # Optimized debug build
│   │   ├── build.gradle             # App build configuration
│   │   └── proguard-rules.pro       # ProGuard rules
│   ├── gradle/                      # Gradle wrapper
│   ├── build.gradle                 # Project build configuration
│   ├── settings.gradle              # Project settings
│   ├── gradle.properties            # Gradle properties
│   ├── gradlew                      # Gradle wrapper (Unix)
│   └── gradlew.bat                  # Gradle wrapper (Windows)
│
├── app.json                         # Expo configuration
├── babel.config.js                  # Babel configuration
├── eslint.config.mjs                # ESLint configuration
├── metro.config.js                  # Metro bundler configuration
├── tsconfig.json                    # TypeScript configuration
├── package.json                     # Dependencies and scripts
└── index.ts                         # App entry point
```

### Documents

```
Documents/
├── images/                          # Documentation images
│   └── ERD.png                     # Database Entity Relationship Diagram
├── ProjectDocs/                     # Project documentation files
│   ├── Palaverimuistiot/           # Scrum meeting notes (Finnish)
│   │   ├── scrum_palaverimuistio 6.1.-13.1.2026.docx
│   │   ├── scrum_palaverimuistio 15.1.2026 .docx
│   │   ├── scrum_palaverimuistio 18.1.2026.docx
│   │   ├── scrum_palaverimuistio 22.1.2026.docx
│   │   ├── Scrum palaverimuistio 25.1.2026.docx
│   │   ├── Scrum palaverimuistio 26.1.2026.docx
│   │   ├── Scrum palaverimuistio 29.1.2026.docx
│   │   ├── Scrum palaverimuistio 1.2.2026.docx
│   │   ├── Scrum palaverimuistio 4.2.2026.docx
│   │   ├── Scrum palaverimuistio 9.2.2026.docx
│   │   ├── Scrum palaverimuistio 12.2.2026.docx
│   │   ├── Scrum palaverimuistio 15.2.2026.docx
│   │   ├── Scrum palaverimuistio 16.2.2026.docx
│   │   ├── Scrum palaverimuistio 17.2.2026.docx
│   │   ├── Scrum palaverimuistio 18.2.2026.docx
│   │   └── Scrum palaverimuistio 19.2.2026.docx
│   ├── PrivacyPolicy.md            # Application privacy policy
│   ├── README.md                    # Project documentation main file
│   ├── Security Audit Report R5-App - February 2026-1.pdf  # Security audit results
│   ├── Työajan seuranta.xlsx       # Time tracking spreadsheet
│   └── wireframe.pdf                # UI/UX wireframes
└── README.md                        # This file
```

## Postman

Access the API documentation and test the endpoints using Postman:

https://documenter.getpostman.com/view/48372140/2sBXcEk16i

