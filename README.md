# NBS Infiltration Model

Provided by: **EXUS**

## Description

The NBS Infiltration Model provides infiltration analysis for various nature-based solutions in the Leuven area, including rain gardens, bioswales, permeable pavement, green roofs, constructed wetlands, urban forests, and infiltration trenches.

## Installation Prerequisites

- Docker and Docker Compose installed  
- GitHub Container Registry access to URBREATH organization(```ghcr.io/urbreath```)  
- MinIO credentials for URBREATH storage

## Installation Instructions

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
docker pull ghcr.io/urbreath/infiltration-api:v1.1

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

## Built Image Registry

- Registry URL: ```ghcr.io/urbreath```
- Image Name:  ```ghcr.io/urbreath/infiltration-api:v1.1```
- Version: ```v1.1```

## License
  
This tool is licensed under Proprietary Software Licence - End-User License Agreement (EULA).

## External Technical Resoures

API documentation: [here](https://lisboncouncil.sharepoint.com/sites/URBREATH/Gedeelde%20documenten/Forms/AllItems.aspx?id=%2Fsites%2FURBREATH%2FGedeelde%20documenten%2FGeneral%2FWork%20packages%2FWP3%20URBREATH%20data%20strategy%20and%20tools%2FTask%20T3%2E1%20AI%2Dbased%20algorithms%20and%20tools%2FInfiltration%20Model%2Finfiltration%5Fmodel%5FAPI%5Fdoc%2Emd&parent=%2Fsites%2FURBREATH%2FGedeelde%20documenten%2FGeneral%2FWork%20packages%2FWP3%20URBREATH%20data%20strategy%20and%20tools%2FTask%20T3%2E1%20AI%2Dbased%20algorithms%20and%20tools%2FInfiltration%20Model&xsdata=MDV8MDJ8fDUzYjU1MDQ2ZTM5MDRhYjU0NThiMDhkZTYzZTY1MjA5fGM5Mzg0MGExZTJkNTQyODNhNTBmMGYzODBkNWM2YmJlfDB8MHw2MzkwNTgwMzgwMDMxNTk3NjN8VW5rbm93bnxWR1ZoYlhOVFpXTjFjbWwwZVZObGNuWnBZMlY4ZXlKRFFTSTZJbFJsWVcxelgwRlVVRk5sY25acFkyVmZVMUJQVEU5R0lpd2lWaUk2SWpBdU1DNHdNREF3SWl3aVVDSTZJbGRwYmpNeUlpd2lRVTRpT2lKUGRHaGxjaUlzSWxkVUlqb3hNWDA9fDF8TDJOb1lYUnpMekU1T2poalpqTTJNR0poTldVMFl6UTBORFk1WWpBNVpHUTBZVFV5TXpNM09EVm1RSFJvY21WaFpDNTJNaTl0WlhOellXZGxjeTh4Tnpjd01qQTJPVGs0TkRZNHwxNWQ0NWViMTBlNWU0ZjNjYmM1OTA4ZGU2M2U2NTIwOHw1NDM3MGZmNjdmYmY0NGE4OTM2YmU4YTBhNTcwYjI2YQ%3D%3D&sdata=dDVURWFRYVpwVHhlR0VycDBvM2x2ajkwNzJ2Y29PVnRNWTM5S1htVUoybz0%3D&ovuser=c93840a1%2De2d5%2D4283%2Da50f%2D0f380d5c6bbe%2Cc%2Enichiforov%40exus%2Eai&OR=Teams%2DHL&CT=1772197551888&clickparams=eyJBcHBOYW1lIjoiVGVhbXMtRGVza3RvcCIsIkFwcFZlcnNpb24iOiI0OS8yNjAyMDEwMTExNyIsIkhhc0ZlZGVyYXRlZFVzZXIiOmZhbHNlfQ%3D%3D&SafelinksUrl=https%3A%2F%2Flisboncouncil%2Esharepoint%2Ecom%2Fsites%2FURBREATH%2FGedeelde%2520documenten%2FForms%2FAllItems%2Easpx)
 
  ## User Guide References

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
    }```

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
    }```
    
  ### Output Files
  Results automatically uploaded to MinIO at:
  ```s3://urbreath-public-repo/Leuven/infiltration-model/reports/YYYYMMDD_HHMMSS/```
