# Public Health Disease Surveillance Architecture Development

## Project Overview

This project focuses on designing and implementing a public health disease surveillance system using interoperable healthcare technologies. The goal was to simulate real-world data flow between hospitals, electronic health record (EHR) systems, and a centralized Health Information Exchange (HIE) to monitor and analyze disease outbreaks such as COVID-19.

The system integrates FHIR-based data exchange, synthetic patient data generation, and analytics dashboards to support public health decision-making.

## Objectives

- Build a multi-hospital simulation environment using virtual machines
- Generate synthetic patient and outbreak data
- Implement FHIR-based interoperability using a HAPI-FHIR server
- Integrate EHR systems (OpenEMR) with FHIR
- Enable data aggregation and visualization for outbreak detection
- Analyze trends and identify patterns in disease spread

## System Architecture

The architecture consists of:

- Multiple hospital nodes (Aspirus, Portage, BCMH, MGH)
- A centralized UPHIE (Health Information Exchange) server
- Data exchange via HL7 FHIR APIs
- Synthetic data generation using Synthea
- Visualization using Looker Studio

All virtual machines were successfully configured and networked, ensuring communication across systems.

## Technologies Used

- HAPI-FHIR Server
- Postman
- OpenEMR
- Synthea
- Docker and Linux (Ubuntu)
- Apache and MySQL
- Looker Studio
- Python (Jupyter Notebook)

## Implementation Steps

### 1. Virtual Machine Setup

- Configured five virtual machines representing hospitals and HIE
- Verified connectivity using ping tests
- Ensured compatibility with OpenEMR and HAPI-FHIR

### 2. OpenEMR Installation and Security

- Installed and configured OpenEMR

Secured MySQL using:

```bash
sudo mysql_secure_installation
```

Updated Apache configuration to restrict access

Security limitations identified:

- Use of HTTP instead of HTTPS
- Risk of session hijacking due to unencrypted cookies

### 3. Synthetic Data Generation (Synthea)

- Generated patient data for multiple hospitals
- Simulated outbreak distributions

| Hospital | Population % | COVID Patients |
| --- | --- | --- |
| Aspirus | 0.4% | 20 |
| Portage Health | 0.5% | 45 |
| BCMH | 2% | 140 |
| MGH | 6% | 1200 |

Challenges included:

- Java compatibility issues
- Converting percentages into patient counts
- Managing large FHIR JSON datasets

### 4. HAPI-FHIR Server Setup

- Installed and configured HAPI-FHIR server
- Verified system resources and port availability

Used commands such as:

```bash
free -h
sudo lsof -i :8080
```

### 5. FHIR API Integration

- Created FHIR resources using POST requests in Postman

Example endpoint:

```text
http://localhost:8090/fhir/Practitioner
```

Successfully received 201 Created responses

Error handling included:

- 400 Bad Request
- 404 Not Found
- 500 Internal Server Error

### 6. Data Aggregation and Visualization

- Aggregated hospital data using Python
- Built dashboards in Looker Studio

Key observations:

- Certain hospitals reported higher case counts
- Sharp increases in diagnosis dates indicated outbreak spikes

## Key Outcomes

- Developed an end-to-end disease surveillance pipeline
- Enabled real-time FHIR-based data exchange
- Simulated outbreak scenarios across multiple hospitals
- Identified actionable public health insights

## Challenges

- Environment setup and dependency conflicts
- Managing large-scale healthcare datasets
- Debugging API and JSON formatting errors
- Security limitations in OpenEMR

## Future Improvements

- Implement HTTPS for secure communication
- Add real-time data streaming
- Integrate machine learning for outbreak prediction
- Implement OAuth2 or SMART on FHIR authentication
- Deploy system on cloud infrastructure

## Project Dashboard

https://lookerstudio.google.com/reporting/511128a2-9460-4cdf-911b-dac3f8fe3171

## Conclusion

This project demonstrates how interoperability standards such as FHIR, combined with synthetic data and analytics tools, can be used to build scalable public health surveillance systems. It highlights both the capabilities and challenges of integrating distributed healthcare systems for real-time disease monitoring.