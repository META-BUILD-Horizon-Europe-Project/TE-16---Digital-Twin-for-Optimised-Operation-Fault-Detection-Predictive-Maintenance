## **General Information and Purpose**

**TE ID & Name:** TE-16 - Building Digital Twins (Digital Twin for Optimised Operation, Fault Detection & Predictive Maintenance)

**Description and purpose:** TE-16 delivers a **building-level Digital Twin (DT)** supporting **optimised operation**, **real-time fault detection** and **predictive maintenance** for electrified buildings.

The service integrates **hybrid physical and data-driven models**, **advanced analytics** and **machine-learning techniques** to represent the dynamic behaviour of building systems and assets, enabling:

- continuous monitoring of operational performance
- short- and mid-term operational optimisation
- early detection and diagnosis of faults
- prediction of **Remaining Useful Lifetime (RUL)** of critical equipment

The Digital Twin acts as a **decision-support tool** for facility managers, energy managers and service operators, supporting **energy savings**, **improved reliability**, **user comfort** and **grid flexibility participation**.

An initial DT prototype was developed before pre-pilot (**D4.1**), with progressive enrichment and pilot-specific calibration in **D4.2** and **D4.3**.

**Lead partner/Contact Information:**

- Lead (TE-16): **TECNALIA**
- In collaboration with: **EDF**

**Associated Task:** **T4.6** - Digital Twin for buildings optimised operation, fault detection and predictive maintenance

**Target Deliverables:**

- **D4.1** - Initial release
- **D4.2** - Pilot-ready update
- **D4.3** - Final validated version

**Target Front Runners/Pilots:** **FR6 - Spanish pilot**

**Other possible pilots for TE scalability:**

- META-BUILD demonstration buildings where **TECNALIA** and **EDF** are involved
- Electrified buildings with monitoring infrastructure

**Architecture Diagram:**
![Model](methodology.png)

This architecture provides a high-level view of the system components, their connections and the communication protocols used throughout the META-BUILD Digital Twin framework.

**Assets covered:**

- **Heat Pumps (HPs)**
- **PV / PVT systems and inverters**
- **Auxiliary HVAC components** (valves, pumps, controllers)
- **Sensors and meters** (temperature, power, flow, status, occupancy)

**Operational focus:**

- **Zone-level HVAC operation**
- **Building-level energy planning**
- **Equipment health and degradation**
- **Interaction between assets** (thermal-electrical coupling)

The Digital Twin operates as a **hybrid cloud-edge service** composed of the following layers:

1. **Data Ingestion Layer**
   - Inputs from sensors, BMS / EMS, asset controllers and historical databases
   - Potential integration through the **TE-10 interoperability layer**

2. **Hybrid Modelling Layer**
   - **Physical models** (Modelica-based representations)
   - **Data-driven models** (e.g. RC, ARX)
   - **Metamodels** for diagnosis and prognosis

3. **Analytics & Intelligence Layer**
   - Energy-use planning based on forecasting
   - Operational optimisation algorithms
   - Fault detection and diagnosis (**FDD**)
   - Reinforcement learning-based policy refinement

4. **Service Exposure Layer**
   - APIs for dashboards
   - DT visualisation
   - Alerts
   - Integration with other WP4 services such as **T4.4** and **T4.5**

## **Functional Requirements**

Describe the core capabilities of the TE and the functions it provides.  
Focus on what the TE does, not how it is implemented.

- **Digital Twin Representation:** Provide dynamic simulation of building energy behaviour and system interactions, synchronised with real operational data and advanced module outputs.
- **Energy Use Planning:** Support daily and weekly energy-use planning, recommend load shifting and prioritisation strategies, and evaluate scenarios under different tariffs, weather and demand profiles.
- **Optimised Operation:** Analyse building occupancy profiles and preferences, evaluate thermal comfort and IAQ, and support automated HVAC control based on multi-objective optimisation of comfort, IAQ and energy consumption.
- **Predictive Maintenance & Fault Detection:** Identify faulty components and fault types, detect abnormal behaviour and deviations from expected performance, trigger early warnings and support maintenance prioritisation.
- **Decision Support:** Provide interpretable indicators, alerts and recommendations, enable what-if analysis and mid-term planning, and support advanced HVAC operational logics.
- **Hybrid Analytics Integration:** Combine physical, data-driven and AI-based methods for building-level monitoring, planning and operational optimisation.
- **Cross-Service Support:** Produce outputs that can feed optimisation, maintenance and flexibility-related services within the WP4 stack.

## **Non-Functional Requirements**

- **Performance:**
  - Supports **near-real-time monitoring** with **minutes-level latency**
  - Supports **batch and periodic analytics** for optimisation and prognosis
  - Designed for **scalable execution** across different building and zone typologies
- **Reliability and Availability:**
  - Designed for **continuous operation** during pilot phases
  - Supports **offline analysis** using historical data
- **Security (authentication, authorisation, data encryption, data privacy):**
  - **Authentication:** Authenticated APIs for monitoring and service access
  - **Authorisation:** Role-based access control
  - **Encryption:** Secure communication using **TLS**
  - **Privacy:** No personal data processing; focus on operational and technical building data
  - **Compliance:** GDPR-compliant data handling

## **Service Interfaces**

#### **Interface Types**

- **REST APIs** for data ingestion and analytics results
- **Optional message-based interfaces** (e.g. MQTT) for events and alerts
- **Dashboard integration** for facility managers and operators

#### **Typical Outputs**

- **Fault alerts** and diagnostic reports
- **Health indicators** and degradation indices
- **Optimised operation recommendations**
- **KPIs** for energy, performance and reliability

**Potential interoperability note:** Interfaces may be exposed through standardised APIs and data models defined in **T4.1 (ED)**.

#### **API Endpoints**

For each exposed endpoint:

- Request Parameters
- Request Example
- Response Parameters
- Response Example
- Error Handling

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 1</strong></p></th><th><p><strong>Get Latest Sensor Reading</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/api/v1/sensors/{sensorId}/latest</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>GET</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Returns the latest available reading for a given sensor in the Digital Twin platform.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>sensorId (path, required): Sensor identifier, e.g. ieq-co2-01</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>GET /api/v1/sensors/ieq-co2-01/latest</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>sensorId (string): Sensor identifier</li><li>value (float): Latest measured value</li><li>unit (string): Unit of measurement</li><li>timestamp (ISO8601): Reading timestamp</li><li>location (string): Sensor location</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"sensorId": "ieq-co2-01",<br>"value": 487.5,<br>"unit": "ppm",<br>"timestamp": "2026-02-04T10:32:15Z",<br>"location": "office-floor-2"<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>404 Not Found: {"error":{"code":"SENSOR_NOT_FOUND","message":"Sensor does not exist"}}</li><li>503 Service Unavailable: {"error":{"code":"DATABASE_UNAVAILABLE","message":"InfluxDB unavailable"}}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 2</strong></p></th><th><p><strong>Get Sensor Time Series History</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/api/v1/sensors/{sensorId}/history</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>GET</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Returns historical time-series data for a given sensor, with optional aggregation and time windowing.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>sensorId (path, required): Sensor identifier</li><li>start (query, required): Start time (ISO8601 or relative, e.g. -24h)</li><li>stop (query, optional): End time (default: now)</li><li>aggregation (query, optional): mean, max, min, sum</li><li>window (query, optional): Aggregation window, e.g. 5m, 1h, 1d</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>GET /api/v1/sensors/ieq-co2-01/history?start=-24h&amp;aggregation=mean&amp;window=1h</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>sensorId (string)</li><li>unit (string)</li><li>aggregation (string)</li><li>window (string)</li><li>data (array): Timestamped values</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"sensorId": "ieq-co2-01",<br>"unit": "ppm",<br>"aggregation": "mean",<br>"window": "1h",<br>"data": [<br>{"timestamp": "2026-02-03T11:00:00Z", "value": 425.3},<br>{"timestamp": "2026-02-03T12:00:00Z", "value": 512.8},<br>{"timestamp": "2026-02-03T13:00:00Z", "value": 498.1}<br>]<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>400 Bad Request: {"error":{"code":"INVALID_TIME_RANGE","message":"Invalid time range"}}</li><li>400 Bad Request: {"error":{"code":"INVALID_AGGREGATION","message":"Unsupported function"}}</li><li>401 Unauthorized: {"error":{"code":"UNAUTHORIZED","message":"Invalid token"}}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 3</strong></p></th><th><p><strong>Get Zone IEQ Metrics</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/api/v1/zones/{zoneId}/ieq</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>GET</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Returns indoor environmental quality metrics and occupancy information for a given zone.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>zoneId (path, required): Zone identifier, e.g. office-floor-2</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>GET /api/v1/zones/office-floor-2/ieq</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>zoneId (string)</li><li>timestamp (ISO8601)</li><li>metrics (object): Temperature, humidity, CO2, VOC index, PM2.5, noise</li><li>occupancy (object): Occupancy detection and count</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"zoneId": "office-floor-2",<br>"timestamp": "2026-02-04T10:35:00Z",<br>"metrics": {<br>"temperature": {"value": 22.4, "unit": "°C"},<br>"humidity": {"value": 45.2, "unit": "%"},<br>"co2": {"value": 487.5, "unit": "ppm"},<br>"voc_index": {"value": 95, "unit": "index"},<br>"pm25": {"value": 8.3, "unit": "µg/m³"},<br>"noise": {"value": 42.1, "unit": "dB"}<br>},<br>"occupancy": {"detected": true, "count": 12}<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>404 Not Found: {"error":{"code":"ZONE_NOT_FOUND","message":"Zone does not exist"}}</li><li>401 Unauthorized: {"error":{"code":"UNAUTHORIZED","message":"Invalid token"}}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 4</strong></p></th><th><p><strong>Get Equipment Telemetry</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/api/v1/equipment/{equipmentId}/telemetry</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>GET</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Returns telemetry for HVAC or other building equipment over a selected time range.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>equipmentId (path, required): Equipment identifier, e.g. fancoil-ref-01</li><li>start (query, optional): Start time (default: -1h)</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>GET /api/v1/equipment/fancoil-ref-01/telemetry?start=-6h</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>equipmentId (string)</li><li>type (string)</li><li>data (array): Timestamped telemetry records</li><li>units (object): Units for temperature, airflow and power values</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"equipmentId": "fancoil-ref-01",<br>"type": "fancoil",<br>"data": [{<br>"timestamp": "2026-02-04T10:30:00Z",<br>"supplyAirTemp": 28.5,<br>"returnAirTemp": 22.1,<br>"airFlowRate": 320.5,<br>"waterSupplyTemp": 45.2,<br>"waterReturnTemp": 38.7,<br>"thermalPower": 2.85,<br>"electricalPower": 0.12<br>}],<br>"units": {<br>"temperature": "°C",<br>"airFlowRate": "m³/h",<br>"thermalPower": "kW",<br>"electricalPower": "kW"<br>}<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>404 Not Found: {"error":{"code":"EQUIPMENT_NOT_FOUND","message":"Equipment not found"}}</li><li>401 Unauthorized: {"error":{"code":"UNAUTHORIZED","message":"Invalid token"}}</li></ul></td></tr></tbody></table></div>

<div class="joplin-table-wrapper"><table><tbody><tr><th><p><strong>Endpoint 5</strong></p></th><th><p><strong>Get Aggregated Energy Consumption</strong></p></th></tr><tr><td><p><strong>Url</strong></p></td><td><p>/api/v1/energy/consumption</p></td></tr><tr><td><p><strong>Method</strong></p></td><td><p>GET</p></td></tr><tr><td><p><strong>Description</strong></p></td><td><p>Returns aggregated energy consumption for a selected period, with optional grouping by floor, equipment or type.</p></td></tr><tr><td><p><strong>Headers</strong></p></td><td><ul><li>Authorization: Bearer &lt;token&gt;</li></ul></td></tr><tr><td><p><strong>Request Parameters</strong></p></td><td><ul><li>start (query, required): Period start</li><li>stop (query, optional): Period end (default: now)</li><li>groupBy (query, optional): floor, equipment, type</li></ul></td></tr><tr><td><p><strong>Request</strong><br><strong>Example</strong></p></td><td><p>GET /api/v1/energy/consumption?start=-7d&amp;groupBy=floor</p></td></tr><tr><td><p><strong>Response Parameters</strong></p></td><td><ul><li>period (object): Start and end of queried period</li><li>totalConsumption (object): Total value and unit</li><li>breakdown (array): Grouped consumption entries</li></ul></td></tr><tr><td><p><strong>Response</strong><br><strong>Example</strong></p></td><td><p>Example {<br>"period": {<br>"start": "2026-01-28T00:00:00Z",<br>"stop": "2026-02-04T10:40:00Z"<br>},<br>"totalConsumption": {"value": 1245.8, "unit": "kWh"},<br>"breakdown": [<br>{"floor": "floor-1", "consumption": 412.3, "unit": "kWh"},<br>{"floor": "floor-2", "consumption": 523.1, "unit": "kWh"},<br>{"floor": "floor-3", "consumption": 310.4, "unit": "kWh"}<br>]<br>}</p></td></tr><tr><td><p><strong>Error Handling</strong></p></td><td><ul><li>400 Bad Request: {"error":{"code":"INVALID_PARAMETERS","message":"Invalid parameters"}}</li><li>401 Unauthorized: {"error":{"code":"UNAUTHORIZED","message":"Invalid token"}}</li><li>429 Too Many Requests: {"error":{"code":"RATE_LIMIT_EXCEEDED","message":"Rate limit exceeded"}}</li><li>503 Service Unavailable: {"error":{"code":"DATABASE_UNAVAILABLE","message":"Database unavailable"}}</li></ul></td></tr></tbody></table></div>

#### **General Error Response Format**

```json
{
  "error": {
    "code": "SENSOR_NOT_FOUND",
    "message": "Sensor 'ieq-co2-99' not found in database",
    "timestamp": "2026-02-04T10:45:00Z",
    "path": "/api/v1/sensors/ieq-co2-99/latest"
  }
}
