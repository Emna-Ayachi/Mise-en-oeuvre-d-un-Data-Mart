# Sales Data Mart - Pentaho ETL Project

## Overview
This project implements a **Data Mart for sales analysis** using **Pentaho Data Integration (PDI) 11** (Spoon) and **MySQL**. It transforms operational data from a source database ("Prod" schema) into a star schema Data Mart ("ventesDM") optimized for OLAP queries on sales by time, customers, and products.[file:1]

**Author**: Emna Ayachi, GLSI-2A, Institut Supérieur des Technologies de l’Information et de la Communication (ISTIC), University of Carthage – April 2026[file:1]

## Key Objectives
- Design a star schema with dimensions (Time, Products, Customers) and fact table (Sales).[file:1]
- Build complete ETL processes: Extract from MySQL Prod, Transform (aggregations, deduplication), Load into Data Mart.[file:1]
- Validate data integrity and quality.[file:1]

## Technologies
- **Database**: MySQL Server 8.3, MySQL Workbench 8.3[file:1]
- **ETL Tool**: Pentaho Data Integration 11 Community Edition[file:1]
- **Connector**: MySQL JDBC Driver 9.6.0[file:1]

## Schema Design (Star Model)
| Table       | Key Fields                  | Purpose                  |
|-------------|-----------------------------|--------------------------|
| DimTemps   | idJours (DATE PK), Mois (INT) | Time dimension (day/month)[file:1] |
| DimProduits| idProd (INT PK), NomProd, CatProd | Products by category[file:1] |
| DimClients | idCl (VARCHAR PK), NomCl, PaysCl | Customers by country[file:1] |
| FactVentes | Quantite (INT), Montant (DOUBLE), FKs | Aggregated sales facts[file:1] |

## Setup Instructions
1. **Install MySQL**: Set up MySQL Server and Workbench. Import `ProductionDumpExemple.sql` to create "Prod" schema.[file:1]
2. **Create Data Mart**: Use MySQL Workbench to generate and run the Data Mart schema script (star model).[file:1]
3. **Install Pentaho**: Download PDI-CE-11.x.x, extract, add MySQL JDBC jar to `lib/`, launch `spoon.bat` as admin.[file:1]
4. **Configure Connections**:
   - Source: `connectprod` (localhost:3306/prod)
   - Target: `connectdatamart` (localhost:3306/ventesDM)[file:1]
5. **Run ETL**: Open and execute the main transformation (includes product/client/time dimensions and sales facts ETL).[file:1]

## ETL Processes
- **Products**: SELECT from `produits` + `categories`, load with category mapping.[file:1]
- **Clients**: SELECT Codeclient, Societe, Pays from `clients`.[file:1]
- **Time**: Extract dates from `commandes`, deduplicate by day/month.[file:1]
- **Sales Facts**: Aggregated SUM(Quantite), SUM(Montant) GROUP BY date, product, client.[file:1]

## Validation
- 77 products loaded (e.g., Chai - Boissons).[file:1]
- 20 clients (e.g., ALFKI - Germany).[file:1]
- Sales facts verified for integrity and aggregation consistency.[file:1]

## Results
The Data Mart supports:
- Temporal sales analysis (daily/monthly).[file:1]
- Product category breakdowns.[file:1]
- Customer sales by country.[file:1]

Ready for BI dashboards or further OLAP tools.

## Project Report
Full documentation in [Datawarehouse.pdf](Datawarehouse.pdf).[file:1]

## License
MIT License – feel free to use and extend.
