# NBS Infiltration Model API

This repository contains the deployment configuration for the URBREATH NBS (Nature-Based Solutions) Infiltration Model API.

## Overview

The NBS Infiltration API provides infiltration analysis for various nature-based solutions in the Leuven area, including:
- Rain gardens
- Bioswales
- Permeable pavement
- Green roofs
- Constructed wetlands
- Urban forests
- Infiltration trenches

## Prerequisites

- Docker and Docker Compose installed
- GitHub Container Registry access to URBREATH organization
- MinIO credentials for URBREATH storage

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/URBREATH/infiltration-model.git
```

### 2. Login to GitHub Container Registry
```bash
docker login ghcr.io -u YOUR_GITHUB_USERNAME
```

### 3. Run the API
```bash
docker-compose up -d

# Check container status
docker-compose ps

# Check logs
docker-compose logs -f

# Test health endpoint
curl http://localhost:8000/health
```

## API Endpoints

### Health Check
```
GET http://localhost:8000/health
```

### List of Available Weather Presets
```
GET http://localhost:8000/presets
```

### List Available NBS Options
```
GET http://localhost:8000/nbs_options
```

### Run Analysis 
#### Example 1
```
POST http://localhost:8000/analyze_polygon
Content-Type: application/json

{
  "polygon": [
    [4.7005, 50.8798],
    [4.7015, 50.8798],
    [4.7015, 50.8808],
    [4.7005, 50.8808],
    [4.7005, 50.8798]
  ],
  "mode": "preset",
  "weather": "Normal Spring Day"
  "nbs_scenarios": [
    "bioswale"
}
```
#### Available Presets
- Normal Spring Day: Typical spring conditions with moderate rainfall
- Summer Storm: Heavy summer storm with intense rainfall
- Extreme Event: Extreme precipitation and saturated soils
- Winter Conditions: Cold winter rain with wet antecedent conditions

#### Available NBS Scenarios
- Existing conditions ('existing_conditions')
- Rain gardens ('rain_garden')
- Bioswales ('bioswale')
- Permeable pavement ('permeable_pavement')
- Green roofs ('green_roof_extensive')
- Constructed wetlands ('constructed_wetland')
- Urban forests ('urban_forest')
- Infiltration trenches ('infitlration_trench')


#### Example 2
```
POST http://localhost:8000/analyze_polygon
Content-Type: application/json

{
  "polygon": [
    [4.4250, 50.8000],
    [4.4350, 50.8000],
    [4.4350, 50.8050],
    [4.4250, 50.8050],
    [4.4250, 50.8000]
  ],
  "mode": "custom",
  "weather": {
    "temperature": 15.0,
    "precipitation": 20.0,
    "humidity": 75.0,
    "antecedent_precip_7d": 20.0
  },
  "nbs_scenarios": [
    "bioswale"
  ]
}
```

## Output Files
Results automatically uploaded to MinIO at:
```
s3://urbreath-public-repo/Leuven/infiltration-model/reports/YYYYMMDD_HHMMSS/
```





