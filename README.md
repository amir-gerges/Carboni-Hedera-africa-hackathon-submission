# Carboni — Hedera Africa Hackathon Submission

This repository contains the submission assets for the Carboni project.

- [Whitepaper(s)](project-whitepapers/)
- [Slide deck](Carboni-Hedera-Africa-Hackathon-Pitch-Deck.pdf)
- [Policy artifacts](carboni-policy/)
- [Schema artifacts](schema/)
- [Hashgraph Certificate](Certificates/)

## 1. Project Overview

- **Project name**: Carboni — Renewable Energy NFT Offset Platform
- **Summary**: Tokenize renewable energy and retire fractional NFTs to offset hourly consumption with verifiable, tamper‑proof data on Hedera.
- **Vision**: End‑to‑end transparency from meter to retirement using Guardian VCs, HCS logging, and HTS tokens.
- **Track**: Track II: DLT For Operations.

### Problem Statement

Lack of real-time, transparent, and verifiable systems for renewable energy offsets in Africa.

### Solution Overview

Carboni leverages Hedera Guardian to tokenize renewable energy hourly generation into verifiable NFTs (anchor NFTs and fNFTs), enabling real-time, auditable carbon offsets.

### Key Innovations

- **Integration of Advanced Technologies:** Use of smart meters for precise tracking and verification of energy generation, consumption, and offsets.
- **Transparent and Secure Data Management:** Data captured is securely stored on the Hedera DLT, ensuring transparency and immutability, leveraging the Guardian Managed Service.
- **Tokenization of Renewable Energy Certification and offsetting:** Minting of REN tokens to encapsulate the value of renewable energy generated, providing tangible rewards and incentivizing further participation in green energy generation.

## 2. Architecture & Hedera Usage

- **Guardian** for Verifiable Credential management and multi-role governance.
- **Hedera Consensus Service (HCS)** for immutable ledger of entities, facilities, devices, meter data for both generation and consumption, offsets (audit trail). HCS predictable fee guarantees operational cost stability, which is essential for low margin logistics in Africa.
- **Hedera Token Service (HTS)** for producer NFTs and fractional fungible tokens (fNFTs) used in offsetting. HTS built-in compliance controls, and its automatic royalties and revenue sharing are critical for our business model.

## 3. Technology Readiness Level and Evidence

TRL: Prototype (Working Guardian policy)

### Hedera Testnet transactions

There was many transactions sent to the testnet on the Policy development topic.

Here is a link to HCS topic messages:

- <https://hashscan.io/testnet/topic/0.0.7101537/messages>

One of the transactions:

- link: <https://hashscan.io/testnet/transaction/1761054738.041053463>
- type: SUBMIT MESSAGE

## 4. Deployment & Setup Instructions

- Sign Up for Tenant Admin Account on [MGS](https://guardianservice.app/)
- Click on “Sign Up” and enter your username, email, password, and agree to the terms of use.
- Sign in for  admin login and Tenant Configuration.
- Select IPFS Storage Provider.
- Invite Users and Customizing Tenant Branding.
- Set Up Policy User Account
- Login in as user (Invited through Admin)
- Set Up a Standard Registry User Account.
- Import Carboni policy

## 5. Architecture Diagram

```
                      ┌──────────────────────────────────────┐
                      │         Hedera Network               │
                      │--------------------------------------│
                      │  • Hedera Consensus Service (HCS)    │
                      │  • Hedera Token Service (HTS)        │
                      │  • DID / VC Anchoring (Guardian)     │
                      └──────────────────────────────────────┘
                                      ▲
                                      │   (Hashes of VCs, Minting, NFT/FT txs)
                                      │
                                      │
┌───────────────────────────────────────────────────────────────────────────────┐
│                          Carboni Guardian Policy Engine                        │
│───────────────────────────────────────────────────────────────────────────────│
│   Roles / Users:                                                               │
│   ┌────────────┐   ┌─────────────┐   ┌─────────────┐   ┌────────────┐          │
│   │ EgyptERA   │   │ CarboniAdmin│   │ Installer   │   │ Entity     │          │
│   │ (Regulator)│   │ (Platform)  │   │ (Devices)   │   │ (Producer, │          │
│   │             │   │             │   │             │   │ Consumer)  │          │
│   └────────────┘   └─────────────┘   └─────────────┘   └────────────┘          │
│          ▲                ▲                     ▲               ▲              │
│          │                │                     │               │              │
│          │                │                     │               │              │
│          │                │                     │               │              │
│   ┌───────────────┐  ┌───────────────┐   ┌──────────────┐   ┌────────────────┐ │
│   │ Approve       │  │ Approve       │   │ Register     │   │ Register       │ │
│   │ Installer,    │  │ Installer,    │   │ Device        │   │ Facility       │ │
│   │ Facility,     │  │ Facility,     │   │ (Producer,    │   │ Assign Installer│ │
│   │ Device        │  │ Device        │   │ Consumer, Bat.)│  │                │ │
│   └───────────────┘  └───────────────┘   └──────────────┘   └────────────────┘ │
│          │                │                     │               │              │
│          └────────────────┴─────────────────────┴───────────────┘              │
│                              │                                                │
│                              ▼                                                │
│             ┌────────────────────────────────────────────────┐                │
│             │   Operator Backend (IoT Gateway / MRV Engine)   │                │
│             │────────────────────────────────────────────────│                │
│             │  Collects minute-level meter data               │                │
│             │  → aggregates hourly totals                     │                │
│             │  → signs & issues DataVCs (Production,          │                │
│             │     Consumption, Charging, Discharge)           │                │
│             │  → submits VCs to Guardian via REST API         │                │
│             └────────────────────────────────────────────────┘                │
│                              │                                                │
│                              ▼                                                │
│             ┌────────────────────────────────────────────────┐                │
│             │  Guardian Policy Flow                          │                │
│             │────────────────────────────────────────────────│                │
│             │  1️⃣ Validate VCs (Operator → Device → Facility)│                │
│             │  2️⃣ Mint Anchor NFT + fNFTs (via HTS)         │                │
│             │  3️⃣ Log hash of VC to HCS                     │                │
│             │  4️⃣ Await ERA/Carboni approvals (Unfreeze)    │                │
│             │  5️⃣ Enable marketplace trading / offsets       │                │
│             │  6️⃣ Burn fNFTs → Issue OffsetVC (CO2 proof)   │                │
│             └────────────────────────────────────────────────┘                │
│                              │                                                │
│                              ▼                                                │
│            ┌──────────────────────────────────────────────────┐               │
│            │ Decentralized Marketplace                         │               │
│            │──────────────────────────────────────────────────│               │
│            │ • Trades fNFTs (HTS Fungible Tokens)              │               │
│            │ • Uses CEGP token for settlement                  │               │
│            │ • Enforces FloorPriceVC                           │               │
│            │ • Burned fNFTs trigger OffsetVC issuance          │               │
│            └──────────────────────────────────────────────────┘               │
│                                                                               │
│   ┌──────────────────────────────┐   ┌─────────────────────────────────────┐   │
│   │ EmissionFactorVC             │   │ FloorPriceVC                        │   │
│   │ (issued by Govt / Carboni)   │   │ (issued by ERA / FRA)               │   │
│   │ Used in offset calculation   │   │ Used in minting & trading pricing   │   │
│   └──────────────────────────────┘   └─────────────────────────────────────┘   │
└───────────────────────────────────────────────────────────────────────────────┘
```

## 6. Deployed Hedera ID

- Hedera Testnet account ID used for the Guardian instance: 0.0.6884660

## 7. Deployed instance

- Deployed instance: `http://185.206.122.21:3000/`. Credentials will be provided in DoraHacks submission form.

## 8. Guardian Policy Walkthrough

### Policy import

Use Guardian UI to import `Carboni POC v1 - Renewable Energy Certificates_1761054778465.policy`.

### Policy Design

1. Entity Onboarding (KYC / KYB Block)

   - Any Entity undergoes KYC/KYB verification by Carboni.
   - Approved Entities receive a Guardian-issued Entity VC.
   - Entity VC links to all subsequent Facilities, Devices, NFTs, and Offset VCs.

2. Facility Registration Block

   - Verified Entities register Facilities (production, consumption, or storage sites).
   - Approved jointly by Carboni + EgyptERA.
   - Facility VC includes location, ownership, and permitted Device types.

3. Device Registration Block

   - Carboni registers the devices on the platform.
   - Installer installs one of his assigned devices under approved Facilities.
   - Signed by Installer and Entity; approved by Carboni + ERA.
   - Device type determines policy logic (Producer / Consumer / Storage).

4. Operator Data Validation Block (Corrected)

   - Each Device is linked to an Operator account.
   - Operator collects and signs hourly readings
   - Guardian verifies signature and schema
   - Guardian uses the validated data to mint for producers or issue consumption VC for consumers.

5. NFT Minting Block

   - Guardian mints Anchor NFT (frozen) and fractionalizes it into fNFTs.
   - ERA approves and unfreezes NFTs for market activity.

6. Offset Verification Block

   - Guardian retires fNFTs matched against Consumption VCs.
   - Issues Offset VC referencing the relevant NFTs, Device IDs, and data hashes.

### Step-by-Step Execution Guide

#### 1) Import the Policy

1. You can view the policy by clicking on the policy configuration button.
2. Click “Dry Run” to start running the policy in demo mode.

#### 2) Create the Initial Users

We’ll create the roles needed for the onboarding flow.

1. In the Guardian **Users panel**, click **“Create User”**.
2. Choose **role = EgyptERA (Regulator)**.

   - This account will later review and approve Installers, Facilities, and Devices.
3. Repeat to **create another user**, choose **role = Carboni Administrator**.

   - This account acts as the platform operator (approving Installers, Entities, Facilities).
4. Create another user and choose **role = Installer**.

   - This user represents an ERA-approved technician.
5. Create another user and choose **role = Entity**.

   - This account represents a business or person who owns renewable assets or consumption points.

#### 3) Complete KYC for Installer and Entity

1. Switch to the **Installer** user using the **user switcher** in the Guardian interface.
2. Open **“Profile / KYC”**, fill out required information, and click **Submit**.
3. Switch to the **Entity** user and do the same — complete and submit KYC.

#### 4) Approve Users

1. Switch to **EgyptERA** user.

   - Navigate to **“Installer Approvals”** and review the Installer’s KYC document.
   - Click **Approve**.
2. Switch to **Carboni Administrator**.

   - In **Installer Approvals**, approve the Installer again.
   - In **Entity Approvals**, review and approve the Entity’s KYC submission.

Once both approvals are done, the Installer and Entity can now access their dashboards.

#### 5) Facility Registration

1. Switch to **Entity** user.
2. Go to **“Facilities” → “Register Facility”**.
3. Fill in the facility form (name, location, type, etc.) and click **Submit**.
4. Switch to **EgyptERA** user → open **Facility Approvals** → review → **Approve**.
5. Switch to **Carboni Administrator** user → open **Facility Approvals** → **Approve**.

The facility is now active and ready for device installation.

#### 6) Assign Installer to Facility

1. Stay logged in as **Entity** user.
2. In the **Facilities** table, open the **Actions dropdown** beside your facility.
3. Click **“Assign Installer”** and choose from the list of approved Installers.

#### 7) Installer Registers Device

1. Switch to **Installer** user.
2. Open **“Assignments”** tab — your assigned facility should now appear.
3. Click on the facility → **“Add Device”**.
4. Fill in device details (Device ID, type: Producer / Consumer / Storage).
5. Submit the device registration request.
6. Switch to **EgyptERA** user → go to **Device Approvals** → review and **Approve**.
7. Switch to **Carboni Administrator** user → **Approve** again.

The device is now officially registered and linked to the facility.

#### 8) Operator Data Flow *(Work-in-Progress — future release)*

1. The **Operator backend** collects minute-level meter readings and aggregates them hourly.
2. It sends a signed **Data VC** (e.g., Production, Consumption, Charging) to Guardian via API.
3. Guardian validates the VC and:

   - If **Producer**, triggers the **minting path** to issue Anchor NFT + fNFTs.
   - If **Consumer**, issues **Consumption VC** instead.

#### 9) Regulatory Actions *(Future steps — not in current policy)*

1. **ERA** unfreezes NFTs for market trading.
2. **Carboni** fractionalizes Anchor NFTs into fNFTs.
3. **Carboni** retires fNFTs when matched against Consumption VCs.
4. **Carboni** issues an **Offset VC** referencing:

   - Related NFTs
   - Device IDs
   - Data hashes (stored on Hedera HCS)

**End of current working flow.**
This completes the registration and approval process up to device onboarding in the Carboni Guardian ecosystem.

Note : the policy is WIP (steps 10 to 14 are not included in currenrt policy)

## 9. Demonstration Video

- The Playlist link: <https://www.youtube.com/playlist?list=PLvPZDyb0GQLXRUxoqreDmt1a1LRF1qOF4>. includes:

  - An overview of Carboni tokenized REC platform: <https://youtu.be/-wjeaZsbg_I?si=KdItojyQFgJA8Nqe>
  - Demonstration Video link: <https://youtu.be/-wjeaZsbg_I?si=KdItojyQFgJA8Nqe>

## 10. Pitch Deck

- [see here](Carboni-Hedera-Africa-Hackathon-Pitch-Deck.pdf)

## 11. Demo Credentials

- Deployed instance: `http://185.206.122.21:3000/`. Credentials will be provided in DoraHacks submission form.

## 12. License

Apache‑2.0
