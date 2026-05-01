# Attachments

* **Structure** (attachments.lua)

```
supportedAttachments = {
    tint = {
        -- Global weapon tints
    },
    ['weapon_name'] = {
        clip = {
            -- Clip attachments
        },
        scope = {
            -- Scope attachments
        },
        // Additional attachment types...
    }
}
```

*   **Required Fields for Each Attachment:**

    ```
    {
        component = "COMPONENT_ID",     -- GTA component ID
        bone = "BONE_NAME",            -- Attachment point
        label = "Display Name",        -- UI name
        image = "image_file.png",      -- UI image
        name = "at_type_variant",      -- ESX identifier (required for ESX)
        isDefault = true/false         -- Default component flag
    }
    ```


* **Framework-Specific Requirements**
  * ESX:
    * Requires 'name' field (e.g., 'at\_clip\_extended')

