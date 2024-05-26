# API Plan Documentation V 0.0.1

---

```dart
{
"Planning SootheMate API V 0.0.1"
}
```

---

- [ ] Authorization

## 1. **POST** Login

```jsx
{{BASE_URL}}/auth/login
```

### Body

```json
{
  "email": "example@bangkit.academy",
  "password": "screetpassword"
}
```

### Success Response

```json
{
  "status": 200,
  "message": "Success",
  "data": {
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9",
    "token_type": "bearer",
    "expires_in": 25200,
    "user": {
      "name": "Fahmy Rosyadi",
      "gender": "Laki - laki",
      "birth_date": "2003-01-29",
      "email": "example@bangkit.academy",
      "email_verified": false //Default False
    }
  }
}
```

### Failed Response

```json
{
  "status": 401,
  "message": "Password is incorrect",
  "data": {}
}
```

## 2. POST Register

```jsx
{{BASE_URL}}/auth/register
```

### Body

```json
{
  "name": "Fahmy Rosyadi",
  "email": "example@bangkit.academy",
  "gender": "Laki - laki",
  "birth_date": "2003-01-29",
  "password": "screetpassword"
}
```

### Success Response

```json
{
  "status": 200,
  "message": "Success",
  "data": {
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9",
    "token_type": "bearer",
    "expires_in": 25200,
    "user": {
      "name": "Fahmy Rosyadi",
      "gender": "Laki - laki",
      "birth_date": "2003-01-29",
      "email": "example@bangkit.academy",
      "email_verified": false // Default False
    }
  }
}
```

### Failed Response

```json
{
  "status": 409,
  "message": "Email already exists",
  "data": {}
}
```

## 3. POST Logout

```jsx
{{BASE_URL}}/auth/logout
```

> Authorization {{Bearer_Token}}

### Success Response

```json
{
  "status": 200,
  "message": "Success",
  "data": {}
}
```

### Failed Response

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {}
}
```

## 4. PUT Update Password

```jsx
{{BASE_URL}}/auth/update-password
```

> Authorization {{Bearer_Token}}

### Body

```json
{
  "old_password": "Password123",
  "password": "12345678",
  "password_confirmation": "12345678"
}
```

### Success Response

```json
{
  "status": 202,
  "message": "Password changed",
  "data": []
}
```

### Failed Response

```json
{
  "status": 401,
  "message": "Old password is incorrect",
  "data": {}
}
```

- Upcoming Features
  - Validate OTP
  - Reset Password via Email
  - Refresh Token

---

- [ ] User Profile

## 1. GET User Detail

```jsx
{{BASE_URL}}/user/detail
```

> Authorization {{Bearer_Token}}

### Succcess Response

```json
{
  "status": 200,
  "message": "Success",
  "data": {
    "id": 54321,
    "name": "Fahmy Rosyadi",
    "gender": "Laki - laki",
    "birth_date": "2003-01-29",
    "email": "example@bangkit.academy",
    "email_verified_at": null, // default null
    "avatar": null, // default null
    "created_at": "2024-04-07T14:39:10.000000Z",
    "updated_at": "2024-04-07T21:21:20.000000Z"
  }
}
```

### Failed Response

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {}
}
```

## 2. PUT Update Profile

```jsx
{{BASE_URL}}/user/update
```

> Authorization {{Bearer_Token}}

## Body

```json
{
  "name": "Fahmy Rosyadi",
  "gender": "Laki - laki",
  "birth_date": "2003-01-29"
}
```

## Success Response

```json
{
    "status": 200,
    "message": "Profile updated successfully",
    "data": {
			  "name" : "Fahmy Rosyadi",
				"email" : "example@bangkit.academy",
				"gender" : "Laki - laki",
				"birth_date" : "2003-01-29"
        "email_verified_at": null, // default null
        "avatar": null, // default null
        "created_at": "2024-04-07T14:39:10.000000Z",
        "updated_at": "2024-04-07T21:21:20.000000Z"
    }
}
```

## Failed Response

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {}
}
```

## 3. POST Update Avatar

```jsx
{{BASE_URL}}/user/avatar
```

> Authorization {{Bearer_Token}}

## Body [Form Data]

```json
{
  "avatar": "home/acer/Downloads/cd3414b0.jpg"
}
```

## Success Response

```json
{
  "status": 200,
  "message": "Avatar updated successfully",
  "data": {
    "name": "Fahmy Rosyadi",
    "email": "example@bangkit.academy",
    "gender": "Laki - laki",
    "birth_date": "2003-01-29",
    "email_verified_at": null, // default null
    "avatar": "https://storage.googleapis.com/user-shootemate/avatar/cd3414b0.jpg",
    "created_at": "2024-04-07T14:39:10.000000Z",
    "updated_at": "2024-04-07T21:21:20.000000Z"
  }
}
```

## Failed Response

```json
{
  "status": 400,
  "message": "Validation failed",
  "data": {
    "message": "Avatar is required"
  }
}
```

- Upcoming Features
  - Deleted Avatar

---

- [ ] Stress Level Management

## 1. POST Predict Stress

```jsx
{{BASE_URL}}/predict
```

> Authorization {{Bearer_Token}}

### Body with Mandatory Only

```json
{
  "gender": "male",
  "age": 30,
  "sleep_duration": 7, // Sleep Duration (hours): The number of hours the person sleeps per day.
  "quality_of_sleep": 8, // Quality of Sleep (scale: 1-10): A subjective rating of the quality of sleep, ranging from 1 to 10.
  "physical_activity_level": 5, // Physical Activity Level (minutes/day): The number of minutes the person engages in physical activity daily.
  "working_hours": 8
}
```

### Body with Optional Data

```json
{
  "gender": "male",
  "age": 30,
  "sleep_duration": 7,
  "quality_of_sleep": 8,
  "physical_activity_level": 5,
  "working_hours": 8,
  "bmi_category": "normal",
  "blood_pressure": "120/80", //  Blood Pressure (systolic/diastolic): The blood pressure measurement of the person, indicated as systolic pressure over diastolic pressure.
  "heart_rate": 70, //  Heart Rate (bpm): The resting heart rate of the person in beats per minute.
  "daily_steps": 10000 // Daily Steps: The number of steps the person takes per day.
}
```

### Success Response

```json
{
  "status": 200,
  "message": "Stress level predicted successfully",
  "data": {
    "stress_level": 40,
    "suggestion": "Consider relaxation techniques and regular exercise."
  }
}
```

### Failed Response (401)

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {
    "message": "Token is invalid or expired"
  }
}
```

### Failed Response (400)

```json
{
  "status": 400,
  "message": "Validation failed",
  "data": {
    "message": "Invalid request data, missing mandatory fields"
  }
}
```

### Failed Response (500)

```json
{
  "status": 500,
  "message": "Internal Server Error",
  "data": {
    "message": "Error during prediction: [error details]"
  }
}
```

## 1. POST **Save Prediction Result**

```jsx
POST {{BASE_URL}}/save-result/my
```

> Authorization {{Bearer_Token}}

## Body

```json
{
  "stress_level": 40
}
```

### **Success Response**

```json
{
  "stress_level": 40,
  "suggestion": "Consider relaxation techniques and regular exercise."
}
```

### **Failed Response (401)**

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {
    "message": "Token is invalid or expired"
  }
}
```

### Failed Response (400)

```json
{
  "status": 400,
  "message": "Validation failed",
  "data": {
    "message": "Invalid request data"
  }
}
```

### Failed Response (500)

```json
{
  "status": 500,
  "message": "Internal Server Error",
  "data": {
    "message": "Error saving prediction result: [error details]"
  }
}
```

## 2. GET **User Prediction History**

```jsx
{{BASE_URL}}/history
```

> Authorization {{Bearer_Token}}

### Success Response

```json
{
  "status": 200,
  "message": "User prediction history retrieved successfully",
  "data": [
    {
      "date": "2024-05-26",
      "stress_level": 40
    },
    {
      "date": "2024-05-25",
      "stress_level": 70
    }
  ]
}
```

### Failed Response (401)

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {
    "message": "Token is invalid or expired"
  }
}
```

### Failed Response (500)

```json
{
  "status": 500,
  "message": "Internal Server Error",
  "data": {
    "message": "Error retrieving prediction history: [error details]"
  }
}
```

## 2. GET **User Detail Prediction History**

```jsx
{{BASE_URL}}/history/:date
```

> Authorization {{Bearer_Token}}

### Success Response

```json
{
  "status": 200,
  "message": "User prediction detail retrieved successfully",
  "data": {
    "date": "2024-05-26",
    "stress_level": 40,
    "suggestion": "Consider relaxation techniques and regular exercise.",
    "age": 30,
    "gender": "male",
    "sleep_duration": 7,
    "quality_of_sleep": 8,
    "physical_activity_level": 5,
    "working_hours": 8,
    "bmi_category": "normal",
    "blood_pressure": "120/80",
    "heart_rate": 70,
    "daily_steps": 10000
  }
}
```

### Failed Response (401)

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {
    "message": "Token is invalid or expired"
  }
}
```

### Failed Response (500)

```json
{
  "status": 500,
  "message": "Internal Server Error",
  "data": {
    "message": "Error retrieving prediction history: [error details]"
  }
}
```

## 3. GET **User Current Stress**

```jsx
{{BASE_URL}}/current-stress
```

> Authorization {{Bearer_Token}}

### Success Response

```json
{
  "status": 200,
  "message": "Current stress level retrieved successfully",
  "data": {
    "date": "2024-05-26",
    "stress_level": 40,
    "suggestion": "Consider relaxation techniques and regular exercise."
  }
}
```

### Failed Response (401)

```json
{
  "status": 401,
  "message": "Unauthorized",
  "data": {
    "message": "Token is invalid or expired"
  }
}
```

### Failed Response (500)

```json
{
  "status": 500,
  "message": "Internal Server Error",
  "data": {
    "message": "Error retrieving prediction history: [error details]"
  }
}
```
