## **Carboni – Renewable Energy NFT Offset Platform (Draft v3)**

### **1\. White Paper**

#### **1.1 Problem Statement**

The world urgently needs transparent and trustworthy systems to account for renewable energy production and consumption. Current renewable energy certificate (REC) systems face several critical challenges:

* **Opacity:** Participation is often limited to large utilities and corporations, leaving small-scale producers and individual consumers unable to easily access or benefit from these markets.  
* **Delays:** The verification and issuance of certificates can take weeks or months, creating a significant disconnect between when energy is generated and when it is recognized as an offset.  
* **Detachment from Real-Time Data:** Most REC systems rely on annual matching. This coarse granularity fails to reflect the hourly fluctuations of renewable generation and grid demand, allowing for mismatches that can overstate climate benefits and inadvertently increase carbon emissions.  
* **Limited Data Trust:** Current systems depend heavily on manual reporting and intermediaries, making it difficult to guarantee that certificates correspond directly to verified, tamper-proof, meter-level energy data.

Together, these issues reduce transparency, slow market adoption, and weaken public and regulatory confidence in renewable energy offsetting as a credible climate solution.

---

#### **1.2 Vision**

This project leverages **Hedera Guardian** to create a verifiable and transparent digital ecosystem where renewable energy is tokenized.

Our vision is a platform where:

* Every unit of renewable energy is tracked from production to consumption with cryptographic certainty.  
* All raw meter data is logged on the **Hedera Consensus Service (HCS)** for a tamper-proof audit trail.  
* Each device-hour of generation produces a parent **Producer NFT**, which is immediately **fractionalized into fungible tokens (fNFTs)** for liquid trading.  
* Consumers prove their hourly electric energy usage via **Consumption Verifiable Credentials (VCs)**.  
* They offset this consumption by purchasing and retiring **fNFTs**, creating a provable, one-to-one match in time and place (country for now) between clean energy generation and use.

---

#### **1.3 Objectives**

Our primary objectives are to build a platform that can:

* **Enable Liquid Tokenization:** Allow producers to tokenize renewable generation via a parent anchor NFT, immediately fractionalized into fungible kWh tokens (fNFTs) to ensure market liquidity.  
* **Empower Energy Storage:** Integrate energy storage solutions, providing a clear financial incentive for storage operators by allowing them to tokenize stored and released energy.  
* **Ensure Scalable Offsetting:** Provide consumers with an auditable method to track their footprint via **Consumption VCs** and offset it by purchasing and retiring hourly-matched fNFTs.  
* **Guarantee Trust with Multi-Role Governance:** Establish a robust governance framework with distinct roles for **Installers**, **Operators**, and **Government Representatives** to ensure data integrity and regulatory compliance.  
* **Facilitate a Liquid Market:** Support seamless financial settlement using **CEGP** fungible tokens, alongside HBAR internally.  
* **Mobilise more Just green finance:** use the RECs as collateral for green loans to deploy more renewable energy storage and a currency hedge  
* **Build a Scalable Foundation:** Start with a Proof of concept (POC) featuring manual data entry and settlement, designed to scale towards full automation with smart meter integration.

---

### **2\. Project Summary**

The Carboni platform is a DLT platform built on top of a Guardian-based policy framework and other Hedera services that orchestrates a complete lifecycle for renewable energy certificates.

1. **Onboarding:** Producers, Consumers, and Installers undergo a Know Your Customer (KYC) or Know Your Business (KYB) process.  
2. **Device Registration:** Certified **Installers** register and verify energy-producing, consuming, and storage devices.  
3. **Data Validation via HCS:** An **Operator** gateway streams signed smart meter readings to the Hedera Consensus Service (HCS), creating an immutable, real-time audit trail.  
4. **NFT Minting & Fractionalization:** For each device-hour, Guardian mints a parent Producer NFT (which is frozen) and fractionalizes it into a supply of tradable fungible tokens (fNFTs) equal to the energy output.  
5. **Regulatory Oversight:** **Government Representatives** approve the parent NFTs, which unlock the corresponding fNFTs for trading, and set market parameters like grid emission factors and calculate residual mixes.  
6. **Marketplace:** A decentralized marketplace allows Consumers to purchase approved **fungible tokens (fNFTs)** to offset their consumption.  
7. **Offset & Proof:** When a Consumer matches their consumption (proven by a **Consumption VC**) by purchasing and retiring fNFTs, a final **Carbon Offset VC** is issued as immutable proof.  
     
   

![][image1]  
---

### **3\. Roles**

#### **Producer**

* Generates renewable energy (e.g., solar, wind, Hydro).  
* For each device's total production within a one-hour window, a parent **anchor NFT** is minted to their account and immediately frozen (e.g., an NFT representing 3.2 kWh).  
* Simultaneously, a supply of tradable **fungible tokens (fNFTs)**, equivalent to the kWh produced, is minted and sent to the Producer's wallet for sale.  
* (TBD) Each Producer NFT (and its fNFTs) carries an expiry date.

#### **Consumer**

* Consumes electricity from the grid.  
* Consumption is recorded as a **Consumption Verifiable Credential (VC)**, a signed, off-chain proof of usage for a specific hour.  
* Each Consumption VC includes the **carbon emission factor**, updated monthly by the government. That gets exported/reported automatically to their Scope 2 That gets exported/reported automatically to their Scope 2 software.  
* Offsets their carbon footprint by purchasing **fNFTs**, for which they receive a formal Offset VC.

#### **Energy Storage Provider**

* Stores energy and releases it back to the grid, profiting from price arbitrage.  
* Subject to an efficiency loss function (e.g., 100 kWh stored yields \~90 kWh released).  
* **Types:**  
  * **Solar \+ Storage:** Acts only as a Producer.  
  * **Grid Storage:** Acts as a **Consumer** when charging from the grid (receiving a Consumption VC) and a **Producer** when discharging (receiving an anchor NFT and tradable fNFTs).

#### **Installer**

* An authorized entity responsible for the physical installation and registration of energy meters and devices for both Producers and Consumers.  
* Links physical device IDs to the corresponding digital identity (Guardian account), ensuring the authenticity of the hardware source.  
* Paid installation fees.

#### **Operator (IoT Gateway)**

* A gateway service that collects, signs, and streams device readings as messages to the **Hedera Consensus Service (HCS)**, providing the tamper-proof data feed for the entire system.  
* Aggregates data into hourly buckets and provides the trusted data layer between physical devices and the Guardian policy.  
* Leverages anti-tampering features in smart meters and may use AI for anomaly detection to flag suspicious readings for physical inspection.

#### **Government Representatives**

This role is divided into three distinct authorities to ensure clear separation of duties:

* **EgyptERA (Egyptian Electric Utility and Consumer Protection Regulatory Agency)**  
  * **Approves NFT Issuance:** Unfreezes the fungible fNFTs for trading after verifying the parent anchor NFT.  
  * **Sets Emission Factors:** Inputs the official monthly carbon emission value (kg CO2e per kWh) for grid consumption and updates the residual mix accordingly.  
  * **Collects Fees:** Takes a royalty fee for each certificate issued.  
  * **Monitors Market:** Has administrative access to monitor national statistics.  
* **FRA (Financial Regulatory Authority)**  
  * **Approves Brokers:** Licenses financial brokers to trade fNFTs on the marketplace.  
  * **Oversees Transactions:** Audits and approves all financial transactions.  
  * **Manages Collateral Registry:** Maintains a registry for anchor NFTs and fNFTs used as collateral.  
  * **Collects Fees:** Take a royalty per transaction.  
  * **Audits Claims:** Audits the quality and validity of all offset claims and VCs issued.  
* **Tax Authority**  
  * **Collects Transaction Taxes:** Manages tax collection on the basis of fNFT trading.  
    * **Self-Consumption/Offsetting:** No tax is applied.  
    * **Trading/Speculation:** A tax is applied.

#### **Marketplace**

* The decentralized venue for trading **fungible tokens (fNFTs)**.  
* Enforces the floor price set by the Government Representative.  
* Utilizes an **order book** and **matching engine** to facilitate trades, with settlement occurring in **CEGP**.

#### **Finance Role (Future)**

* Provides loans to Producers and storage operators for infrastructure development.  
* Uses future NFT revenue streams for **securitization** or as **collateral** for loans. Loan issuance and repayment are tracked via VCs.  
* **Device registration can be tied to financing approval**, creating a secure workflow for project finance.

**Note on Multi-Signature (Multi-Sig) Governance:** To enhance security and decentralize authority, the platform supports multi-sig configurations for all major roles. This allows organizations to require multiple internal approvals for critical actions, such as a corporation requiring two managers to approve a large fNFT purchase, or a joint-venture solar farm requiring signatures from both partners to sell assets.

---

### **4\. High-Level Design**

#### **4.1 Tokenization: The Anchor NFT \+ Fractional Model**

To ensure both auditability and liquidity, we use a hybrid model:  
---

* A parent **Producer anchor NFT** is minted per device-hour and immediately frozen. It acts as an immutable anchor for auditability, containing all metadata.  
* The anchor NFT is immediately fractionalized into a supply of **fungible tokens (fNFTs)**.  
* **Granularity**: The base unit will be **1 token \= 1 kWh**. To allow for watt-hour (Wh) level precision and accommodate micro-transactions, the token will be configured with **3 decimals**, making it divisible down to `0.001` tokens (equivalent to **1 Wh**).


#### **4.2 Marketplace Mechanics**

The marketplace is more than just a listing service. It includes:

* **Order Book:** Displays buy and sell orders exclusively for **fungible tokens (fNFTs)**.  
* **Matching Engine:** Automatically matches buyers with sellers based on price and time priority.  
* **Settlement Layer:** Handles the atomic swap of CEGP tokens for fNFTs upon a successful trade.  
* **Budget-Based Matching:** Consumers can set a budget, and the system can automatically purchase the optimal mix of available fNFTs to meet their offset goals.

#### **4.3 The Offset Lifecycle: From Mint to Proof**

*(Mint Anchor → Fractionalize → Approve fNFTs → Issue Consumption VC → Trade fNFTs → Retire fNFTs → Burn Anchor → Issue Offset VC)*

1. **Mint & Fractionalize:** A parent Producer NFT is minted and fractionalized into fNFTs.  
2. **Approval:** A Government Representative approves the parent anchor NFT, which unfreezes the fNFTs for trading.  
3. **Consumption Proof:** A Consumer receives a Consumption VC for their hourly usage from the Operator.  
4. **Offset Claim:** The Consumer presents their Consumption VC to the Guardian policy. The policy verifies the VC and that the consumer holds a sufficient balance of corresponding fNFTs, which are then burned.  
5. **Burn:** The fNFTs are destroyed. Once the entire supply is gone, the parent anchor NFT is automatically burned.  
6. **VC Issuance:** Guardian issues the final **Carbon Offset Verifiable Credential (VC)**.

---

### **5\. Use Cases**

#### **5.1 Hourly Matching Example**

This example demonstrates how the hourly matching mechanism ensures precise and verifiable offsetting.

#### **🌞 Producers: Three Solar Panel Owners**

| Hour | Producer A (kWh) | Producer B (kWh) | Producer C (kWh) | Tradable Assets Minted |
| :---- | :---- | :---- | :---- | :---- |
| 09:00–10:00 | 5.0 | 25.0 | 3.0 | 5 `fNFT-A-09`, 25 `fNFT-B-09`, 3 `fNFT-C-09` |
| 10:00–11:00 | 6.0 | 30.0 | 4.0 | 6 `fNFT-A-10`, 30 `fNFT-B-10`, 4 `fNFT-C-10` |

*At 09:00, three parent anchor NFTs are created and frozen. A total of 33 tradable fungible tokens (fNFTs) are minted to the producers' wallets.*

#### **⚡ Consumer: Industrial Plant**

| Hour | Consumption (kWh) | Proof Issued |
| :---- | :---- | :---- |
| 09:00–10:00 | 90.0 | Consumption VC (90 kWh) |

*At 09:00, the plant receives a Consumption VC for 90 kWh from the Operator.*

#### **🔗 Hourly Matching Logic (09:00–10:00)**

1. **Offset Request:** The Consumer presents its Consumption VC for 90 kWh to the Guardian policy.  
2. **Market Purchase:** The Consumer purchases all 33 available fNFTs from the 09:00 hour on the marketplace.  
3. **Matching & Burning:** The 33 purchased fNFTs are burned by the Consumer to offset their consumption.  
4. **VC Issuance & Remaining Balance:**  
   * A **Carbon Offset VC is issued** to the Consumer, certifying they have offset **33 kWh**.  
   * The consumer's record shows an unoffset balance of **57 kWh** for that hour.

This method guarantees that every offset claim is tied to a specific unit of energy, generated in a specific hour, with an immutable record of its retirement.

---

#### **5.2 Certificate Tagging for Grid Storage**

This example demonstrates how a grid storage provider uses the "Certificate Tagging" model to create a valuable, time-shifted renewable energy certificate.

#### **🌞 Producer: Solar Farm (SolarCorp)**

At midday, solar generation is at its peak, leading to an abundance of fNFTs on the market, which typically lowers their price.

| Hour | Production (kWh) | Tradable Assets Minted | Market Status |
| :---- | :---- | :---- | :---- |
| 13:00–14:00 | 10,000 | 10,000 `fNFT-SolarCorp-13` tokens | Low Price |

**Action:** SolarCorp's anchor NFT is created, and 10,000 fNFTs are minted to its wallet and listed for sale on the marketplace.

#### **🔋 Storage Provider: Grid Operator (GridBalance)**

GridBalance's strategy is to buy low-value midday fNFTs to "color" their stored energy and sell high-value evening fNFTs. **Topology:** Battery is connected directly to the grid.

| Hour | Action | Grid Interaction (kWh) | Marketplace Activity |
| :---- | :---- | :---- | :---- |
| 13:00–14:00 | **Charge Battery** | Consume 10,000 | **Buy & Retire** 10,000 `fNFT-SolarCorp-13` |
| 19:00–20:00 | **Discharge Battery** | Produce 9,000 | **Mint & Sell** 9,000 `fNFT-GridBalance-19` |

**Actions:**

1. At 1 PM, GridBalance draws 10,000 kWh from the grid and receives a **Consumption VC**.  
2. Simultaneously, it purchases and **retires (burns) 10,000 `fNFT-SolarCorp-13` tokens**. This provides auditable proof that its charging was matched by an equivalent amount of renewable generation.  
3. At 7 PM, it discharges 9,000 kWh, and a new anchor NFT and **9,000 tradable `fNFT-GridBalance-19` tokens** are minted to its wallet.

#### **⚡ Consumer: Industrial Plant (FactoryCo)**

The industrial plant operates during the evening and needs to offset its consumption during peak hours.

| Hour | Consumption (kWh) | Proof Issued |
| :---- | :---- | :---- |
| 19:00–20:00 | 9,000 | Consumption VC (9,000 kWh) |

**Need:** FactoryCo must purchase **9,000 fNFTs** from the 19:00–20:00 hour to offset its consumption and meet its 24/7 carbon-free energy goals.

#### **🔗 Hourly Matching & Arbitrage Logic**

This step-by-step flow demonstrates how the certificate attribute is transferred through time.

1. **The Midday Transaction (13:00–14:00): Proving the "Green" Input**  
   * GridBalance buys **10,000 `fNFT-SolarCorp-13` tokens** for a low price, for example, **100 CEGP**, and immediately retires them. The system's audit trail now shows that the energy stored in the battery is verifiably "green."  
2. **The Evening Transaction (19:00–20:00): Creating the "Green" Output**  
   * GridBalance receives **9,000 `fNFT-GridBalance-19` tokens** from discharging.  
   * FactoryCo purchases these **9,000 fNFTs** for a premium price, for example, **500 CEGP**.  
3. **Final Outcome & Value Creation**  
   * **For the Consumer (FactoryCo):** FactoryCo burns the 9,000 fNFTs and receives an **Offset VC**.  
   * **For the Storage Provider (GridBalance):** They have successfully performed temporal arbitrage. Their profit is the sale price minus the purchase price: `500 CEGP - 100 CEGP = 400 CEGP profit`.  
   * **For the System:** The integrity of the environmental claim is upheld, and a clear financial incentive for building grid-stabilizing storage has been demonstrated.

---

#### **5.3 Maximizing Value (Solar \+ Storage)**

This example shows how a producer with co-located solar panels and a battery can time-shift their *own* generation to sell a certificate at a more valuable time.

#### **🌞 Producer & Storage Provider: Solar Farm (SolarHarvest)**

SolarHarvest owns both solar panels and a battery. Their goal is to avoid selling their fNFTs during the midday solar glut. **Topology**: Solar and Battery are "behind the meter."

| Hour | Solar Generation (kWh) | Action Taken | Grid Export (kWh) | Tradable Assets Minted |
| :---- | :---- | :---- | :---- | :---- |
| 12:00–13:00 | 500 | **Charge On-site Battery** | 0 | **None** |
| 18:00–19:00 | 0 | **Discharge Battery** | 450 | 450 `fNFT-SolarHarvest-18` tokens |

**Actions:**

1. At 12 PM, SolarHarvest generates 500 kWh and stores it. No on-chain assets are created.  
2. At 6 PM, it discharges 450 kWh to the grid. An anchor NFT is created, and **450 `fNFT-SolarHarvest-18` tokens** are minted to its wallet.

#### **⚡ Consumer: Corporate Office (EcoCorp)**

EcoCorp wants to make a premium ESG claim that their offices are "100% solar-powered," even after sunset.

| Hour | Consumption (kWh) | Proof Issued |
| :---- | :---- | :---- |
| 18:00–19:00 | 450 | Consumption VC (450 kWh) |

**Need:** To substantiate their specific marketing claim, EcoCorp must purchase **450 `fNFTs` with a renewable origin** from the 18:00–19:00 hour.

#### **🔗 Hourly Matching & Value Maximization Logic**

This flow shows how storing self-generated energy creates a more valuable asset.

1. **The Midday Decision (12:00–13:00): Store, Don't Sell**  
   * SolarHarvest generates 500 kWh and sees that 12 PM fNFTs are selling for a low price (e.g., **20 CEGP** for 500 tokens). They choose to store the energy instead.  
2. **The Evening Transaction (18:00–19:00): Sell at a Premium**  
   * SolarHarvest receives **450 `fNFT-SolarHarvest-18` tokens**.  
   * EcoCorp purchases these 450 tokens for a premium price (e.g., **150 CEGP**).  
3. **Final Outcome & Value Creation**  
   * **For the Consumer (EcoCorp):** EcoCorp burns the fNFTs and receives a specific Offset VC.  
   * **For the Producer (SolarHarvest):** Their revenue with storage is **150 CEGP**, compared to only **20 CEGP** without it.  
   * **For the System:** This model provides a direct financial incentive for producers to invest in batteries, helping to solve the intermittency of solar power.

*Taken together, these use cases demonstrate the platform's versatility in serving simple hourly matching, complex energy arbitrage, and the value maximization of co-located renewable assets, all within a single, consistent framework.*

---

## **6\. Guardian-Specific Design**

The platform leverages the **Hedera Guardian** framework to orchestrate all interactions through policy blocks, ensuring transparency, compliance, and auditability. Every **Producer NFT** is minted as a frozen regulatory anchor, then immediately **fractionalized into fungible HTS tokens (fNFTs)**. All matching and trading occur **only with fungible tokens**, while the parent anchor NFT preserves lineage and auditability.

---

### **6.1 Policy Blocks**

* **KYC Block**  
    
  * Collects identity and legal documents from Producers, Consumers, Brokers, and Government Representatives.  
  * Ensures compliance with national regulations.


* **Device Registration Block**  
    
  * Installers submit device and facility/plant metadata (e.g., panel model, inverter type, GPS location, number of units).  
  * Guardian validates and links devices to owners.


* **IoT \+ Operator Block (HCS-enabled)**  
    
  * Smart meters stream signed readings through IoT gateways.  
  * Gateways submit hourly readings as **HCS messages** to a dedicated topic.  
  * Guardian subscribes to this topic, ensuring readings are **tamper-proof, timestamped, and auditable**.  
  * Operator Block aggregates readings into hourly totals for NFT minting.


* **Producer NFT \+ Fractionalization Block**  
    
  * For each device-hour, Guardian mints a **Producer NFT** containing metadata (device, GPS, timestamp, kWh).  
      
  * The Producer NFT is frozen and never traded.  
      
  * Guardian automatically mints a corresponding **fungible token supply (fNFTs)** equal to the NFT’s kWh value.  
      
    * Example: `NFT-Solar-13 (10,000 kWh)` → `fNFT-Solar-13` (10,000 tokens, 1 kWh each).

    

  * All trading and offsets occur using these fungible tokens.  
  * fNFTs sold & burned during offsets, and once supply \= 0, **anchor NFT is burned**.


* **Government Approval Block**  
    
  * EgyptERA, FRA, and Tax Authority jointly review Producer NFTs.  
  * Approve/unfreeze their corresponding fractional tokens for trading.  
  * Can update floor price, set emission factors, and enforce compliance.  
  * Deduct royalty/fee from each issuance or transaction.


* **Marketplace Block**  
    
  * Lists approved fungible tokens (`fNFTs`) for sale.  
  * Consumers and Brokers purchase tokens using **CEGP** (primary) or **HBAR** (fallback).  
  * Implements order book \+ matching engine for efficient liquidity.  
  * Supports **budget-based auto-purchase** to optimize consumer offset strategy.


* **Verification & Offset Block**  
    
  * Consumer usage is represented as Consumption VCs (non-tradable) issued by Operators and includes **a carbon emission data** field.  
      
  * To offset, Consumers burn fractional fungible tokens (fNFTs) 1:1 with their consumption kWh.  
      
  * Guardian issues:  
      
    * **Carbon Offset VC** – immutable proof of offset.  
    * **REN% VC** – Verifiable credential stating percentage of renewable coverage.

    

  * Once all fractional tokens from a Producer NFT are retired, the **parent anchor NFT is burned**, ensuring no double-counting.  
    * Audit trail still exists via:  
      * Immutable HCS log of meter data.  
      * Consumption \+ Offset VCs referencing the NFT ID.  
    * This keeps the ledger leaner. On-chain state doesn’t explode with billions of frozen, useless NFTs.

---

### **6.2 NFT \+ Fungible Token Metadata Schema**

Each **Producer NFT (Anchor)** includes:

* Device/Facility ID  
* Owner ID  
* Operator gateway ID  
* Approving entities  
* Timestamp (hourly bucket)  
* Renewable technology type ( solar, wind, hydro, etc.)  
* Energy quantity (kWh)  
* GPS coordinates  
* Expiry date (TBD rule)  
* Finance entity

Each **fungible token (fNFT)** inherits metadata from its parent anchor NFT:

* Parent anchor NFT ID  
* Fractional supply (e.g., 10,000 tokens)  
* kWh equivalence (e.g., 1 token \= 1 kWh)

---

### **6.3 Auditability**

* **Raw Data Audit:** Regulators can replay HCS messages to independently verify meter readings.  
* **Fractional Token Traceability:** Every fNFT maps back to a frozen parent anchor NFT, ensuring 1:1 linkage with real-world energy.  
* **VC Trail:** Final environmental claims are backed by immutable Verifiable Credentials, referencing both fractional tokens and parent anchor NFTs.

With this model, the **marketplace becomes fully fungible (kWh tokens only)** while still retaining the **NFT audit layer for regulators**. This greatly improves liquidity, user experience, and scalability.

---

### **7\. Simplified Proof of Concept (POC)**

To accelerate rollout, a POC will focus on delivering the core lifecycle with reduced automation.

#### **7.1 POC Constraints**

* **Data Input:** Producers manually upload energy production readings (simulated devices).  
* **Operator:** Manual validation replaces automated gateway functions.  
* **Marketplace:** Only **HBAR** is supported at the POC (CEGP introduced later).  
* **Floor Price:** Static, set by Government Representatives.  
* **Matching:** Manual offset matching by the Guardian policy engine.

---

#### **7.2** POC Flow

1. **Producer Onboarding**  
     
   * Registers with Guardian.  
   * Completes KYC verification.  
   * Device registered manually (no IoT integration).

   

2. **Consumer Onboarding**  
     
   * Registers with Guardian.  
   * Completes KYC/KYB verification.

   

3. **Data Entry**  
     
   * Producer uploads daily/weekly production data.  
   * Operator (simulated) validates the data before minting.

   

4. **Approval & Pricing**  
     
   * Government Representative approves or rejects \*\*parent anchor NFTs\*\*, which unlocks the corresponding fNFTs for trading.  
   * Static floor price is enforced.

   

5. **Marketplace**  
     
   * Approved **fNFTs** listed in the marketplace.  
   * Purchases made using HBAR.

   

6. **Offset Proof**  
     
   * Consumer requests offset matching.  
   * fNFTs are burned.  
   * Guardian issues a **Carbon Offset VC** as immutable proof that references the **anchor NFT ID (on ledger history)** \+ fNFT burn transactions.

---

### **8 Attachments**:

1 \- [Fractionalizing a Renewable Energy Certificate](https://docs.google.com/document/d/1j3X5_D4M2ERlIgR1kA_5GJ-V4QhZOaKPVl0v3SKauQQ/edit?usp=sharing)  
2- [VC structure](https://docs.google.com/document/d/13dyAi1zbuJYgv-0JBhfHkK35rJxXICvFLUH7pozvvtA/edit?usp=sharing)

### **Changelog: v2**

\- **Energy Storage provider**: Features a fully detailed Energy Storage Provider role. It explains their business model (arbitrage), the mechanics of efficiency loss, and the different battery types (**Solar \+ Storage vs. Grid Storage**).

\- **Multi-sig Governance**: includes a note stating the need to support multi-sig accounts for all key roles.

\- mentions an **expiry date** for NFTs.  
	\- mentions using **AI for anomaly detection**.

### **Changelog: v3**

\- **Tokenization Model:** Upgraded to Anchor NFTs \+ Fractionalization and Clarified Token Granularity

\- **Consumer Accounting:** Replaced Consumer NFTs with Consumption VCs

\- introduce **"Use Cases"** section.

\- **structural upgrade.**

[image1]: <data:image/png;base64,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ScCBmwnHgFPPn0onQMBZDwEXAm7btsM0hleWgAtMAg7cTDgGXPbs2Y1DtkHAWY/jA+722283jYWbRGzaTEw8I9On/2Uax5Ql4MDNpFfAnT592jgEKUDAWY/jA065deu/prFwcc+efaYxTL3q+3frrbdKzpw55ZZbbpEcOXLIzTfnkJtuutnz3+lNki1bdsmaNZvHrPrTLrJkyaLfikSZOXNmyZgxo1x33XVy7bXX+g5HYGio3gD6hhtu0D/XbNmyeX7mN+mfv3o83HbbbZIrVy6544475O6775Z7771X7r//fnnwwQfl4Ycfljx58kjevHn1K5kLFiwohQoV0hYpUkSKFi0qxYoVk+LFi0uJEiWkZMmS+j0JS5curT8WrmzZslKuXDlt+fLl9aeLVKpUSX90XJUqVaRq1apSrVo1qV69utSoUUNq1qwptWrVktq1a0udOnWkbt26Uq9ePalfv740aNBAGjVqpG3SpIm2WbNm2hYtWkjLli3lsccek1atWskTTzwhbdu2lSeffFLat28vHTp0kE6dOknnzp2lS5cu0q1bN+nRo4f06tVL+vTpIy+88IL07dtXXn75ZXnllVdkwIAB8vrrr8ugQYNk8ODBMmTIEBk6dKgMGzZM3n33XRk+fLh8+OGH8vHHH8uIESPkk08+kdGjR8vnn38uY8aMka+++kq++eYbGTdunEyYMEG+//57+fHHH2XixIkyZcqUZP72228ybdo0+f333+WPP/6QP//80/PP1nT566+/ZMaMGdqZM2fK7NmztX///bfMmTNH5s6dK/PmzZP58+fLggULZOHChbJo0SJZvHix/PPPP7JkyRJZunSpLFu2TJYvXy4rVqyQlStXyqpVq2Tq1KmyZs0aWbt2raxbt067fv162bhxo3bTpk2yefNm2bJlS0Cqx5radkX+/FU9j4P6mILFitYwjV2tjzxS0Rcz4UhIBNyqVaslX74I07ib7dCho/7DEBsbb5qHmB6yBw7cTHrtgVN/p7174Z5s18v0e4VJ7t273zR2taqAC+e/WSERcF4ffji3acxtqr0An3/+hWkcMb0l4MDNpFfA+WNnwKk9zCqSxo//TgYMeFWOHo2UxYv/0Z9Uo3aCeN9W6fnnX9AfUThp0mR9fePGzXLHHXdKz55J993/7Zd27dojb701VL8TgjoSERMT5/tIw8GD35QvvxwjK1euMt2XlCTgrCekAs6rOswxbNi7pvFQ9OTJKP0fHO/zhnZLwIGbcXvAKVVgeS+rw+u//DJFn0LgHduy5V99Oom6vHnzFj1VAaem6jQR73IrV67WAaguR0TklzvvvFN/bGFK56SXLl3GNJaSBJz1hGTAeU3adZ38gedk69dv4Luszqe566679In2xuUQ7ZCAAzcTDgGXWtW5v8ax9JaAs56QDjil94TlHTt2meY5SfVebt772rt3H9N8RLsl4MDNEHD2SsBZjyMDrmLFZq4zIqKiPPRQaa3/+KFDR03bj2iHBBy4GQLOXgk463FkwA0e9IH/fXQ1O3bs4ZWm6AgJOHAzBJy9EnDWQ8DZzJYt2zwPwGjT9wAx2BJw4GYIOHsl4KyHgLMZAg6dIgEHbsZJATd06Cj5/PMJrnH06HGmbTRKwFkPAWczBBw6RQIO3IzTAs5NnDlzxve2I5eSgLOekAu4fXsPSEJ8glSv0tI4y0f7J3v7Ljdu2F6WLFnlNzcwinie1C5HwYiqkpiYKP/tPyQ7duzW57TN+GuucbFLQsChUyTgwM0QcOkHAWcPIRlwlco38TxgzurrIz4a45vX9bmX9bRdmx4yfuwkfblOrSf09Nix43Lu3Dnfsoofvv812XUjat0pBdz58+f111AkPWiTPkalXu22erply3YZ+81EiYuN993mUhBw6BQJOHAzBFz6QcDZQ8gFnIqnlK6rd6BWlxMSEiUuTr2q84xvmZiYWD2Nj0/wjSmio5PG1W2NJCYmRZl/9PkHmfoaivPnL/hi0ou6H2fPntXzrgQBh06RgAM3Q8ClnVIl6hqHkkHA2UPIBZzbIODQKRJw4GacHnDNmnSUd9/5VKpUbCbD3/tMCuWvqncgFClYQ89XR54UnTq8IK8NeEeOHon03bZwgWq+y17y5amop2VK1tfTbs/1l7HfTpJJE6fJyI+/1usfP/ZnadXyWf+baapUbO7bedHl2ZelQL4q8srLb8vrr74nzz3TT4YOGZFseQLOHgg4myHg0CkScOBmQiHgBr32vrzUd4gU9MTV37MX6vE5cxbr6VLDudzFCtf0XTYeBVIYl1eUf7SRlC1VXzq2f17Kl20klT2xmNJy3rH9+w/oaf06bWXWzPn68ldjvjfdhoCzh5AMOP/Dmo+36uq7rB6YFcs39V1PKyWK1jYOpYoCEVX0dN26zVLh0cbyTIcXpaBnTB1OvRQEHDpFAg7cjNMDLpg81a6nceiqIODsIWQCTp1z9s6wT6Ra5RbJxlXARUfH6MvLl6/xxZ0aq1urjaxds1G+/Pw735g/77w9Sr+i1UuPrgP01P+/i5Ur1ul1eFHn2P35+2yZNOl3KVW8jqxatV5HmuLjD8f4zp2bPWuBnvbsNkA2rN/iu70RAg6dIgEHboaASz8IOHsImYBTPNf5JeneLSmyFG+9+ZEOOO+LFFTA+VO0UE19/F4F2fLla/WLFSaMn+ybP/nnP/yWToq1TRv/leXLktajXrmqgk2tw5+JP/4mj5ZpoC8P6D9M/vAEneLNNz6UJ1p18V9UB9wno76VenWSXqFqhIBDp0jAgZsh4NIPAs4eQirgnMTGDVtl1869xuGAIeDQKRJw4GYIuPSDgLMHAs5mCDh0igQcuBmnBVyxwjVcJQEXfAg4myHg0CkScOBmnBRwyri4BB09btK4jf4ScNZDwNkMAYdOkYADN+O0gAs3CTjrcWTADej3tvR9fnBQjchTyjQWDHft2kvAoSMk4MDNEHD2SsBZjyMDTnn8+EltZOSJoBgREWEaS63e+5pW1Ud6GbcfMdgScOBmCDh7JeCsx7EBF2wLFChgGkMMJwk4cDMEnL0ScNZDwF2UgMNwl4ADN0PA2SsBZz0E3EUJOAx3CThwMwScvRJw1kPAXZSAw3CXgAM3Q8DZKwFnPQTcRQk4DHcJOHAzBJy9EnDWQ8BdlIDDcJeAAzdDwNkrAWc9BNxFCTgMdwk4cDMEnL0ScNZDwHmsVKmyZMmSRUqUKCGrVq0xzUcMBwk4cDPhFnClS5fWz2nKnTt3m+YHWwLOegi4i15zzTVa4zhiuEjAgZsJt4BTque0DBkymMbtkICzHgLuouqTGIxjiOEkAQduJhwDLioqxjRmlwSc9RBwiKgl4MDNhGPAOUkCznpCPuC2bt3hONWDyng/EZ0uAQduxqkB9/WYH0zPIaFiIM91BJz1hHzAORH1oDp6NNJ0XxGdLAEHbsapATf9zznG1YQMgTzXEXDWQ8ClA4E8qBGdIgEHboaAs55AnusIOOsh4NKBQB7UiE6RgAM3Q8BZTyDPdQSc9RBwF6lVo7XUq9PWOJwmAnlQIzpFAg7cTDgHXLXKLYxDlhDIcx0BZz2uDbjSJerp6cgRX+tpjaqPSfNmnaS95xfs1yl/6bFC+avpqXqptaJ4kVoyc8Z8fblalZZy5MgxfdnL8eMnpcNTfWTI4I+SjRsJ5EGN6BQJOHAzoRRwA/oP812eNOl3PVUvGlA0bfS0vPP2KKlbq41vmY7t+8i6tZt8z21/z16kpyWK1pZihWtKuTINZffufXrM+xynmDF9rlSq0NR3/fz58xITEyvHjh3X1yMeqSQzZyYtf/jQUd9yXgJ5riPgrMd1ARcbGyexMXHy7Tc/yZeffyc7tu/2hFpVKZCvig64ghFVZM+e/XrZQa8P9zz4kh6oChVwY778TooWqiFdn+vvCzv1gPYy+I0P5PDhoxIdHStnzpyRjRu2+uZ5CeRBjegUCThwM6EScGvWbNTPOcojh4/JoYNH5OiRSF/AFSpQzbMtu2X+vCVSpmTSjooF85dKm9bdZMnilfJ870G+gMuft5JUrdRc76xQz1vTfpuln+O8MacCLsbzfOmP92sr+vQeKHFx8fqyd6eIP4E81xFw1uO6gHMCgTyoEZ0iAQduJlQCzkqu9tDp4491kcTERH05Pj7BMDew5zoCznoIuHQgkAc1olMk4MDNhGPApTeBPNcRcNZDwKUDgTyoEZ0iAQduhoCznkCe6wg46yHg0oFAHtSITpGAAzdDwFlPIM91BJz1hHzAqR+gE03tgxrRKRJw4GacGnDG545QM7XPdQSc9YR8wCnV23tcrREREaaxq9V4PxGdLAEHbsapAac0PneEmsbtSUkCznpcEXBWWKBAAdMYYjhJwIGbcXLAhYMEnPUQcBcl4DDcJeDAzRBw9krAWQ8Bd1ECDsNdAg7cDAFnrwSc9RBwFyXgMNwl4MDNEHD2SsBZjy/gfp74e1h73733m8YQw0kCDtwMAWevBJz1+AJOob4R4ap6FapxDDEcBXAjBJy9EnDWkyzgwpmCBQsahwAAwCUQcPZKwFkPAXcRAg4AwL0QcPZKwFkPAXcRAg4AwL0QcPZKwFkPAXcRAg4AwL0QcPZKwFkPAXcRAg4AwL0QcPZKwFkPAXcRAg4AwL0QcPZKwFkPAXcRAg4AwL0QcPZKwFkPAXcRAg4AwL0QcPZKwFkPAXeRa665RgsAAO6DgLNXAs56KJaLqHg7duyYcRgAAFwAAWevS5cuN41drQQcAACAywnXgIuKijGN2aHaSWIcu1oJOBtR3/wqVVogIiKmq2VK1zGNXY0p4cSAS49wCtQTJ05JTEycafxqJeBsRH3zjT8QREREq928eatp7GpU4XD27Nlkz2lODLjExDPy7bdjTePBtESJEqYxKyTgbISAQ0ybr776up7eeeedUqtWLTl6NFI6duwk48aNl4SE05IpUybfssePn5CePXvJ1q3bfGMzZ86WG264QXbs2GVaN6IbDdeA85ozZ07TWHo7bNg7pjErJeBshIBDTJtFixaVuLgEqVevvgwZ8pYOuHfeeVf/t63MnDmzTJnyq2/5kSNHyaJFi03r+eyzL0xjiG403ANOee2118qjjz5qGk8P1ddSf4uM41ZKwNkIAYeIiMGQgEtSnRO3adMW07iVqr37xrH0kICzEQIOERGDIQF3VnLnzq0Dzv8UCytVe9yCFW9KAs5GCDhERAyGoR5wxYvXcbS5c5czjaVV47ZfSgLORgg4REQMhqEecOFCTEysftsR4/anJAFnIwQcIiIGQwIuNFABp16UZdz+lCTgbORqA+7UqRj5dcpfjrP/S2+Z7isiItonARcaEHCpJ+QDzon8+MOUVD8AEREx/SXgQgMCLvUQcOkAAYeI6CzdHnDNm3SU2jVa+67/+cfffnNTx+JFy+XQwSPG4cvSqcMLya4/1/mlZNcDhYBLPQRcOkDAISI6S7cHXL48FaVW9dbSqMFT0ubxbr6A++nHqb5pbGyc/Pj9r8nGP/rgi6QVeOjW5RU93bVrr56OHztJypVpKAUjqsrx4yf12Pnz5+WZji/6buMNuGlTZ0rJ4nV8AafW/8bAD3zLRUXFSIF8VXzXLwUBl3oIuDTw7787jUPJIOAQEZ2l2wNu374DEh+foC/v33/QN751yw493bFjj2zZvN133bvM1q1J1xVqftIrQM/o60eOHNOq20RHx+j5f/z+t5w7dy7ZbRISEuXfrTtl9659vvGdO/f41hMIBFzqcV3AqV+oiT9NkyFvfqT/E1DF37vn6/oB9lLfIdKrx2t6uUEDh8vTT/Xx/Ycw6PX39bRZk456WqFc46QVehj+/me+y6dPn9b/STzq+a/kB89/Mp+PHu+b54WAQ0R0lm4PuGDw559zjEOWQ8ClHtcFnLf4y5SsJ7VrPp5sl60KOhVwFy5c0AG3auV6OXMm5V8M/4DzsmL5Wj1VAbd61QbD3P9BwCEiOksCLjQg4FKP6wLOCRBwiIjOMtwD7sm2PY1DPmrVeFy+/OI7fQRq2m8zpXmTTvLTD0nnyBUpWF3KlmogA/oP09u7f99B36FahTqvzkoIuNRDwKUDBBwiorMMx4DbvGmb73K7Nj385iRRuWIz+eD9z+WjD7/UL4JQlC5RT48tWbxSX/9w+BdSp+bj8uwz/fR1FW/qSFeti6943bZtl9St1UbOnPnf+W5RUdG+y8cjT/gupwYCLvUQcOkAAYeI6CzDLeC6PPuytGrxrO96ubKN/OYmR8VX0UI1ZPHiFdKq5XNSrHBN/aIIhQo4hTHgXu73lj63XAVcZ79XpSrU+s6eTXqhQ2peeeoPAZd6CLh0gIBDRHSW4RZwTsH/FaupgYBLPSEfcEWK1HScBQpUS/UDEBER018CLjQg4FJPSAec8uTJKP3Dvlrz5s1rGrtajfcVERHtkYALDQi41BPyAWeVERERpjFERHSHBFxoQMClHgLuogQcIqJ7DfWAmzDhV/nyyx/DQgIudRBwFyXgEBHda6gHnFJ9Hmm4aNz2lCTgbISAQ0TEYOiGgMPkEnA2QsAhImIwJODcJwFnIwQcIiIGQwLOfRJwNkLAISJiMCTg3CcBZyMEHCIiBsNgBFy9eu1kypS/MEgScDZCwCEiYjAMRsAp1DgG13CFgLsoAYeI6F6DFXAAwYKAuygBh4joXgk4cBsE3EUJOERE90rAgdsg4C7auHFj0xgiIrrDyMjjprGrkYADuyHgLpqQcFqeeqq9aRwREUPb6667zjR2tRJwYDcEnMG33x4mZcqUkeuvv16uueYa7a233ipNmzaTjz76WNasWWu6DSIipq+xsfGyceMmmTbtDxk5cpS0bdtWihcvITfccIPvb7Xy//7v/6RatWrSsWMneffd92T16vT5m03Agd0QcBao9t6dOhUtixYt9vxRaef7Q5IhQwb9x+Xmm2+WYcPelaioGNNtERHdpvp7+NNPE6VDh45yzz33yI033mgKLeVDDz0kgwe/KUuXLpfIyBMSHR2r/54a1+dECTiwGwLOJhcsWCQjRoyUli0fk9tvv933By1XrtvlscdayfDhH8qKFStNt0NETC+PHTsu8+YtkNGjP5MePXpKlSpV5f77H9D/jBrDq02btjJ06Ns61DZv3iKJiWdM63OzBBzYDQEXIs6bN1+eeaazPPDAA5I1a1bfH9Ls2bNL587P6vn79x8Iuz+iiJh0FOC//w7Ipk1b5O+/50r37j2kSJEipj1eWbJk0XvE8ucvIE880UY+//wLHW3G9eGVJeDAbgg4lxsVFa3PARk16lNp0aJlssMY9957n1SuXEU++miEbN++03RbRLTeHTt26b1Wffv2k7p163piKr/kzJkzWWhde+21UqJECenf/xX5+efJsnDhYv0PmnFdaJ8EHNgNAYcm//hjunTp0lXKli2rTwj2PqmoPX+9e/eRadN+1//ph8q5KohWmHQS/WaZPXuOfPXV19KqVWt56KGHk4VXpkyZPP8Y3SsVKlTUe7jUqRALFiw0rQtDXwIO7IaAwzSrAu7EiVP68G3r1o8neyLLnDmzfvFG167dZN26DabbOslihWu5ysL5q5u2EZOcNetvadfuScmVK5f+h8T/1eZe1WHGJk2ayKefjpajRyP1CflxcQmmdWF4S8CB3RBwGDTVq3DVCdLq7VgqVaqsDxN5nzTvuusuqVevvowa9YkcOHDIdNv01G0sXrRCh4dxO0PV+PhEWbFilYwdO066deuuDzvmy5fPFF433XST3musXvk4evTnMmPGTPn33+2m9SFaIQEHdkPAYUipDt/Wr19fv3hD7eXzPnmrGHzzzSFy8OBhvcfkSod316//315Bt2FHwKk9VCdPRumvO3HiJGnQoIF+81T/wMqYMaPeu6X2zDZr1lyfQD937nzTuhBDQQIO7IaAQ1eqzlf6558l8sUXX0rDho2ShcQtt9zim6pl3UZaAk59v+bPXyjDh3/gia+GUrJkSbnnnntNe7nKl68gvXr1lgkTvpclS5bJrl179B4y4/oQ3S4BB3ZDwGFYqvbYeS87hXeGfWIcShMq4PyjS72Hl3r7mTJlykqjRo30nsqlS5eZvieImHoJOLAbAg7DXiPPde4nzz3TTxLiE/T1mJhYOX/+vJQsVkfeGDg82bIXzl/Q03PnzunpyI+/lnJlGkqfXgMl4pFKUqfmE3pek0ZPywfvfy7R0TFy5swZ6dC+j/w86XfPepNur1izaoOe7tm9X08TE0/75ilKFa+rp2O++F5q1WjtG/d+bS9p2QOHiIFJwIHdEHAY9hpRAadQAXfhwgVJTEiU3bv36YDbsX23b7lZMxf4Lg94ZZhs3rRNBvQfJiWK1vYF3NIlq2TmjPlS4dHGUr5sIx1wip49XtUB5x9f3oBTt0mJQvmr6unQIR/rIPQGngpMfwg4xPSXgAO7IeAw7E0rLZo98//t1rEJxDAQRNG+XYFbcHwlqoE7Xehswctg6X14ibINBHN/KjUHXEcGHPQz4JTOgGN7q2XAQT8DTukMOLa3WgYc9DPglM6AY3urZcBBPwNO6Qw4tnddn6Ucx2nAQTMDTukMOPiZg2c19xuB5xhwSmfAAUCRAad0BhwAFBlwSmfAAUCRAad0BhwAFBlwSmfAAUCRAad00QE3G2P8PwIAvIkBp2TxASdJkqRaBpwkSdLL+gKQwrOJn7UhUgAAAABJRU5ErkJggg==>