
# 🧭 SingaHai Travel Buddy – PRD + API Specification v1.0

## 📌 Overview
SingaHai Travel Buddy is a mobile travel assistant that helps users create a highly personalized and efficient travel experience between Singapore and Shanghai. Key features include itinerary planning, accommodation matching, and food discovery — all tailored to the user's personality and preferences.

## 🎯 Goals and Objectives
- Enable users to plan personalized itineraries.
- Match accommodations based on personality, preferences, and budget.
- Provide curated local food recommendations based on dietary and personality profiles.

## 🧍‍♂️ User Personas
| Trait            | Preferences                                                                |
|------------------|----------------------------------------------------------------------------|
| Introvert        | Quiet spaces, solo activities, peaceful surroundings                       |
| Night Owl        | Late-night events, open restaurants, calm atmospheres                      |
| Adventure Junkie | Active experiences, thrill-seeking, local exploration                      |

## 📅 Feature 1: Personalized Itinerary Planner

**User Story:**  
_As a traveler, I want to create a personalized itinerary for my Singapore to Shanghai trip so that I can make the most of my time._

### ✅ Acceptance Criteria
- Personality-based activity suggestions  
- Customizable daily schedule  
- Travel time and cost estimation included

### 🛠 Functional Requirements
- Personality quiz/init
- Drag-and-drop schedule builder
- Maps and travel time APIs
- Cost tracker

### 🎨 Design Requirements
- Calm, minimal UI  
- Dark mode preference  
- Muted color palette (twilight blue, lavender)

## 🏨 Feature 2: Accommodation Matcher

**User Story:**  
_As a traveler, I want to find accommodation that matches my personality and budget so that I feel comfortable during my stay._

### ✅ Acceptance Criteria
- Personality-based filters  
- Distance to planned activities  
- User reviews + booking integration

### 🛠 Functional Requirements
- Personality & budget filters
- Integration with booking APIs
- Map-based sorting by distance

### 🎨 Design Requirements
- Quiet visuals, smooth transitions  
- Card layout for hotels  
- Emphasis on comfort and calm

## 🍜 Feature 3: Food Discovery Engine

**User Story:**  
_As a food enthusiast, I want personalized restaurant recommendations so that I can experience the best local cuisine._

### ✅ Acceptance Criteria
- Filters for dietary preferences  
- Personality-based restaurant tags  
- Menu translations + local highlights

### 🛠 Functional Requirements
- Cuisine + diet filter
- Popularity indicators
- Menu translation layer

### 🎨 Design Requirements
- Vibrant food photos  
- Simple UI with strong visual hierarchy  
- Soft color contrasts

## 📈 Success Metrics
- >70% itinerary completion  
- >50% hotel recommendation usage  
- >80% satisfaction with food recs  
- <5% crash rate per session  

---

## 🧪 API Specification

### 🔐 Authentication
```http
Authorization: Bearer <JWT_TOKEN>
Content-Type: application/json
```

### 👤 GET /user/profile
Returns the current user’s profile and preferences.

```json
{
  "id": "user_12345",
  "name": "Alex",
  "age": 31,
  "personality": ["introvert", "night_owl", "adventure_junkie"],
  "budget": { "currency": "SGD", "daily_max": 150 },
  "dietary_preferences": ["vegetarian", "no_pork"]
}
```

### 🧭 POST /itinerary/generate
Generate a custom itinerary based on profile and dates.

```json
{
  "from": "Singapore",
  "to": "Shanghai",
  "start_date": "2025-09-10",
  "end_date": "2025-09-18",
  "personality": ["introvert", "night_owl", "adventure_junkie"]
}
```

**Response:**
```json
{
  "itinerary_id": "itn_101",
  "days": [
    {
      "date": "2025-09-10",
      "activities": [
        {
          "title": "Gardens by the Bay",
          "type": "nature",
          "start_time": "10:00",
          "end_time": "12:00",
          "travel_time_minutes": 15,
          "estimated_cost": 18.0
        }
      ]
    }
  ]
}
```

### 🛠 PATCH /itinerary/:id
Update an existing itinerary day.

```json
{
  "date": "2025-09-11",
  "activities": [
    {
      "title": "Solo Tea House Visit",
      "start_time": "11:00",
      "end_time": "12:30"
    }
  ]
}
```

### 🏨 GET /accommodations/search
**Query Parameters**:
```
location=Shanghai
personality=introvert,night_owl
max_price=120
radius_km=5
```

**Response:**
```json
[
  {
    "id": "hotel_998",
    "name": "Tranquil Stay Inn",
    "price_per_night": 95,
    "distance_to_itinerary_km": 3.2,
    "amenities": ["free_wifi", "soundproof_rooms", "late_checkin"],
    "reviews_rating": 4.5,
    "booking_url": "https://booking.example.com/tranquil-stay"
  }
]
```

### 🍜 GET /restaurants/recommendations
**Query Parameters**:
```
location=Singapore
personality=adventure_junkie,night_owl
diet=vegetarian
max_price=40
```

**Response:**
```json
[
  {
    "id": "rest_401",
    "name": "Late Night Laksa",
    "cuisine": "Peranakan",
    "open_until": "02:00",
    "features": ["vegetarian_options", "menu_translation"],
    "menu_url": "https://menu.example.com/lnl"
  }
]
```

### 📖 GET /restaurants/:id/menu
```json
{
  "restaurant_id": "rest_401",
  "menu": [
    {
      "item": "Vegetarian Laksa",
      "translated_name": "Vegetarian Spicy Noodle Soup",
      "price": 12.5,
      "popular": true
    }
  ]
}
```

### 🚕 POST /travel/estimate
```json
{
  "from": "Gardens by the Bay, Singapore",
  "to": "Night Safari, Singapore",
  "mode": "taxi"
}
```

**Response:**
```json
{
  "travel_time_minutes": 22,
  "estimated_cost": {
    "currency": "SGD",
    "amount": 20.5
  }
}
```

### ❗ Common Error Responses

| Code | Message                |
|------|------------------------|
| 400  | Invalid request format |
| 401  | Unauthorized           |
| 404  | Resource not found     |
| 500  | Internal server error  |
