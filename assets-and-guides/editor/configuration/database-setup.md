# Database Setup

PC-Gun\_Crafting utilizes a database to store persistent data about:

* **Weapon Damage:** Tracks the health of individual weapon parts over time.
* **Crafting Experience:** Stores player experience and crafting history.

**1. Database Table Creation (MySQL)**

Execute the following SQL queries on your database to create the necessary tables:

```
SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;


CREATE TABLE `crafting_experience` (
  `Member` varchar(255) NOT NULL,
  `History` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL CHECK (json_valid(`History`)),
  `ExperienceGained` int(11) DEFAULT NULL,
  `HistoryRepair` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL,
  `QueueData` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT NULL CHECK (json_valid(`QueueData`)),
  `TableInventory` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin DEFAULT '[]' CHECK (json_valid(`TableInventory`))
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

CREATE TABLE `ui_styles` (
  `id` int(11) NOT NULL,
  `styles` longtext NOT NULL,
  `updated_at` timestamp NOT NULL DEFAULT current_timestamp() ON UPDATE current_timestamp()
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;

CREATE TABLE `weapon_damage_records` (
  `serial_number` varchar(255) NOT NULL,
  `weapon_name` varchar(255) NOT NULL,
  `last_owner` varchar(255) DEFAULT NULL,
  `parts_damage` longtext CHARACTER SET utf8mb4 COLLATE utf8mb4_bin NOT NULL CHECK (json_valid(`parts_damage`))
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_general_ci;


ALTER TABLE `crafting_experience`
  ADD UNIQUE KEY `Member` (`Member`);

ALTER TABLE `ui_styles`
  ADD PRIMARY KEY (`id`);

ALTER TABLE `weapon_damage_records`
  ADD PRIMARY KEY (`serial_number`);


ALTER TABLE `ui_styles`
  ADD PRIMARY KEY (`id`),
  MODIFY `id` int(11) NOT NULL AUTO_INCREMENT;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;

```

<details>

<summary><strong>Database Errors</strong></summary>

Double-check your database connection details in your server configuration files.

</details>
