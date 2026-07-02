# Stage 1

## Notification System Design

### Features

- View notifications
- Create notifications
- Mark notification as read
- Delete notifications
- Receive real-time notifications

---

## 1. Get Notifications

**Method:** GET

**Endpoint:**
```
/notifications
```

**Headers:**
```
Content-Type: application/json
Authorization: Bearer Token
```

**Response**

```json
[
  {
    "id": 1,
    "title": "Placement Drive",
    "message": "Drive starts tomorrow",
    "type": "Placement",
    "isRead": false
  }
]
```

---

## 2. Create Notification

**Method:** POST

**Endpoint:**

/notifications


**Request**

```json
{
  "title": "Placement Drive",
  "message": "Drive starts tomorrow",
  "type": "Placement"
}


**Response**

```json
{
  "message": "Notification created successfully"
}




## 3. Mark as Read

**Method:** PUT

**Endpoint:**
```
/notifications/{id}/read
```

**Response**

```json
{
  "message": "Notification marked as read"
}
```

---

## 4. Delete Notification

**Method:** DELETE

**Endpoint:**
```
/notifications/{id}
```

**Response**

```json
{
  "message": "Notification deleted successfully"
}
```

---

## Notification Fields

- id
- title
- message
- type
- isRead

---

## Real-Time Notifications



# Stage 2

## Database Choice

I choose MySQL because it is reliable, easy to manage, and supports indexing and transactions.

## Notification Table

| Column | Type |
|---------|------|
| id | INT |
| studentId | INT |
| title | VARCHAR(100) |
| message | TEXT |
| notificationType | VARCHAR(30) |
| isRead | BOOLEAN |
| createdAt | TIMESTAMP |

## Challenges with Large Data

- Slow queries
- High database load
- More storage usage

## Solutions

- Create indexes on frequently used columns.
- Use pagination.
- Archive old notifications.
- Optimize SQL queries.

## SQL Queries

### Create Notification

```sql
INSERT INTO notifications(studentId,title,message,notificationType,isRead)
VALUES(101,'Placement Drive','TCS drive starts tomorrow','Placement',false);
```

### Get Notifications

```sql
SELECT * FROM notifications
WHERE studentId = 101
ORDER BY createdAt DESC;
```

### Mark as Read

```sql
UPDATE notifications
SET isRead = true
WHERE id = 1;
```

### Delete Notification

```sql
DELETE FROM notifications
WHERE id = 1;
```