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
VALUES(101,'Placement Drive',' Drive starts tomorrow','Placement',false);
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




# Stage 3

## Query Analysis

### Query

```sql
SELECT *
FROM notifications
WHERE studentId = 1042
AND isRead = false
ORDER BY createdAt ASC;
```

### Is this query efficient?

The query is correct, but it may become slow when the table contains a large amount of data.

### Why?

- It scans many records.
- Sorting by createdAt takes more time.
- Performance decreases as data grows.

### Index Recommendation

Create a composite index on:

- studentId
- isRead
- createdAt

### Should every column be indexed?

No.



### Placement Notifications in the Last 7 Days

```sql
SELECT *
FROM notifications
WHERE notificationType = 'Placement'
AND createdAt >= NOW() - INTERVAL 7 DAY;
```



# Stage 4

## Performance and Scaling

### Reducing Database Load

- Use pagination.
- Cache frequently accessed notifications.
- Load only required data.
- Use WebSocket for real-time updates.

### Caching Strategy

Store recently accessed notifications in cache so repeated requests do not always query the database.

### Pagination

Display notifications page by page instead of loading all notifications at once.

Example:

Page 1 → Notifications 1–10

Page 2 → Notifications 11–20

### Trade-offs


- Pagination reduces database load but users see limited records per page.
- Caching improves response time but cached data should be updated regularly.
- WebSocket provides instant updates but requires maintaining active connections.




