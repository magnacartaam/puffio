# Puffio

A vape device with user-configurable consumption limits and control, along with a system of cryptocurrency token rewards for adhering to these set limits. The goal is to allow users to manage their dependency while engaging them in blockchain activities, showcasing the potential use cases to the recent influx of new users.

How it works: the vape can be used as a regular vape device, but it will be actively promoted alongside a Web3 application, where users can set a constant consumption limit or enable a mode for gradually reducing their intake. A user who purchases the vape and installs the application can receive rewards in the form of cryptocurrency tokens or NFTs, which are deposited into their wallet for further activities. They will continue to earn these rewards periodically, as long as they maintain an active smoking limit. Additionally, non-smokers can participate in the app’s activities without purchasing the vape, using “virtual smoking” instead of real smoking.

![puffio drawio-2](https://github.com/user-attachments/assets/ba7c5b16-1f9b-4ff6-9cfe-76a9310ac441)

## Entities:
### 1. User
* UserId: Primary Key
* Name: Unique username
* Email: User's email address
* Password: Password hash
* Role: User's role
* WalletAddress: Cryptocurrency wallet address
* RegistrationDate: Registration date
* LastLogin: Last login date
### 2. Device
* DeviceId: Primary Key
* SerialNumber: Device serial number
* UserId: Foreign Key to the user (relation with User)
* LastActive: Device status (active/inactive)
### 3. Transaction
* TransactionId: Primary Key
* UserId: Foreign Key to the user (relation with User)
* Amount: Amount of cryptocurrency
* TransactionDate: Transaction date
* AssetType: Asset type
### 4. VapeSession
* VapeSessionId: Primary Key
* UserId: Foreign Key to the user (relation with User)
* DeviceId: Foreign Key to the device (relation with Device)
* Timestamp: Timestamp
* NicotineConsumed: Abstract value of vape usage
### 5. Reward
* RewardId: Primary Key
* UserId: Foreign Key to the user (relation with User)
* Event: Event where reward was earned
* Amount: Number of tokens or other rewards
* IssuedAt: Reward issue date
* TokenContract: Contract of issued token
### 6. Limit
* id: Primary Key
* UserId: Foreign Key to the user (relation with User)
* device_id: Foreign Key to the device (relation with Device)
* daily_puff_limit: Daily puff limit
* decrease_rate: Rate of puff reduction (e.g., -2 puffs per week)
* active: Flag indicating if the limit is active
### 7. Achievement
* id: Primary Key
* name: Achievement name
* description: Achievement description
* earned_at: Achievement earned date
### 8. NFT
* id: Primary Key
* name: NFT name
* metadata_url: URL to NFT metadata
* created_at: Creation date
### 9. ActivityLog
* id: Primary Key
* UserId: Foreign Key to the user (relation with User)
* action: Action type (session creation, limit change, etc.)
* timestamp: Time of the action
* description: Action description
### 10. Event
* id: Primary Key
* name: Event name
* description: Event description
* start_date: Event start date
* end_date: Event end date
* reward: Reward for participation (tokens, NFTs, etc.)
* status: Event status (active/completed)
## User functionality:
### Basic user:
* Can register and log in
* Can edit personal information
* Can connect new device
* Can buy NFT
### Advanced user:
* Can participate in events
* Can set device vaping limits
* Can earn rewards daily for set limits
