# Real-time state propagation in asynchronous systems (Backend)

Backend API for a university final-year project application.

## Project Context

- Application: **Health and Fitness Tracking Application**
- Research/dissertation title: **Real-time state propagation in asynchronous systems**
- Scope of this repository: **backend only** (Spring Boot API)

## Related Repository

- Frontend (React): [https://github.com/MyNameIsHamzah/async-system-frontend-react](https://github.com/MyNameIsHamzah/async-system-frontend-react)

## What This Service Provides

- BMI calculation endpoint
- TDEE (Total Daily Energy Expenditure) calculation endpoint
- CORS enabled for all origins (to support frontend integration during development)

## Tech Stack

- Java 8
- Spring Boot 2.6.3
- Maven (with Maven Wrapper)

## Getting Started

### Prerequisites

- JDK 8 installed

### Run locally

```bash
./mvnw clean install
./mvnw spring-boot:run
```

By default, the API runs at:

```text
http://localhost:8080
```

## API Reference

Base path:

```text
/api/v1/calculate
```

### 1) BMI

- Endpoint: `/BMI`
- Parameters:
- `weight` (Double, kg)
- `height` (Double, meters)
- Formula: `weight / (height * height)`
- Response: `Double` rounded to 2 decimal places

Example:

```bash
curl "http://localhost:8080/api/v1/calculate/BMI?weight=70&height=1.75"
```

### 2) TDEE

- Endpoint: `/TDEE`
- Parameters:
- `weight` (Double, kg)
- `height` (Double, meters; converted internally to cm)
- `age` (int)
- `gender` (String; expects `female` for female formula, otherwise male formula is used)
- `activitylevel` (String; one of: `sedentary`, `light exercise`, `moderate exercise`, `heavy exercise`, `athlete`)
- BMR formula used:
- Female: `(10 * weight) + (6.25 * height_cm) - (5 * age) - 161`
- Otherwise: `(10 * weight) + (6.25 * height_cm) - (5 * age) + 5`
- TDEE is derived by multiplying BMR by an activity factor.
- Response: `int`

Example:

```bash
curl "http://localhost:8080/api/v1/calculate/TDEE?weight=70&height=1.75&age=24&gender=male&activitylevel=moderate%20exercise"
```

## Testing

Run tests with:

```bash
./mvnw test
```

Current test coverage is minimal (`contextLoads` smoke test).

## Project Structure

```text
src/main/java/com/example/healthandfitnessappapis/
  - HealthandfitnessappApisApplication.java
  - controllers/userCalculationsController.java
  - models/userCalculations.java
```

## Notes

- This project is an academic backend prototype.
- No authentication, persistence, or advanced validation is currently implemented.
- Query parameter values are case-sensitive in the current implementation.
