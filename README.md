# sandbox

```mermaid
C4Context
    title System Context diagram for Pub Allocation System

    Person(customer, "Pub Goer", "A customer of the pub in need of a drink.")
    System_Ext(pub_roulette, "Random Pub Chooser", "Allows customer to randomly find a pub to go to.")
    System_Ext(pub_reminder, "Weekly Pub Reminder", "Reminds customer to attend a pub they liked from week before.")
    System_Ext(pub_fast_finder, "Quick Pub Chooser", "Allows customer to quickly find a pub with minimal input.")
    System(pubs, "Pubs API", "Allows services to retrieve information about pubs.")
    System_Ext(pub_files, "Pub Files", "Monthly pub details provided by pubs.")
    System_Ext(pubs_online, "Pubs Online", "Website that provides real-time pub information.")

    Rel(customer, pub_roulette, "Uses")
    Rel(customer, pub_fast_finder, "Uses")
    Rel_Back(customer, pub_reminder, "Sends e-mails to")
    Rel(pub_roulette, pubs, "Calls")
    Rel(pub_fast_finder, pubs, "Calls")
    Rel(pub_reminder, pubs, "Calls")
    Rel(pubs_online, pubs, "Updates")
    Rel(pub_files, pubs, "Updates")

     UpdateLayoutConfig($c4ShapeInRow="4")

```

```mermaid
graph TB
    subgraph "Row 1: Person"
        customer[Pub Goer]
    end
    subgraph "Row 2: External Systems"
        pub_roulette[Random Pub Chooser]
        pub_fast_finder[Quick Pub Chooser]
        pub_reminder[Weekly Pub Reminder]
        pubs_online[Pubs Online]
        pub_files[Pub Files]
    end
    subgraph "Row 3: System"
        pubs[Pubs API]
    end

    customer -->|Uses| pub_roulette
    customer -->|Uses| pub_fast_finder
    pub_reminder -->|Sends e-mails to| customer
    pub_roulette -->|Calls| pubs
    pub_fast_finder -->|Calls| pubs
    pubs_online -->|Updates| pubs
    pub_files -->|Updates| pubs

    classDef system fill:#aaffaa;
    classDef person fill:#ffaaaa;
    classDef system_ext fill:#ffddaa;
    classDef relation fill:#ffffff,stroke:#333333,stroke-width:2px;
    classDef arrowHead fill:#333333;

    class customer person;
    class pub_roulette,pub_fast_finder,pubs_online system_ext;
    class pubs system;

```

```
 <!-- System_Ext(mail_system, "E-mail system", "The internal Microsoft Exchange e-mail system.")
    System_Ext(mainframe, "Mainframe Banking System", "Stores all of the core banking information about customers, accounts, transactions, etc.")

    Rel(customer, pub_roulette, "Uses")
    Rel_Back(customer, mail_system, "Sends e-mails to")
    Rel_Back(pub_roulette, mail_system, "Sends e-mails", "SMTP")
    Rel(banking_system, mainframe, "Uses")

    UpdateElementStyle(customerA, $fontColor="red", $bgColor="grey", $borderColor="red")
    UpdateRelStyle(Person, SystemAA, $textColor="blue", $lineColor="blue", $offsetX="5")
    UpdateRelStyle(SystemAA, SystemE, $textColor="blue", $lineColor="blue", $offsetY="-10")
    UpdateRelStyle(SystemAA, SystemC, $textColor="blue", $lineColor="blue", $offsetY="-40", $offsetX="-50")
    UpdateRelStyle(SystemC, customerA, $textColor="red", $lineColor="red", $offsetX="-50", $offsetY="20")

    UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1") -->
```

```mermaid
C4Context
    title System Context diagram for Internet Banking System
    Enterprise_Boundary(b0, "BankBoundary0") {
    Person(customerA, "Banking Customer A", "A customer of the bank, with personal bank accounts.")
    Person(customerB, "Banking Customer B")
    Person_Ext(customerC, "Banking Customer C", "desc")

    Person(customerD, "Banking Customer D", "A customer of the bank, <br/> with personal bank accounts.")

    System(SystemAA, "Internet Banking System", "Allows customers to view information about their bank accounts, and make payments.")

    Enterprise_Boundary(b1, "BankBoundary") {

        SystemDb_Ext(SystemE, "Mainframe Banking System", "Stores all of the core banking information about customers, accounts, transactions, etc.")

        System_Boundary(b2, "BankBoundary2") {
        System(SystemA, "Banking System A")
        System(SystemB, "Banking System B", "A system of the bank, with personal bank accounts. next line.")
        }

        System_Ext(SystemC, "E-mail system", "The internal Microsoft Exchange e-mail system.")
        SystemDb(SystemD, "Banking System D Database", "A system of the bank, with personal bank accounts.")

        Boundary(b3, "BankBoundary3", "boundary") {
        SystemQueue(SystemF, "Banking System F Queue", "A system of the bank.")
        SystemQueue_Ext(SystemG, "Banking System G Queue", "A system of the bank, with personal bank accounts.")
        }
    }
    }

    BiRel(customerA, SystemAA, "Uses")
    BiRel(SystemAA, SystemE, "Uses")
    Rel(SystemAA, SystemC, "Sends e-mails", "SMTP")
    Rel(SystemC, customerA, "Sends e-mails to")

    UpdateElementStyle(customerA, $fontColor="red", $bgColor="grey", $borderColor="red")
    UpdateRelStyle(customerA, SystemAA, $textColor="blue", $lineColor="blue", $offsetX="5")
    UpdateRelStyle(SystemAA, SystemE, $textColor="blue", $lineColor="blue", $offsetY="-10")
    UpdateRelStyle(SystemAA, SystemC, $textColor="blue", $lineColor="blue", $offsetY="-40", $offsetX="-50")
    UpdateRelStyle(SystemC, customerA, $textColor="red", $lineColor="red", $offsetX="-50", $offsetY="20")

    UpdateLayoutConfig($c4ShapeInRow="3", $c4BoundaryInRow="1")
```