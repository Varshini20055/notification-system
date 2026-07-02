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

