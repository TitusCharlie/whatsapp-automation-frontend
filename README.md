WhatsApp Automation API Documentation

Overview

This API enables WhatsApp automation by handling contacts, messages, statuses, and group management. The backend integrates with the 360Dialog API for WhatsApp messaging.

Base API URL: http://127.0.0.1:8000/

1️⃣ Contacts API

Manages user contacts fetched from the WordPress landing page.

Action

Method

Endpoint

Functionality

Get all contacts

GET

/contacts/

Retrieve a list of all contacts.

Get a contact

GET

/contacts/{id}/

Retrieve a specific contact.

Create a contact

POST

/contacts/

Add a new contact.

Update a contact

PUT

/contacts/{id}/

Modify an existing contact.

Delete a contact

DELETE

/contacts/{id}/

Remove a contact.

Example: Fetch All Contacts

async function fetchContacts() {
    const response = await fetch("http://127.0.0.1:8000/contacts/");
    const data = await response.json();
    console.log(data);
}

2️⃣ WhatsApp Messages API

Handles the sending and scheduling of WhatsApp messages.

Action

Method

Endpoint

Functionality

Get all messages

GET

/whatsapp/

Retrieve all WhatsApp messages.

Get a message

GET

/whatsapp/{id}/

Retrieve a specific message.

Send a message

POST

/whatsapp/

Send or schedule a message.

Delete a message

DELETE

/whatsapp/{id}/

Remove a scheduled message.

Example: Send a WhatsApp Message

async function sendMessage() {
    const response = await fetch("http://127.0.0.1:8000/whatsapp/", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
            phone_number: "+1234567890",
            message: "Hello from API!",
            scheduled_at: "2025-02-20T10:00:00Z"
        })
    });
    const data = await response.json();
    console.log(data);
}

3️⃣ WhatsApp Status API

Handles WhatsApp status updates via the 360Dialog API.

Action

Method

Endpoint

Functionality

Get all statuses

GET

/status/

Retrieve all status updates.

Get a status

GET

/status/{id}/

Retrieve a specific status.

Post a status

POST

/status/

Schedule a WhatsApp status.

Delete a status

DELETE

/status/{id}/

Remove a status update.

Example: Post a Status

async function postStatus() {
    const response = await fetch("http://127.0.0.1:8000/status/", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
            text: "Good morning!",
            scheduled_at: "2025-02-20T10:00:00Z"
        })
    });
    const data = await response.json();
    console.log(data);
}

4️⃣ Group Management API

Handles automatic grouping of contacts.

Action

Method

Endpoint

Functionality

Get all groups

GET

/groups/

Retrieve a list of groups.

Get a group

GET

/groups/{id}/

Retrieve a specific group.

Create a group

POST

/groups/

Create a new WhatsApp group.

Delete a group

DELETE

/groups/{id}/

Remove an empty group.

Example: Fetch Groups

async function fetchGroups() {
    const response = await fetch("http://127.0.0.1:8000/groups/");
    const data = await response.json();
    console.log(data);
}

5️⃣ Auto-Fetch Contacts from WordPress

Contacts are automatically fetched from WordPress landing pages and assigned to groups.

Process:

The backend periodically pulls new contacts from the WordPress API.

Contacts are assigned to available WhatsApp groups.

If a group reaches the limit (250 contacts), a new group is created.

This is handled automatically by Celery in the backend.

6️⃣ Auto-Reply Feature

Automatically replies to incoming WhatsApp messages based on predefined logic.

Functionality

Handled By Backend

Auto-replies to messages

✅ Yes

💡 Notes for Frontend Team

No Authentication Required (for now)

All Requests Must Use JSON Format

Contacts from WordPress Are Auto-Fetched (No manual API request needed)

360Dialog API Handles Messaging and Status Updates (No additional setup required)

