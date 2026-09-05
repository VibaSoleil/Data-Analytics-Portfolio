# n8n MySQL Connection

## 1. Purpose

This document describes the MySQL connection configuration used by n8n within the Docker environment for this project.

The configuration enables n8n workflows to communicate with and process data stored in the MySQL database.

---

## 2. Docker Environment

### n8n Container

* Container: `n8n`
* Image: `docker.n8n.io/n8nio/n8n:latest`
* Port: `5678`
* URL: `http://localhost:5678`

### MySQL Container

* Container: `mysql-server`
* Image: `mysql:8.4`
* Port: `3306`

---

## 3. Docker Network

The n8n and MySQL containers are connected through the following Docker network:

* Network: `n8n-network`
* Driver: `bridge`
* Network Subnet: `172.18.0.0/16`
* Gateway: `172.18.0.1`

The shared Docker network enables n8n to communicate with the MySQL container using the container hostname `mysql-server`.

---

## 4. Connection from n8n to MySQL

The n8n container connects to MySQL using the MySQL container hostname rather than `localhost`.

### Connection Parameters

| Parameter | Value                                  |
| --------- | -------------------------------------- |
| Host      | `mysql-server`                         |
| Port      | `3306`                                 |
| Database  | `mydb`                                 |
| Username  | `user`                                 |
| Password  | `<REDACTED — NOT THE ACTUAL PASSWORD>` |

The hostname `mysql-server` is resolvable within the `n8n-network` Docker network.

`localhost` is not used as the MySQL host from inside the n8n container because n8n and MySQL run as separate Docker containers.

---

## 5. MySQL Environment Configuration

The following MySQL environment variables were verified from the running `mysql-server` container:

| Variable              | Value                                       |
| --------------------- | ------------------------------------------- |
| `MYSQL_DATABASE`      | `mydb`                                      |
| `MYSQL_USER`          | `user`                                      |
| `MYSQL_PASSWORD`      | `<REDACTED — NOT THE ACTUAL PASSWORD>`      |
| `MYSQL_ROOT_PASSWORD` | `<REDACTED — NOT THE ACTUAL ROOT PASSWORD>` |
| `MYSQL_MAJOR`         | `8.4`                                       |
| `MYSQL_VERSION`       | `8.4.10-1.el9`                              |

Actual passwords are intentionally excluded from this documentation.

---

## 6. Connection Architecture

```text
┌─────────────────────────────┐
│        n8n Container        │
│                             │
│  Container: n8n             │
│  Port: 5678                 │
└──────────────┬──────────────┘
               │
               │ MySQL Connection
               │ Host: mysql-server
               │ Port: 3306
               │
               ▼
┌─────────────────────────────┐
│      MySQL Container        │
│                             │
│  Container: mysql-server    │
│  Image: mysql:8.4           │
│  Port: 3306                 │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│       MySQL Database        │
│                             │
│  Database: mydb             │
└─────────────────────────────┘

Docker Network:
n8n-network
```

---

## 7. Verified Docker Network Configuration

The running Docker environment confirms that both containers are attached to `n8n-network`.

### n8n

* Network: `n8n-network`
* IP Address: `172.18.0.2`

### MySQL

* Network: `n8n-network`
* IP Address: `172.18.0.3`
* DNS Name: `mysql-server`

This confirms that the containers share the same Docker network and that `mysql-server` is the container hostname used for network communication.

---

## 8. Prerequisites

The following components must be available and running:

* Docker Desktop
* n8n container
* MySQL container
* Docker network: `n8n-network`
* MySQL database: `mydb`

The n8n and MySQL containers must be connected to the same Docker network for container-to-container communication.

---

## 9. Connection Verification

The Docker environment was verified using Docker CLI inspection commands.

The verification confirmed:

* The `n8n` container is running.
* The `mysql-server` container is running.
* n8n is exposed on port `5678`.
* MySQL is exposed on port `3306`.
* Both containers are connected to `n8n-network`.
* The MySQL database configuration specifies `mydb`.
* The MySQL application user is configured as `user`.
* The MySQL container hostname is `mysql-server`.

The database password is intentionally excluded from this documentation.

A successful n8n MySQL credential test should be used to verify application-level authentication after the correct credential is configured.

---

## 10. Operational Dependency

The n8n-to-MySQL connection depends on the following components and configuration:

```text
Docker Desktop
      ↓
Docker Network: n8n-network
      ↓
 ┌─────────────────┬────────────────────┐
 ↓                 ↓                    │
n8n Container      MySQL Container       │
 ↓                 ↓                    │
MySQL Credentials → mysql-server:3306    │
                    ↓
                Database: mydb
                    ↓
               n8n Workflow
```

If the connection fails, the following items should be checked:

1. Docker Desktop status.
2. n8n container status.
3. MySQL container status.
4. Docker network membership.
5. MySQL hostname (`mysql-server`).
6. MySQL port (`3306`).
7. Database name (`mydb`).
8. MySQL username.
9. Authentication credentials.

This dependency structure separates the Docker infrastructure, network connectivity, database configuration, and application-level authentication 
involved in the n8n-to-MySQL connection.


## 11. Security Note

Actual MySQL credentials are intentionally excluded from this documentation.

The following values are placeholders and are **not the actual passwords**:

* `MYSQL_PASSWORD`
* `MYSQL_ROOT_PASSWORD`
* MySQL connection password

For production environments:

* Use strong and unique passwords.
* Do not expose credentials in public documentation.
* Do not commit secrets to public repositories.
* Use environment variables or a secure secrets-management mechanism where appropriate.
* Rotate credentials if they are accidentally exposed.

---

## 12. Configuration Scope

This configuration applies specifically to the Docker-based n8n and MySQL environment used by this project.

Container names, network names, database names, ports, image versions, and other configuration values may differ in other environments.

Any deployment change should be reflected in the corresponding technical documentation.

---

## 13. Final Configuration Summary

| Component            | Verified Configuration           |
| -------------------- | -------------------------------- |
| n8n Container        | `n8n`                            |
| n8n Image            | `docker.n8n.io/n8nio/n8n:latest` |
| n8n Port             | `5678`                           |
| n8n URL              | `http://localhost:5678`          |
| MySQL Container      | `mysql-server`                   |
| MySQL Image          | `mysql:8.4`                      |
| MySQL Port           | `3306`                           |
| Database             | `mydb`                           |
| MySQL Username       | `user`                           |
| Docker Network       | `n8n-network`                    |
| Network Driver       | `bridge`                         |
| Connection Direction | n8n → MySQL                      |
| MySQL Password       | `<REDACTED>`                     |
| MySQL Root Password  | `<REDACTED>`                     |

---

## 14. Verification Status

**Docker Environment Verification: PASS**

The container, network, hostname, port, database configuration, and MySQL username documented above were verified against the running Docker environment.

Passwords are intentionally excluded for security reasons.

**Application-Level Credential Authentication: Requires valid credentials**

The previously tested example password was rejected by MySQL. Therefore, this documentation does not claim that the redacted password has been verified.

This distinction ensures that the documentation accurately represents the verified infrastructure configuration without making unsupported authentication claims.
