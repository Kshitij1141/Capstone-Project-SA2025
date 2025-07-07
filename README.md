# Dynamic Pricing for Urban Parking Lots
---
A capstone project for **Summer Analytics 2025**
---
Hosted by the **Consulting & Analytics Club × Pathway**  
---

---

##  Overview

Urban parking is a scarce and often mismanaged resource. 
Fixed pricing models frequently cause overcrowding in 
high-demand zones and underuse in others. 
Our solution introduces a real-time, data-driven **dynamic 
pricing engine** across 14 city parking lots. By 
leveraging **machine learning** and **economic principles,** the 
system intelligently adjusts prices based on fluctuating 
demand, environmental context, and competitor behavior 
All implementations are built from scratch using  
**NumPy,** **Pandas,** and **Pathway.**



## Tech Stack


| Feature              | Tools/Libraries                     |
|----------------------|-------------------------------------|
| Programming Language | Python                              |
| Data Manipulation    | Pandas, NumPy                       |
| Stream Processing    | Pathway                             |
| Visualization        | Bokeh (for real-time plotting)      |
| Development Platform | Google Colab / Jupyter Notebooks    |




---

## Architecture Diagram

---

![Architecture Diagram](https://github.com/user-attachments/assets/40f9fdd1-d564-47fc-9e50-c2c61a073941)

---



## Project architecture and workflow:

The purpose of this project is to model an urban parking lot's **real-time dynamic pricing system**. Data preprocessing, pricing logic, Pathway real-time simulation, and Bokeh visualization are all integrated into the architecture.

###  Workflow Steps:

1. **Data Ingestion**
- A dataset with records from 14 parking spaces spanning 73 days is loaded.

- Date and time fields are combined to create time features.

---

2. **Features Engineering**
- Important features were derived, including:

- `occupancy_rate` = Occupancy / Capacity

-   Normalized traffic level and queue length

- Special event flag (`IsSpecialDay`)

- Weighting by vehicle type (bike = 0.5, car = 1.0, etc.)

----

3. **Baseline Linear Pricing(Model 1)**
- Price increases linearly with occupancy.

- Formula used:  

    ```

    Price = Base_Price + α × (Occupancy / Capacity)

   ```
---

4. **Demand-Based Pricing (Model 2)**

 - Key features (occupancy, traffic, events, vehicle type, and queue) are used to create a weighted demand function

- Normalized demand is used to smoothly adjust the price.

- The formula is as follows: 
 

   ```
    Price = Base_Price × (1 + λ × Normalized_Demand) 


   ```

---

5. **Competitive Pricing (Model 3)**

-By utilizing competitor pricing and location to compare with neighboring parking lots, the Model     
 2 is improved.

- Price is dynamically adjusted:
- Reduce if overworked and cheaper competitors are available.
- Increase if the prices of competitors are higher.

---

6. **Real-Time Simulation with Pathway**

- Information is streamed as though it were coming in real time.
- Maintaining timestamp order and consistently applying pricing logic are two uses for Pathway.
- Provide current prices for each lot.

---

7. **Bokeh Visualization**

- Time-series plots display each model's price change over time.
- Pricing decisions in comparison to competitors are highlighted by comparative bar charts.
- Bokeh is utilized in the notebook because of its interactive and real-time plotting features.

---

 ###  Summary of Key Modules:

- `Feature Engineering & Preprocessing`- Taking useful characteristic out of unprocessed data.

- `Model Definitions` - Every pricing model was developed gradually and logically.

- `Real-Time Processing` - Pathway's streaming table and UDF logic were used to simulate.

- `Visualization` - Using easily comprehensible plots, the model behavior was explained.

---

## Additional Notes and Assumptions:

- Demand weights (α, β, γ, δ, ε) were manually selected according to trial and feature importance.

- In order to simulate in real time, timestamped data was fed sequentially into Pathway.

- For simplicity, "Special Days" were handled as binary (1 if special, else 0).

- With weights of 1.0 and 0.5, the vehicle types were narrowed down to two: `car` and `bike`.

- To maintain reasonable bounds, price caps were set between $5 and $20.

- Competitive pricing rerouted when overloaded and used the average prices of neighboring lots
  (same timestamps).        
---




