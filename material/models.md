# Model Variations


> [!NOTE]  
> Each `Car` model includes a `user_id` field that associates the car with the user who created it. This field is not supplied by the client; instead, it is automatically populated by middleware using the authenticated user's information.  


----

## Version A

### Car Model

```javascript
const carSchema = new mongoose.Schema({
  make: { type: String, required: true },       // e.g., Toyota
  model: { type: String, required: true },      // e.g., Corolla
  vin: { type: String, required: true },        // Vehicle Identification Number
  manufacturer: { type: String, required: true },
  year: { type: Number, required: true },
  type: { type: String, required: true },       // e.g., Sedan, SUV
  availability: {
    isAvailable: { type: Boolean, required: true },
    dueDate: { type: Date },
    renter: { type: String }
  },
  user_id: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true }
}, { timestamps: true });
```

### User Model

```javascript
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  companyName: { type: String, required: true },
  companyAddress: { type: String, required: true },
  jobTitle: { type: String },
  githubUsername: { type: String, required: true },
  phoneNumber: { type: String, required: true },
}, { timestamps: true, versionKey: false });
```

---

## Version B

### Car Model

```javascript
const carSchema = new mongoose.Schema({
  make: { type: String, required: true },
  model: { type: String, required: true },
  vin: { type: String, required: true },
  year: { type: Number, required: true },
  condition: { type: String, required: true }, // e.g., "Excellent"
  location: { type: String, required: true },  // e.g., "Garage B2"
  availability: {
    isAvailable: { type: Boolean, required: true },
    dueDate: { type: Date },
    renter: { type: String }
  },
  user_id: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true }
}, { timestamps: true });
```

### User Model

```javascript
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  role: { type: String, required: true },
  githubUsername: { type: String, required: true },
  lastLogin: { type: Date, default: Date.now },
  jobTitle: { type: String },
  phoneNumber: { type: String, required: true },
  bio: { type: String, required: true },
}, { timestamps: true, versionKey: false });
```

---

## Version C

### Car Model

```javascript
const carSchema = new mongoose.Schema({
  make: { type: String, required: true },
  model: { type: String, required: true },
  vin: { type: String, required: true },
  mileage: { type: Number, required: true },    // kilometers
  fuelType: { type: String, required: true },  // e.g., Petrol, Diesel, Electric
  description: { type: String },
  availability: {
    isAvailable: { type: Boolean, required: true },
    dueDate: { type: Date },
    renter: { type: String }
  },
  user_id: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true }
}, { timestamps: true });
```

### User Model

```javascript
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  githubUsername: { type: String, required: true },
  language: { type: String, required: true },
  website: { type: String },
  jobTitle: { type: String },
  phoneNumber: { type: String, required: true },
}, { timestamps: true, versionKey: false });
```

---

## Version D

### Car Model

```javascript
const carSchema = new mongoose.Schema({
  make: { type: String, required: true },
  model: { type: String, required: true },
  vin: { type: String, required: true },
  year: { type: Number, required: true },
  mileage: { type: Number, required: true },
  summary: { type: String, required: true },   // short description of car
  availability: {
    isAvailable: { type: Boolean, required: true },
    dueDate: { type: Date },
    renter: { type: String }
  },
  user_id: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true }
}, { timestamps: true });
```

### User Model

```javascript
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true },
  address: { type: String, required: true },
  phoneNumber: { type: String, required: true },
  githubUsername: { type: String, required: true },
  jobTitle: { type: String },
  profilePicture: { type: String },
}, { timestamps: true, versionKey: false });
```
