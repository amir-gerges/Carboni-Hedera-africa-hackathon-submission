## **Draft v4 \- Proposal**

**Original Doc (V3):**

[https://docs.google.com/document/d/1phnD\_sn4b6xYuwgcP5pgBqM3XvaKOJ\_TgUbC0A62pF0/edit?pli=1\&tab=t.0\#heading=h.hibpjxblxq2r](https://docs.google.com/document/d/1phnD_sn4b6xYuwgcP5pgBqM3XvaKOJ_TgUbC0A62pF0/edit?pli=1&tab=t.0#heading=h.hibpjxblxq2r)

##  **1\. White Paper**

*(All text remains valid)*

## **2\. Project Summary (Updated)**

The Carboni platform is a DLT-based ecosystem built on top of the **Hedera Guardian** framework. It orchestrates the complete lifecycle of renewable energy certification, storage verification, and offsetting.

### **Entity-Based Architecture**

* **Entities**: Individuals or organizations verified through KYC/KYB, representing the root participants of the system.  
* **Facilities**: Physical sites owned by Entities that can host one or more energy Devices.  
* **Devices**: Installed and approved by certified Installers; can be Producer meters, Consumer meters, or Storage meters.

### **Approval and Validation Layers**

* **Carboni**: Approves Entities and oversees the overall policy and governance logic.  
* **EgyptERA**: Approves Facilities and Devices, ensuring compliance with national standards.  
* **Installers**: ERA-certified professionals who install and register devices.  
* **Operators**: Assigned to each Device; they collect and sign meter readings and send them to Guardian.

### **Lifecycle Summary**

1. **Entity Onboarding:** Entity undergoes KYC/KYB and receives a Guardian-issued VC.  
2. **Facility Registration:** Approved jointly by Carboni and EgyptERA.  
3. **Device Registration:** Installer adds the device under a Facility; approval by Carboni \+ ERA.  
4. **Data Validation:** Operator sends signed Data VC (production, consumption, or charging) to Guardian.  
5. **NFT Minting:** Guardian mints Anchor NFT \+ fNFTs for verified production or discharge.  
6. **Marketplace:** fNFTs traded and retired via offset claims.  
7. **Offset Proof:** Guardian issues Verifiable Credentials for Offset or Storage Coloring, ensuring traceable, auditable energy use.

---

## **3\. Roles (Updated)**

### **Entity**

* Represents any legal participant (individual or business) verified via KYC/KYB.  
* Can own one or more Facilities.  
* Can act as a Producer, Consumer, or Storage Provider depending on Device configuration.

### **Facility**

* Represents the physical site where Devices are installed.  
* Registered by an Entity and approved by both Carboni and EgyptERA.  
* May include multiple Devices of various types (Production, Consumption, Storage).

### **Device**

* Registered by Carboni.  
* Installed by a certified Installer.  
* Linked to a Facility and Entity.  
* Type determines data and tokenization behavior:  
  * **Producer Device:** Generates renewable energy → results in Anchor NFT \+ fNFTs.  
  * **Consumer Device:** Records consumption → issues Consumption VC.  
  * **Storage Device:** Records charging/discharging cycles → issues Charging/Storage/Discharge VCs.

### **Installer**

* Certified by EgyptERA.  
* Responsible for device installation, including setting the device type.  
* Device installation require signatures from Installer, Entity, and approval by Carboni \+ ERA.

### **Operator (service role)**

* Linked to Devices at registration.  
* Collects readings, signs them, and submits **Data VCs** to Guardian.  
* Guardian verifies Operator signatures, stores VC hashes on HCS for immutability.

### **Government Representatives**

**EgyptERA** – Approves Facility/Device registration, unfreezes Producer fNFTs, sets emission factors and floor price.  
**FRA** – Licenses brokers, audits financial trades, maintains NFT collateral registry.  
**Tax Authority** – Manages transaction tax collection rules.

### **Finance**

* Provides loans to Entities owning Producer or Storage Devices.  
* Loans can be secured against future NFT revenues or verified production capacity.

---

## **4\. High-Level Design (Unchanged)**

*(All examples and logic remain valid with minor terminology updates.)*

---

## **5\. Use Cases (Unchanged)**

*(All examples and logic remain valid with minor terminology updates.)*

---

## **6\. Guardian-Specific Design**

### **6.1 Policy Blocks (Updated)**

#### **1\. Entity Onboarding (KYC / KYB Block)**

* Any **Entity** undergoes KYC/KYB verification by Carboni.  
* Approved Entities receive a Guardian-issued Entity VC.  
* Entity VC links to all subsequent Facilities, Devices, NFTs, and Offset VCs.

#### **2\. Facility Registration Block**

* Verified Entities register Facilities (production, consumption, or storage sites).  
* Approved jointly by Carboni \+ EgyptERA.  
* Facility VC includes location, ownership, and permitted Device types.

#### **3\. Device Registration Block**

* Carboni registers the devices on the platform.  
* Installer installs one of his assigned devices under approved Facilities.  
* Signed by Installer and Entity; approved by Carboni \+ ERA.  
* Device type determines policy logic (Producer / Consumer / Storage).

#### **4\. Operator Data Validation Block (Corrected)**

* Each Device is linked to an Operator account.  
* Operator collects and signs hourly readings  
* Guardian verifies signature and schema   
* Guardian uses the validated data to mint for producers or issue consumption VC for consumers.

#### **5\. NFT Minting Block**

* Guardian mints **Anchor NFT** (frozen) and fractionalizes it into fNFTs.  
* ERA approves and unfreezes NFTs for market activity.

#### **6\. Offset Verification Block**

* Guardian retires fNFTs matched against Consumption VCs.  
* Issues **Offset VC** referencing the relevant NFTs, Device IDs, and data hashes.

## **Rest of the doc (WIP)**

*(WIP: To Be Reviewed)*

