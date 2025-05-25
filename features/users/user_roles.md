# Users

**What Roles are there in a bakery app?**

Admin Role - first user is likely owner/manager
- admin's id becomes the `CustomerID` used across all tables
- Create account with business email
- Add business details
- Setup additional roles for the daily users
- Can add/remove other users to the platform
- Will eventually have privileges for other features

Manager
- Will have most all of the permissions of the owner except to delete account or change certain details.
- Can add/remove users.
- Likely the one to manage daily bake quotas and inventory levels.

Baker
- core user of the app
- logs daily bakes which reduce inventory
- logs batches created to add to inventory
- can manually adjust inventory as needed (spoilage, etc)

**How does it work**
- roles file lives in the backend
- backend will expose an API endpoint for the frontend to consume
- frontend gets a sanitized version (in case any internal roles/permissions)

```json
{
  "roles": {
    "owner": {
      "description": "Account creator and business owner with full permissions.",
      "permissions": [        
				"invite_user",
        "remove_user",
        "assign_roles",
				"view_baking_schedule",
        "log_new_batch",
        "log_bake",
			],
		},
    "manager": {
      "description": "Manages daily operations and teams within assigned locations.",
      "permissions": [        
				"invite_user",
        "remove_user",
        "assign_roles",
				"view_baking_schedule",
        "log_new_batch",
        "log_bake",
			],
		},
		"baker": {
      "description": "Logs batches and bakes, and performs inventory-related tasks.",
      "permissions": [
				"view_baking_schedule",
        "log_new_batch",
        "log_bake",
			],
		}
	}
}
```