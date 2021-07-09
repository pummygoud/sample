# Prime Contracts 

Contracts is the core table for different types of contract information. There are types of Contracts in this table.
- prime_contracts (contracts.type = 'PrimeContract')
    - prime contracts
    - prime contracts potential change orders
    - prime contracts change order packages
- committments (contracts.type != 'PrimeContract')
    - purchaseorder
        - committments
        - committments potential change orders
        - committments change order packages
    - workorder
        - committments
        - committments potential change orders
        - committments change order packages

Document will focus on prime_contracts subject area

# Sources
| tables |
| ----- |
| prime_contracts | 
| projects |
| companies |
| vendors (vendors -> contacts) |
| contractor (vendors -> contacts) |
| architect (users -> contacts) | 
| created_by_users (users -> contacts) |
| assigned_to_users (users -> contacts) |


Notes:


# Data modeling options (descriptions and diagrams)

Previous data modeling options explored around contracts data modeling listed [here](https://github.com/procore/blue-steel/tree/main/data_model_explorations/data_model_areas/contracts_change_orders_line_items)

## [Modeling : PrimeContacts logical model is [here](https://miro.com/app/board/o9J_l7LomVI=/)]
Contracts table is split into PrimeContracts by filtering type = 'PrimeContract'. This option will get prime contracts from the contracts OLTP data into a table structure, `prime_contracts`.

The reason for taking the decision is [here](http://google.com)

![prime_contracts_design](prime_contracts_logical_model.png)
## Data Model
- [**prime_contracts**](https://github.com/procore/ods/blob/main/dbt/models/external/finance/prime_contracts.sql) - Granuality of this object is `prime_contract_id`.
- [**projects**](https://github.com/procore/ods/blob/main/dbt/models/external/core/projects.sql) - Granualarity of this object is `id`. Provides project details related to a `prime_contract_id`
- [**companies**](https://github.com/procore/ods/blob/main/dbt/models/external/core/companies.sql) - Granualarity of this object is `id` , `project_id`. Provides details of companies, project associated to a `prime_contract_id`
- [**contacts**] This table is going to split into users and vendors and these tables will be playing multiple roles w.r.t a `prime_contract_id` like architecht, created_by_user, assigned_to_user, vendors, contractor.
    - [**users**](https://github.com/procore/ods/blob/main/dbt/models/external/core/contacts.sql) - Granualarity of this object is `user_id`.
        -  [**architect**](https://github.com/procore/ods/blob/main/dbt/models/external/core/users.sql) - Provides details of architect associated with a `prime_contract_id`
        - [**created_by_users**](https://github.com/procore/ods/blob/main/dbt/models/external/core/users.sql) - Provides details of created user associated to a `prime_contract_id`
        - [**assigned_by_users**](https://github.com/procore/ods/blob/main/dbt/models/external/core/users.sql) - Provides details of assigned user associated to a `prime_contract_id`
    - [**vendors**](https://github.com/procore/ods/blob/main/dbt/models/external/core/contacts.sql) - Granualarity of this object is `vendor_id`.
        - [**vendors**](https://github.com/procore/ods/blob/main/dbt/models/external/core/vendors.sql) - Provides details of vendors associated to a `prime_contract_id`
        - [**contractor**](https://github.com/procore/ods/blob/main/dbt/models/external/core/users.sql) - Provides details of contractor associated to a `prime_contract_id`


**Pros**:
- place holder 


**Cons**:
- place holder 

