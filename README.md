# Puffio

A vape device with user-configurable consumption limits and control, along with a system of cryptocurrency token rewards for adhering to these set limits. The goal is to allow users to manage their dependency while engaging them in blockchain activities, showcasing the potential use cases to the recent influx of new users.

How it works: the vape can be used as a regular vape device, but it will be actively promoted alongside a Web3 application, where users can set a constant consumption limit or enable a mode for gradually reducing their intake. A user who purchases the vape and installs the application can receive rewards in the form of cryptocurrency tokens or NFTs, which are deposited into their wallet for further activities. They will continue to earn these rewards periodically, as long as they maintain an active smoking limit. Additionally, non-smokers can participate in the app’s activities without purchasing the vape, using “virtual smoking” instead of real smoking.

![raw2puffio](https://github.com/user-attachments/assets/91f43882-8ce6-4fe4-8cd1-c792ce91e353)

# Entities:
# Database Schema Entity Attribute Descriptions

## 1. User
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **UserId**        | `BIGSERIAL`    | Primary Key – Unique identifier for the user.          |
| **Name**          | `VARCHAR(32)`  | User's name.                                           |
| **Email**         | `VARCHAR(256)` | User's email address.                                  |
| **RegistrationDate** | `TIMESTAMP` | Date and time when the user registered.                |
| **WalletAddress** | `VARCHAR(48)`  | User's cryptocurrency wallet address.                  |
| **LastLogin**     | `TIMESTAMP`    | Date and time of the user's last login.                |

## 2. Role
| Attribute        | Type           | Description                                            |
|------------------|----------------|--------------------------------------------------------|
| **RoleId**       | `SERIAL`       | Primary Key – Unique identifier for the role.          |
| **UserId**       | `BIGINT`       | Foreign Key – Links the role to a specific user.        |
| **RoleName**     | `VARCHAR(32)`  | Name of the role (e.g., admin, user).                  |
| **Description**  | `TEXT`         | Description of the role.                               |

## 3. VapeSession
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **VapeSessionId** | `BIGSERIAL`    | Primary Key – Unique identifier for the vaping session.|
| **UserId**        | `BIGINT`       | Foreign Key – Links the session to a specific user.    |
| **DeviceId**      | `BIGINT`       | Foreign Key – Links the session to a specific device.  |
| **Timestamp**     | `TIMESTAMP`    | Time when the session took place.                      |
| **NicotineConsumed** | `INT`       | Amount of nicotine consumed during the session.        |

## 4. Device
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **DeviceId**      | `BIGSERIAL`    | Primary Key – Unique identifier for the device.        |
| **UserId**        | `BIGINT`       | Foreign Key – Links the device to a specific user.     |
| **SerialNumber**  | `VARCHAR(48)`  | Serial number of the device.                           |
| **LastActive**    | `TIMESTAMP`    | Last time the device was active.                       |

## 5. NFT
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **NFTId**         | `BIGSERIAL`    | Primary Key – Unique identifier for the NFT.           |
| **DeviceId**      | `BIGINT`       | Foreign Key – Links the NFT to a specific device.      |
| **TokenContract** | `VARCHAR(48)`  | Smart contract associated with the NFT.                |
| **MetadataURL**   | `TEXT`         | URL pointing to the metadata for the NFT.              |
| **Name**          | `VARCHAR(64)`  | Name of the NFT.                                       |

## 6. Event
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **EventId**       | `SERIAL`       | Primary Key – Unique identifier for the event.         |
| **Name**          | `VARCHAR(128)` | Name of the event.                                     |
| **Description**   | `TEXT`         | Description of the event.                              |
| **StartDate**     | `TIMESTAMP`    | Date and time the event starts.                        |
| **EndDate**       | `TIMESTAMP`    | Date and time the event ends.                          |
| **Status**        | `VARCHAR(32)`  | Current status of the event (e.g., active, completed). |

## 7. Reward
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **RewardId**      | `SERIAL`       | Primary Key – Unique identifier for the reward.        |
| **UserId**        | `BIGINT`       | Foreign Key – Links the reward to a specific user.     |
| **EventId**       | `INT`          | Foreign Key – Links the reward to a specific event.    |
| **Amount**        | `BIGINT`       | Amount of the reward.                                  |
| **IssuedAt**      | `TIMESTAMP`    | Time when the reward was issued.                       |
| **TokenContract** | `VARCHAR(48)`  | Smart contract associated with the reward.             |

## 8. ActivityLog
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **ActivityLogId** | `BIGSERIAL`    | Primary Key – Unique identifier for the activity log.  |
| **UserId**        | `BIGINT`       | Foreign Key – Links the activity log to a specific user.|
| **ActionType**    | `VARCHAR(64)`  | Type of action logged.                                 |
| **Timestamp**     | `TIMESTAMP`    | Time when the action occurred.                         |
| **Description**   | `TEXT`         | Additional details about the action.                   |

## 9. Limit
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **LimitId**       | `BIGSERIAL`    | Primary Key – Unique identifier for the limit.         |
| **UserId**        | `BIGINT`       | Foreign Key – Links the limit to a specific user.      |
| **LimitName**     | `VARCHAR(64)`  | Name of the limit (e.g., daily nicotine cap).          |
| **Description**   | `TEXT`         | Description of the limit.                              |

## 10. Verification
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **VerificationId** | `SERIAL`      | Primary Key – Unique identifier for the verification.  |
| **UserId**        | `BIGINT`       | Foreign Key – Links the verification to a specific user.|
| **Token**         | `TEXT`         | Verification token.                                    |
| **IsCompleted**   | `BOOL`         | Whether the verification is completed or not.          |
| **ExpiresAt**     | `TIMESTAMP`    | Time when the verification expires.                    |

## 11. Transaction
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **TransactionId** | `BIGSERIAL`    | Primary Key – Unique identifier for the transaction.   |
| **UserId**        | `BIGINT`       | Foreign Key – Links the transaction to a specific user.|
| **Amount**        | `MONEY`        | Amount involved in the transaction.                    |
| **TransactionDate** | `TIMESTAMP`  | Date and time of the transaction.                      |
| **TransactionHash** | `VARCHAR(66)` | Hash of the transaction for blockchain verification.   |
| **TokenContract** | `VARCHAR(48)`  | Smart contract associated with the transaction.        |

## 12. Notification
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **NotificationId** | `BIGSERIAL`   | Primary Key – Unique identifier for the notification.  |
| **UserId**        | `BIGINT`       | Foreign Key – Links the notification to a specific user.|
| **NotificationObjectId** | `BIGINT` | Foreign Key – Links to the object that triggered the notification. |
| **Status**        | `SMALLINT`     | Status of the notification (e.g., read, unread).       |

## 13. NotificationObject
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **NotificationObjectId** | `BIGSERIAL` | Primary Key – Unique identifier for the notification object. |
| **EntityTypeId**  | `INT`          | Foreign Key – Links the notification object to a specific entity type. |
| **EntityId**      | `INT`          | ID of the entity associated with the notification.     |
| **CreatedOn**     | `TIMESTAMP`    | Time when the notification object was created.         |

## 14. EntityType
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **EntityTypeId**  | `SERIAL`       | Primary Key – Unique identifier for the entity type.   |
| **Entity**        | `VARCHAR(128)` | Name of the entity (e.g., reward, event).              |
| **Template**      | `VARCHAR(256)` | Template for displaying the entity information.        |

## 15. Achievement
| Attribute         | Type           | Description                                            |
|-------------------|----------------|--------------------------------------------------------|
| **AchievementId** | `SERIAL`       | Primary Key – Unique identifier for the achievement.   |
| **UserId**        | `BIGINT`       | Foreign Key – Links the achievement to a specific user.|
| **Name**          | `VARCHAR(32)`  | Name of the achievement.                               |
| **Description**   | `TEXT`         | Description of the achievement.                        |
| **Timestamp**     | `TIMESTAMP`    | Time when the achievement was awarded.                 |

# User functionality:
### Basic user:
* Can register and log in
* Can edit personal information
* Can connect new device
* Can buy NFT
### Advanced user:
* Can participate in events
* Can set device vaping limits
* Can earn rewards daily for set limits
